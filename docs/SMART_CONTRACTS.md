# GoNode Smart Contracts

**Document version:** Season 1 | April 2026
**Component:** GoNode smart contract specifications for Arbitrum One
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the smart contract interfaces that form the economic layer of GoNode. All contracts deploy to Arbitrum One mainnet and follow OpenZeppelin battle-tested patterns. Every function signature, event, and storage layout is documented here as the reference for auditors, integrators, and alternative implementations.

The economic layer consists of six contracts with distinct responsibilities:

| Contract | Purpose | Approximate LOC |
|:---------|:--------|:---------------|
| GoCoin | ERC-20 token with burn tracking | 150 |
| NodeStaking | Node registration and stake management | 300 |
| NodeRewards | Monthly emission and held-back payments | 400 |
| Subscription | Burn-and-mint for Pro subscriptions | 250 |
| Slashing | Evidence-based penalty enforcement | 350 |
| Governance | DAO voting and parameter updates | 300 |

**Language:** Solidity 0.8.24+
**Framework:** Hardhat for development, Foundry for testing
**Deployment:** Arbitrum One (chain ID 42161)
**Upgrade strategy:** Non-upgradeable for economic logic, timelock-guarded for parameters

---

## 1. Contract architecture

### 1.1 Deployment topology

```
+------------------------------------------------------+
|                     GoCoin (ERC-20)                  |
|  Burnable, non-mintable after initial distribution   |
+------------------------------------------------------+
          ^              ^               ^
          |              |               |
   +------+------+  +----+-----+  +-----+------+
   |             |  |          |  |            |
   | NodeStaking |  | Rewards  |  | Subscription
   |             |  |          |  |            |
   +------+------+  +----+-----+  +-----+------+
          ^              ^               ^
          |              |               |
          +------+-------+-------+-------+
                 |               |
                 v               v
          +-------------+  +-------------+
          | Slashing    |  | Governance  |
          |             |  |             |
          +-------------+  +-------------+
```

### 1.2 Deployment sequence

Contracts must be deployed in dependency order:

```
1. GoCoin (no dependencies)
2. NodeStaking (depends on GoCoin)
3. NodeRewards (depends on GoCoin, NodeStaking)
4. Subscription (depends on GoCoin, Uniswap V3 Router, EURC)
5. Slashing (depends on NodeStaking, NodeRewards)
6. Governance (depends on GoCoin)
7. Transfer ownership: Governance -> all contracts (Phase 4 only)
```

### 1.3 Access control roles

| Role | Held by (Phase 0-3) | Held by (Phase 4+) |
|:-----|:--------------------|:-------------------|
| DEFAULT_ADMIN | Foundation multisig (3/5) | Burned (address(0)) |
| REWARD_DISTRIBUTOR | Foundation service account | On-chain distributor with timelock |
| SLASH_SUBMITTER | 2/3 BFT validator quorum | Same |
| PAUSE_GUARDIAN | Foundation multisig | Removed entirely |
| PARAMETER_UPDATER | Foundation multisig + timelock | DAO vote + timelock |

---

## 2. GoCoin ERC-20 contract

### 2.1 Purpose

Standard ERC-20 token with these additions:

- Burn tracking (total burn, per-reason burn)
- Non-mintable after initial supply distribution
- Metadata URI for token info

### 2.2 Interface

```solidity
// SPDX-License-Identifier: AGPL-3.0
pragma solidity ^0.8.24;

interface IGoCoin is IERC20, IERC20Metadata {
    // Standard ERC-20 events inherited

    event TokensBurned(
        address indexed from,
        uint256 amount,
        bytes32 indexed reason
    );

    // Reasons are bytes32 for efficiency:
    // "SUB" = subscription burn
    // "SLASH" = slashing burn
    // "HELD" = held-back forfeiture
    // "ENT" = enterprise revenue burn
    // "AI" = AI service revenue burn
    // "MAN" = manual burn

    function maxSupply() external pure returns (uint256);  // 100M × 10^18
    function totalBurned() external view returns (uint256);
    function burnedByReason(bytes32 reason) external view returns (uint256);

    function burn(uint256 amount, bytes32 reason) external;
    function burnFrom(address from, uint256 amount, bytes32 reason) external;
}
```

### 2.3 Storage layout

```solidity
contract GoCoin {
    // Slot 0: inherited from ERC20
    mapping(address => uint256) private _balances;

    // Slot 1: inherited
    mapping(address => mapping(address => uint256)) private _allowances;

    // Slot 2: inherited
    uint256 private _totalSupply;

    // Slot 3: inherited metadata
    // ...

    // New slots for GoNode:
    uint256 public totalBurned;
    mapping(bytes32 => uint256) public burnedByReason;
}
```

### 2.4 Key functions

**`burn(uint256 amount, bytes32 reason)`**

```
Effect:
  - Decreases msg.sender balance by amount
  - Decreases totalSupply by amount
  - Increases totalBurned by amount
  - Increases burnedByReason[reason] by amount
  - Emits TokensBurned(msg.sender, amount, reason)

Gas cost: ~40,000

Reverts if:
  - msg.sender balance < amount
  - amount == 0 (protection against wasteful calls)
```

**`burnFrom(address from, uint256 amount, bytes32 reason)`**

```
Effect:
  - Requires allowance from `from` to msg.sender >= amount
  - Decreases `from` balance by amount
  - Decreases totalSupply by amount
  - Increases totalBurned by amount
  - Increases burnedByReason[reason] by amount
  - Emits TokensBurned(from, amount, reason)

Gas cost: ~50,000
```

### 2.5 Constructor

```solidity
constructor(
    address foundationTreasury,
    address teamVestingContract,
    address stakingContract,
    address rewardsContract
) ERC20("GoCoin", "GC") {
    uint256 totalMint = MAX_SUPPLY;  // 100M × 10^18

    // Initial circulating: 30M
    _mint(foundationTreasury, 30_000_000 * 10**18);

    // Reward pool: 40M (held in Rewards contract)
    _mint(rewardsContract, 40_000_000 * 10**18);

    // Foundation treasury vest: 15M
    _mint(foundationTreasury, 15_000_000 * 10**18);

    // Team vesting: 10M (held in vesting contract)
    _mint(teamVestingContract, 10_000_000 * 10**18);

    // Ecosystem grants: 5M (held in Governance)
    _mint(address(governance), 5_000_000 * 10**18);

    require(totalSupply() == MAX_SUPPLY, "minting error");

    // After constructor, no more minting possible (no mint function exposed)
}
```

---

## 3. NodeStaking contract

### 3.1 Purpose

Manages node registration, stake deposits, exit cooldowns, and slashing execution. Every active service node must have 10,000 GoCoin staked here.

### 3.2 Interface

```solidity
interface INodeStaking {
    struct StakeInfo {
        uint256 amount;              // Current stake amount
        uint256 exitRequestedAt;     // 0 if not exiting
        bytes32 operatorPubKey;      // Ed25519 public key (32 bytes)
        uint32 registeredEpoch;      // Epoch of registration
        bool active;                 // False after exit requested
    }

    event NodeRegistered(
        address indexed operator,
        bytes32 operatorPubKey,
        uint32 epoch
    );

    event NodeExitRequested(
        address indexed operator,
        uint256 withdrawableAt
    );

    event NodeExited(address indexed operator);

    event StakeSlashed(
        address indexed operator,
        uint256 amount,
        bytes32 reason
    );

    function STAKE_AMOUNT() external pure returns (uint256);  // 10,000 × 10^18
    function EXIT_COOLDOWN() external pure returns (uint256); // 48 hours
    function HELDBACK_COOLDOWN() external pure returns (uint256); // 270 days

    function getStakeInfo(address operator) external view returns (StakeInfo memory);
    function isActive(address operator) external view returns (bool);
    function activeNodeCount() external view returns (uint256);
    function getCurrentEpoch() external view returns (uint32);

    function registerNode(bytes32 operatorPubKey) external;
    function requestExit() external;
    function withdrawStake() external;

    // Only callable by Slashing contract
    function slash(address operator, uint256 amount, bytes32 reason) external;
}
```

### 3.3 State machine

```
UNREGISTERED
    |
    | registerNode() + 10k GC transfer
    v
ACTIVE
    |
    | requestExit()
    v
EXITING (48h cooldown)
    |
    | 48h elapses + withdrawStake()
    v
WITHDRAWN (UNREGISTERED again)

From ACTIVE:
    | slash() from Slashing contract
    v
    (stake reduced, may still be ACTIVE if stake > minimum)

From EXITING:
    | slash() still possible during cooldown
    v
    (reduced withdrawal amount)
```

### 3.4 Key functions

**`registerNode(bytes32 operatorPubKey)`**

```solidity
function registerNode(bytes32 operatorPubKey) external {
    require(!stakes[msg.sender].active, "already active");
    require(operatorPubKey != bytes32(0), "invalid pubkey");

    // Transfer stake from operator
    goCoin.transferFrom(msg.sender, address(this), STAKE_AMOUNT);

    // Record stake
    stakes[msg.sender] = StakeInfo({
        amount: STAKE_AMOUNT,
        exitRequestedAt: 0,
        operatorPubKey: operatorPubKey,
        registeredEpoch: getCurrentEpoch(),
        active: true
    });
    activeNodeCount_++;

    emit NodeRegistered(msg.sender, operatorPubKey, getCurrentEpoch());
}
```

Gas cost: approximately 150,000 (dominated by storage write + ERC-20 transfer).

**`requestExit()`**

```solidity
function requestExit() external {
    require(stakes[msg.sender].active, "not active");
    require(stakes[msg.sender].exitRequestedAt == 0, "already exiting");

    stakes[msg.sender].exitRequestedAt = block.timestamp;
    stakes[msg.sender].active = false;
    activeNodeCount_--;

    emit NodeExitRequested(
        msg.sender,
        block.timestamp + EXIT_COOLDOWN
    );
}
```

Gas cost: approximately 50,000.

**`withdrawStake()`**

```solidity
function withdrawStake() external {
    StakeInfo memory info = stakes[msg.sender];
    require(info.exitRequestedAt > 0, "exit not requested");
    require(
        block.timestamp >= info.exitRequestedAt + EXIT_COOLDOWN,
        "cooldown active"
    );

    uint256 amount = info.amount;
    delete stakes[msg.sender];

    goCoin.transfer(msg.sender, amount);
    emit NodeExited(msg.sender);
}
```

Gas cost: approximately 60,000.

---

## 4. Subscription contract (burn-and-mint core)

### 4.1 Purpose

The central economic mechanism: accepts EURC, buys GoCoin on Uniswap, burns it, and activates Pro subscription. This is the contract that users interact with for Pro.

### 4.2 Interface

```solidity
interface ISubscription {
    event ProActivated(
        address indexed user,
        uint256 expiresAt,
        uint256 goCoinBurned,
        uint256 eurcPaid
    );

    event ProExtended(
        address indexed user,
        uint256 newExpiresAt,
        uint256 goCoinBurned,
        uint256 eurcPaid
    );

    event AnnualProActivated(
        address indexed user,
        uint256 expiresAt,
        uint256 goCoinBurned,
        uint256 eurcPaid
    );

    function MONTHLY_PRICE_EURC() external pure returns (uint256); // 5 × 10^6
    function ANNUAL_PRICE_EURC() external pure returns (uint256);  // 50 × 10^6
    function MONTHLY_DURATION() external pure returns (uint256);   // 30 days
    function ANNUAL_DURATION() external pure returns (uint256);    // 365 days

    function proExpires(address user) external view returns (uint256);
    function isProUser(address user) external view returns (bool);
    function totalBurnedForSubscriptions() external view returns (uint256);
    function totalSubscriptionCount() external view returns (uint256);

    function subscribe() external;          // Monthly, requires EURC approval
    function subscribeAnnual() external;    // Annual, 50 EURC
    function subscribeFor(address user) external;  // Gift/pay-for-someone-else
}
```

### 4.3 Key function

**`subscribe()` - The core burn-and-mint mechanism**

```solidity
function subscribe() external nonReentrant {
    _executeSubscription(msg.sender, MONTHLY_PRICE_EURC, MONTHLY_DURATION);
}

function _executeSubscription(
    address user,
    uint256 priceEurc,
    uint256 duration
) internal {
    // Pull EURC from user
    eurc.transferFrom(msg.sender, address(this), priceEurc);

    // Approve Uniswap to spend EURC
    eurc.approve(address(uniswapRouter), priceEurc);

    // Build swap params
    ISwapRouter.ExactInputSingleParams memory params = ISwapRouter.ExactInputSingleParams({
        tokenIn: address(eurc),
        tokenOut: address(goCoin),
        fee: UNISWAP_POOL_FEE,
        recipient: address(this),
        deadline: block.timestamp + 300,
        amountIn: priceEurc,
        amountOutMinimum: 0,  // Accept any amount (private mempool protection)
        sqrtPriceLimitX96: 0
    });

    // Execute swap on Uniswap V3
    uint256 goCoinReceived = uniswapRouter.exactInputSingle(params);

    // Burn all the GoCoin
    goCoin.burn(goCoinReceived, bytes32("SUB"));

    totalBurnedForSubscriptions += goCoinReceived;
    totalSubscriptionCount += 1;

    // Activate Pro subscription
    uint256 newExpiry;
    uint256 currentExpiry = proExpires[user];
    if (currentExpiry > block.timestamp) {
        // Extend existing
        newExpiry = currentExpiry + duration;
        emit ProExtended(user, newExpiry, goCoinReceived, priceEurc);
    } else {
        // Activate new
        newExpiry = block.timestamp + duration;
        emit ProActivated(user, newExpiry, goCoinReceived, priceEurc);
    }
    proExpires[user] = newExpiry;
}
```

Gas cost: approximately 250,000 (includes Uniswap swap + burn + storage write).

### 4.4 MEV protection

The `amountOutMinimum` is set to 0 to prevent MEV-based griefing. Protection against sandwich attacks is provided by:

1. **Private mempool:** Foundation-operated RPC for Pro transactions routes through Flashbots Protect or equivalent
2. **Pool depth:** 500,000 EURC initial liquidity makes small trades negligible price impact
3. **Multi-pool routing:** If primary pool has issues, fallback to other pools
4. **Circuit breaker:** If unusual price movement detected, reject transaction with informative error

### 4.5 Revenue flow visualization

```
User wallet (5 EURC)
    |
    | subscribe() call
    v
Subscription contract (receives 5 EURC)
    |
    | exactInputSingle() to Uniswap V3
    v
Uniswap V3 EURC/GC pool
    |
    | GoCoin minted at current market rate
    v
Subscription contract (now holds X GoCoin, no EURC)
    |
    | burn(X, "SUB")
    v
GoCoin balance decreases, totalBurned increases
    |
    | proExpires[user] = block.timestamp + 30 days
    v
User sees: "Pro active until DD.MM.YYYY"
```

---

## 5. NodeRewards contract

### 5.1 Purpose

Distributes monthly GoCoin emissions to active service nodes, implements the held-back payment structure, and manages claim logic.

### 5.2 Interface

```solidity
interface INodeRewards {
    struct EmissionSchedule {
        uint32 startMonth;
        uint32 endMonth;
        uint256 monthlyAmount;
    }

    event RewardsDistributed(
        uint32 indexed month,
        address[] nodes,
        uint256 totalDistributed
    );

    event HeldBackClaimed(
        address indexed operator,
        uint256 amount
    );

    event HeldBackBurned(
        address indexed operator,
        uint256 amount,
        bytes32 reason
    );

    function monthlyEmissions(uint32 month) external view returns (uint256);
    function earnings(address operator, uint32 month) external view returns (uint256);
    function heldBackAmount(address operator) external view returns (uint256);
    function nextHeldBackRelease(address operator) external view returns (uint32);

    function distributeRewards(
        uint32 month,
        address[] calldata nodes,
        uint256[] calldata weights
    ) external;

    function claimHeldBack() external;
    function burnHeldBack(address operator) external; // called by Slashing
}
```

### 5.3 Distribution logic

Each month, the Reward Distributor role calls `distributeRewards` with the month's emission and the per-node weights:

```solidity
function distributeRewards(
    uint32 month,
    address[] calldata nodes,
    uint256[] calldata weights
) external onlyRewardDistributor {
    require(nodes.length == weights.length, "length mismatch");
    require(!distributed[month], "already distributed");

    uint256 totalWeight = 0;
    for (uint i = 0; i < weights.length; i++) {
        totalWeight += weights[i];
    }
    require(totalWeight > 0, "zero total weight");

    uint256 emission = monthlyEmissions[month];
    require(emission > 0, "no emission for month");

    for (uint i = 0; i < nodes.length; i++) {
        uint256 earned = (emission * weights[i]) / totalWeight;
        earnings[nodes[i]][month] = earned;

        // Split between immediate payout and held-back
        uint32 monthsActive = getMonthsActive(nodes[i]);
        (uint256 payout, uint256 held) = splitPayout(earned, monthsActive);

        if (payout > 0) {
            goCoin.transfer(nodes[i], payout);
        }
        if (held > 0) {
            heldBack[nodes[i]] += held;
            nextHeldBackRelease[nodes[i]] = uint32(block.timestamp + 270 days);
        }
    }

    distributed[month] = true;
    emit RewardsDistributed(month, nodes, emission);
}
```

### 5.4 Held-back logic

```solidity
function splitPayout(uint256 earned, uint32 monthsActive)
    internal pure returns (uint256 payout, uint256 held)
{
    if (monthsActive < 4) {
        // Months 1-3: 50% paid, 50% held
        return (earned / 2, earned / 2);
    } else if (monthsActive < 7) {
        // Months 4-6: 75% paid, 25% held
        return (earned * 3 / 4, earned / 4);
    } else {
        // Month 7+: 100% paid
        return (earned, 0);
    }
}

function claimHeldBack() external nonReentrant {
    require(heldBack[msg.sender] > 0, "nothing held");
    require(
        block.timestamp >= nextHeldBackRelease[msg.sender],
        "cooldown active"
    );

    uint256 amount = heldBack[msg.sender];
    heldBack[msg.sender] = 0;
    nextHeldBackRelease[msg.sender] = uint32(block.timestamp + 270 days);

    goCoin.transfer(msg.sender, amount);
    emit HeldBackClaimed(msg.sender, amount);
}
```

### 5.5 Gas costs

| Operation | Gas Cost | Notes |
|:----------|:---------|:------|
| distributeRewards (100 nodes) | ~3,000,000 | O(n), amortized 30k per node |
| distributeRewards (1000 nodes) | ~30,000,000 | Approaches block gas limit |
| claimHeldBack | ~80,000 | Single-operator operation |

**Batching strategy:** For networks >500 nodes, distribution is split across multiple transactions for the same month to stay under block gas limit.

---

## 6. Slashing contract

### 6.1 Purpose

Processes evidence of operator misbehaviour and executes slashing actions. Uses BFT validator quorum to prevent single-actor attacks.

### 6.2 Interface

```solidity
interface ISlashing {
    enum OffenseType {
        Equivocation,       // 5% slash
        CorruptedData,      // 5% slash
        Censorship,         // 10% slash
        MaliciousAudit      // 20% slash
    }

    struct Evidence {
        address accused;
        OffenseType offenseType;
        bytes evidenceData;
        bytes[] validatorSignatures;
        uint256 submittedAt;
    }

    event EvidenceSubmitted(
        address indexed accuser,
        address indexed accused,
        OffenseType offense
    );

    event OffenseConfirmed(
        address indexed accused,
        OffenseType offense,
        uint256 stakeSlashed,
        uint256 heldBackBurned
    );

    event EvidenceDisputed(
        address indexed accused,
        uint256 disputeDeadline
    );

    function submitEvidence(
        address accused,
        OffenseType offenseType,
        bytes calldata evidenceData,
        bytes[] calldata validatorSignatures
    ) external;

    function disputeEvidence(
        uint256 evidenceId,
        bytes calldata counterEvidence
    ) external;

    function finaliseSlashing(uint256 evidenceId) external;

    function getSlashPercent(OffenseType offense) external pure returns (uint256);
}
```

### 6.3 Slashing flow

```
Day 0: Evidence submitted
  - submitEvidence() with 2/3+ validator signatures
  - EvidenceSubmitted event emitted
  - 72-hour dispute window begins

Day 0-3: Dispute period
  - Accused operator can submit counter-evidence
  - If no dispute: evidence stands
  - If dispute: further validator vote (another 48 hours)

Day 3-5: Finalisation
  - finaliseSlashing() called
  - Stake slashed per OffenseType
  - Held-back burned 100%
  - OffenseConfirmed event emitted

Day 5: Operator status updated
  - If stake falls below minimum: automatic deregistration
  - If stake remains above minimum: operator continues but with reputation hit
```

### 6.4 Validator quorum

```solidity
function submitEvidence(
    address accused,
    OffenseType offenseType,
    bytes calldata evidenceData,
    bytes[] calldata validatorSignatures
) external {
    require(validatorSignatures.length >= getQuorumSize(), "insufficient quorum");

    // Verify each signature is from a registered validator
    address[] memory validators = getCurrentValidators();
    uint256 validSigCount = 0;
    bytes32 evidenceHash = keccak256(abi.encode(accused, offenseType, evidenceData));

    for (uint i = 0; i < validatorSignatures.length; i++) {
        address signer = recoverSigner(evidenceHash, validatorSignatures[i]);
        if (isValidator(signer, validators)) {
            validSigCount++;
        }
    }

    require(validSigCount >= getQuorumSize(), "insufficient valid signatures");

    // Verify evidence format
    require(verifyEvidenceFormat(offenseType, evidenceData), "invalid evidence format");

    // Store evidence and open dispute window
    uint256 evidenceId = nextEvidenceId++;
    allEvidence[evidenceId] = Evidence({
        accused: accused,
        offenseType: offenseType,
        evidenceData: evidenceData,
        validatorSignatures: validatorSignatures,
        submittedAt: block.timestamp
    });

    emit EvidenceSubmitted(msg.sender, accused, offenseType);
}

function getQuorumSize() public view returns (uint256) {
    uint256 totalValidators = getCurrentValidators().length;
    return (totalValidators * 2) / 3 + 1;  // 2/3 + 1
}
```

---

## 7. Governance contract

### 7.1 Purpose

Enables on-chain proposal submission and voting. Used starting Phase 3 for non-critical parameters, and for all protocol governance from Phase 4 onwards.

### 7.2 Interface

```solidity
interface IGovernance {
    enum ProposalType {
        ParameterChange,
        GrantAllocation,
        ContractUpgrade,
        ProtocolChange
    }

    enum ProposalState {
        Pending,
        Active,
        Succeeded,
        Failed,
        Executed,
        Cancelled
    }

    struct Proposal {
        uint256 id;
        address proposer;
        ProposalType proposalType;
        bytes proposalData;
        uint256 startTime;
        uint256 endTime;
        uint256 forVotes;
        uint256 againstVotes;
        uint256 abstainVotes;
        ProposalState state;
        bytes executionPayload;
    }

    event ProposalCreated(
        uint256 indexed proposalId,
        address indexed proposer,
        ProposalType proposalType,
        string description
    );

    event VoteCast(
        address indexed voter,
        uint256 indexed proposalId,
        uint8 support,  // 0=against, 1=for, 2=abstain
        uint256 weight
    );

    event ProposalExecuted(uint256 indexed proposalId);

    function proposalCount() external view returns (uint256);
    function proposals(uint256 proposalId) external view returns (Proposal memory);
    function getQuorum(ProposalType proposalType) external view returns (uint256);
    function getMajority(ProposalType proposalType) external pure returns (uint256);

    function createProposal(
        ProposalType proposalType,
        bytes calldata proposalData,
        bytes calldata executionPayload,
        string calldata description
    ) external returns (uint256);

    function castVote(uint256 proposalId, uint8 support) external;

    function queueForExecution(uint256 proposalId) external;
    function executeProposal(uint256 proposalId) external;
}
```

### 7.3 Voting parameters

| Proposal Type | Quorum | Majority | Deliberation |
|:-------------|:-------|:---------|:-------------|
| ContractUpgrade | 20% of circulating | 75% yes | 30 days |
| ProtocolChange | 15% of circulating | 66% yes | 14 days |
| ParameterChange | 10% of circulating | 50%+1 yes | 7 days |
| GrantAllocation | 5% of circulating | 50%+1 yes | 3 days |

### 7.4 Timelock

All successful proposals execute through a 2-day timelock for additional safety:

```
Day 0: Vote passes
Day 0-2: Timelock period (can be cancelled by foundation multisig if emergency)
Day 2: Execution callable
```

---

## 8. Auxiliary contracts

### 8.1 TokenVesting

Used for team and advisor allocations. Standard OpenZeppelin VestingWallet with these parameters:

| Beneficiary Category | Total | Cliff | Duration |
|:-------------------|:------|:------|:---------|
| Founding team | 6M GC | 1 year | 4 years linear |
| Core team | 2.5M GC | 1 year | 4 years linear |
| Advisors | 1M GC | None | 2 years linear |
| Early contributors | 500k GC | None | 2 years linear |

### 8.2 MultiSigWallet

Standard Gnosis Safe 3-of-5 for foundation operations. Signers include:

- Founder (Sascha Daemgen)
- Technical lead
- Legal counsel
- External advisor
- External advisor

### 8.3 Timelock

OpenZeppelin Timelock with:

- Delay: 2 days for all operations
- Admin: multisig wallet
- Cancellable by guardian address

---

## 9. Deployment checklist

### 9.1 Pre-deployment

- [ ] All contracts compiled with Solidity 0.8.24
- [ ] Unit tests with 95%+ coverage (Hardhat + Foundry)
- [ ] Integration tests covering all user flows
- [ ] Gas optimisation pass
- [ ] Static analysis (Slither, Mythril) clean
- [ ] First security audit complete
- [ ] Second security audit complete
- [ ] Bug bounty active on testnet

### 9.2 Deployment script

```javascript
// scripts/deploy.js (simplified)
const hre = require("hardhat");

async function main() {
    // 1. Deploy GoCoin
    const GoCoin = await hre.ethers.deployContract("GoCoin", [
        foundationTreasury,
        teamVestingContract,
        stakingContract,
        rewardsContract
    ]);
    await GoCoin.waitForDeployment();

    // 2. Deploy NodeStaking
    const Staking = await hre.ethers.deployContract("NodeStaking", [
        GoCoin.target
    ]);

    // 3. Deploy NodeRewards
    const Rewards = await hre.ethers.deployContract("NodeRewards", [
        GoCoin.target,
        Staking.target
    ]);

    // 4. Deploy Subscription
    const Subscription = await hre.ethers.deployContract("Subscription", [
        EURC_ADDRESS,
        GoCoin.target,
        UNISWAP_V3_ROUTER
    ]);

    // 5. Deploy Slashing
    const Slashing = await hre.ethers.deployContract("Slashing", [
        Staking.target,
        Rewards.target
    ]);

    // 6. Deploy Governance
    const Governance = await hre.ethers.deployContract("Governance", [
        GoCoin.target,
        TIMELOCK_ADDRESS
    ]);

    // 7. Configure access control
    await Staking.grantRole(SLASH_ROLE, Slashing.target);
    await Rewards.grantRole(BURN_HELDBACK_ROLE, Slashing.target);

    console.log("Deployment complete");
    console.log({
        GoCoin: GoCoin.target,
        Staking: Staking.target,
        Rewards: Rewards.target,
        Subscription: Subscription.target,
        Slashing: Slashing.target,
        Governance: Governance.target
    });
}
```

### 9.3 Post-deployment

- [ ] Verify all contracts on Arbiscan
- [ ] Transfer ownership to Timelock/Multisig
- [ ] Initialize emission schedule in Rewards
- [ ] Seed initial Uniswap V3 liquidity pool
- [ ] Publish deployment addresses to documentation
- [ ] Announce deployment to community
- [ ] Monitor contracts for first 48 hours

---

## 10. Gas cost summary

Estimated costs at typical Arbitrum gas prices (0.1 gwei, $2000 ETH):

| Operation | Gas | Cost (USD) |
|:----------|:----|:-----------|
| Deploy GoCoin | ~1,500,000 | $0.30 |
| Deploy NodeStaking | ~2,000,000 | $0.40 |
| Deploy NodeRewards | ~2,500,000 | $0.50 |
| Deploy Subscription | ~2,500,000 | $0.50 |
| Deploy Slashing | ~2,500,000 | $0.50 |
| Deploy Governance | ~3,000,000 | $0.60 |
| **Total deployment** | ~14,000,000 | **~$2.80** |
| | | |
| registerNode() | ~150,000 | $0.003 |
| requestExit() | ~50,000 | $0.001 |
| withdrawStake() | ~60,000 | $0.001 |
| subscribe() | ~250,000 | $0.005 |
| claimHeldBack() | ~80,000 | $0.002 |
| submitEvidence() | ~400,000 | $0.008 |
| distributeRewards (100 nodes) | ~3,000,000 | $0.06 |
| castVote() | ~70,000 | $0.001 |

All costs are negligible relative to transaction value and do not affect unit economics.

---

## 11. Testing and verification

### 11.1 Test coverage

All contracts must achieve 95%+ test coverage before deployment:

```
Unit tests (Hardhat):
  - Each function in isolation
  - Edge cases (overflow, zero, max values)
  - Access control checks
  - Event emissions

Integration tests (Foundry):
  - Full subscription flow (EURC -> swap -> burn -> Pro)
  - Full registration flow (stake -> active -> exit -> withdraw)
  - Full slashing flow (evidence -> dispute -> finalise)
  - Cross-contract interactions

Fuzz tests (Foundry):
  - Invariants across all state changes
  - No negative balances
  - totalSupply = sum(balances)
  - totalBurned = totalSupply_before - totalSupply_current
```

### 11.2 Formal verification (optional)

For highest-risk contract paths:

| Contract | Method | Scope |
|:---------|:-------|:------|
| GoCoin | Symbolic execution | Burn accounting invariants |
| Subscription | Model checking | State transitions |
| Slashing | Proof assistant | Evidence validation logic |

### 11.3 Continuous monitoring

Post-deployment monitoring:

- Forta agents on all contracts
- Defender sentinels for critical functions
- Dashboard tracking metrics (TVL, TVB = Total Value Burned)
- Alerting on anomalies (unusual burn volumes, large withdrawals, rapid slashing)

---

## 12. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [GoNode Architecture](ARCHITECTURE_AND_SECURITY.md) | Smart contract threat model | This repo |
| [GoNode Tokenomics](TOKENOMICS.md) | Economic parameters | This repo |
| [GoNode Wire Protocol](WIRE_PROTOCOL.md) | Off-chain counterpart | This repo |
| [GoNode Roadmap](ROADMAP.md) | Deployment timing | This repo |

---

*GoNode Smart Contracts v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
