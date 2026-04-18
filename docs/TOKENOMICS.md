# GoNode Tokenomics

**Document version:** Season 1 | April 2026
**Component:** GoCoin (GC) - utility token for the GoNode network
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

GoCoin (ticker: GC) is the native utility token of the GoNode decentralised infrastructure network. This document specifies the complete economic design: supply, distribution, emission schedule, burn mechanism, operator incentives, treasury management and governance.

GoCoin is deliberately designed as a utility token under MiCA Article 3(1)(9) ("other crypto-assets"), avoiding security, asset-referenced, and e-money token classifications. Users never touch GoCoin directly - they pay 5 EURC per month for GoNode Pro, and smart contracts handle the conversion and burn automatically. GoCoin is an incentive instrument for node operators, not a consumer-facing currency.

The tokenomic design is patterned after Helium's burn-and-mint equilibrium (proven at 2 million monthly active users post-2025 consolidation) and Storj's held-back payment model (proven at thousands of storage nodes). Every parameter has been calibrated against real operational data from comparable networks.

---

## 1. Token specifications

| Parameter | Value |
|:----------|:------|
| Token name | GoCoin |
| Ticker | GC |
| Standard | ERC-20 |
| Deployment chain | Arbitrum One |
| Decimals | 18 |
| Maximum supply | 100,000,000 GC (fixed, non-mintable after initial deployment) |
| Initial circulating supply (TGE) | 30,000,000 GC |
| Node stake requirement | 10,000 GC per node |
| Initial DEX price target | 0.10 EURC per GC |
| Initial market cap target | 3,000,000 EURC (30M circulating × 0.10) |
| Fully diluted valuation target | 10,000,000 EURC (100M × 0.10) |

**Contract address:** To be published at TGE (Phase 3). Will be announced via:
- GitHub release notes
- Foundation website (simplego.dev)
- Token registries (CoinGecko, CoinMarketCap, Arbiscan)
- Verified on Arbiscan with Solidity source

---

## 2. Supply distribution

Total supply of 100,000,000 GoCoin is distributed across five allocations:

| Allocation | Amount | % of Supply | Vesting |
|:-----------|:-------|:-----------:|:--------|
| Initial Circulating | 30,000,000 | 30% | Released at TGE (see section 2.1) |
| Node Reward Pool | 40,000,000 | 40% | Emitted over 10 years per schedule in section 3 |
| Foundation Treasury | 15,000,000 | 15% | 4-year linear vest, 1-year cliff |
| Team and Advisors | 10,000,000 | 10% | 4-year linear vest, 1-year cliff |
| Ecosystem Grants | 5,000,000 | 5% | Released by DAO vote as needed |

### 2.1 Initial circulating breakdown (30M at TGE)

| Purpose | Amount | Notes |
|:--------|:-------|:------|
| SimpleGo Community Airdrop | 10,000,000 | Early SimpleGo/GoBot/GoLab users. Migration incentive. |
| DEX Initial Liquidity | 5,000,000 | Paired with 500,000 EURC in Uniswap V3 pool. Foundation treasury. |
| Service Node Bonus Program | 5,000,000 | First 200 operators. 25,000 GC each, locked 1 year. |
| Strategic Round (optional) | 5,000,000 | Private sale to strategic investors at 0.20 EURC. 2-year lock. |
| Liquidity Mining Rewards | 3,000,000 | Uniswap LP incentives over 2 years. |
| Grant Program / Bounties | 2,000,000 | Code audits, integrations, marketing campaigns. |

### 2.2 Foundation treasury vesting (15M)

Foundation treasury follows a 4-year linear vest with 1-year cliff:

| Month | Cumulative Vested | Available for Operations |
|:------|:------------------|:-------------------------|
| 0 (TGE) | 0 | 0 |
| 12 (cliff) | 3,750,000 GC | 3,750,000 GC |
| 24 | 7,500,000 GC | 3,750,000 GC new |
| 36 | 11,250,000 GC | 3,750,000 GC new |
| 48 | 15,000,000 GC | 3,750,000 GC new |

After the cliff, ~312,500 GC per month vests. Used for Foundation operating expenses, grants to developers, bounties, and emergency reserves.

### 2.3 Team and advisors vesting (10M)

Team allocations follow the same 4-year/1-year-cliff schedule as the Foundation. Individual allocations:

| Role | Allocation | Notes |
|:-----|:-----------|:------|
| Founding team (Sascha + co-founders) | 6,000,000 GC | Vested per founder agreement |
| Core engineering team (first 10 hires) | 2,500,000 GC | Individual vesting |
| Strategic advisors | 1,000,000 GC | 2-year vest, no cliff |
| Early contributors (pre-TGE) | 500,000 GC | Retroactive recognition, 2-year vest |

### 2.4 Ecosystem grants (5M)

Released incrementally by DAO vote (Foundation-controlled until Phase 4, then fully DAO). Allocation targets:

| Category | Typical Grant | Examples |
|:---------|:--------------|:---------|
| Protocol integrations | 50,000 - 200,000 GC | Wallet integrations, exchange listings, SDK development |
| Community tools | 10,000 - 50,000 GC | Block explorers, analytics dashboards, operator tools |
| Security research | 50,000 - 500,000 GC | Formal verification, audit contributions, bug bounties |
| Translations and documentation | 5,000 - 25,000 GC | Multilingual docs, video tutorials, educational content |
| Third-party GoNode clients | 100,000 - 500,000 GC | Alternative client implementations (Rust, Python, Swift) |

---

## 3. Emission schedule

The 40,000,000 GoCoin Node Reward Pool is emitted over 10 years following a modified Bitcoin-style halving curve. Emission decays as the network matures and burn increases.

### 3.1 Annual emission curve

| Period | Annual Rate | Annual Emission | Monthly Emission | Cumulative |
|:-------|:------------|:----------------|:-----------------|:-----------|
| Year 1 | 12.0% of pool | 4,800,000 GC | 400,000 GC | 4,800,000 |
| Year 2 | 12.0% | 4,800,000 GC | 400,000 GC | 9,600,000 |
| Year 3 | 10.0% | 4,000,000 GC | 333,333 GC | 13,600,000 |
| Year 4 | 10.0% | 4,000,000 GC | 333,333 GC | 17,600,000 |
| Year 5 | 8.0% | 3,200,000 GC | 266,666 GC | 20,800,000 |
| Year 6 | 8.0% | 3,200,000 GC | 266,666 GC | 24,000,000 |
| Year 7 | 6.0% | 2,400,000 GC | 200,000 GC | 26,400,000 |
| Year 8 | 6.0% | 2,400,000 GC | 200,000 GC | 28,800,000 |
| Year 9 | 4.0% | 1,600,000 GC | 133,333 GC | 30,400,000 |
| Year 10 | 4.0% | 1,600,000 GC | 133,333 GC | 32,000,000 |
| Year 11+ | Residual | ~1,000,000 GC/yr | ~83,333 GC | Reaches 40M over 18 more years |

Residual 8,000,000 GoCoin from year 11 onward serves as long-term operator rewards, supplemented by protocol fees (section 6).

### 3.2 Monthly reward distribution

Each month, the emission amount is distributed across all eligible service nodes proportional to their performance weight:

```
node_reward = monthly_emission × (node_weight / total_network_weight)

where node_weight = uptime × correctness × diversity × tenure
```

**Weight components:**

| Component | Range | How computed |
|:----------|:------|:-------------|
| `uptime` | 0.0 - 1.0 | Fraction of epoch node was responsive |
| `correctness` | 0.0 - 1.0 | Fraction of audit challenges answered correctly |
| `diversity` | 0.8 - 1.5 | ASN and geographic diversity bonus (more diverse = higher) |
| `tenure` | 1.0 - 1.3 | Bonus for long-term operation (reaches 1.3 at 24 months) |

### 3.3 Expected operator earnings by year

Assumptions: target network of 500 nodes in year 1 growing to 2,000 nodes in year 5. Reward weight distribution: Gini coefficient of 0.3 (moderately unequal but not extreme).

| Year | Total Emission | Network Nodes | Average Monthly Reward per Node | USD Value (at $0.10/GC) | USD Value (at $0.50/GC) |
|:-----|:---------------|:-------------:|:-------------------------------:|:------------------------:|:------------------------:|
| 1 | 4,800,000 GC | 500 | 800 GC | $80 | $400 |
| 2 | 4,800,000 GC | 1,000 | 400 GC | $40 | $200 |
| 3 | 4,000,000 GC | 1,500 | 222 GC | $22 | $111 |
| 4 | 4,000,000 GC | 1,800 | 185 GC | $18.50 | $92.50 |
| 5 | 3,200,000 GC | 2,000 | 133 GC | $13.30 | $66.50 |

**Reading this table:** As the network grows and emission decays, nominal GC rewards per node decrease. However, burn pressure (section 4) means GC value tends to rise over the same period. Operators earn less nominal GC but each GC is worth more. Net USD value should remain stable or grow slightly.

---

## 4. The burn-and-mint equilibrium

The core economic design of GoCoin. User subscriptions create demand for GC through automatic buy-and-burn. Operator emissions create supply. The interaction determines long-term token value.

### 4.1 How burn works

Every Pro subscription executes this sequence automatically in a single transaction:

```
Step 1: User pays 5 EURC to SubscriptionContract
Step 2: SubscriptionContract sells 5 EURC on Uniswap for GC
Step 3: SubscriptionContract burns 100% of received GC
Step 4: SubscriptionContract activates Pro for 30 days
```

The amount of GC burned depends on the current GC/EURC price:

| GC Price (EURC) | GC burned per subscription |
|:----------------|:---------------------------|
| 0.05 | 100 GC |
| 0.10 | 50 GC |
| 0.25 | 20 GC |
| 0.50 | 10 GC |
| 1.00 | 5 GC |

**Key property:** EUR-denominated burn is constant (5 EURC per subscription), but GC-denominated burn is inversely proportional to price. When GC is cheap, more is burned. This creates a self-stabilising price floor.

### 4.2 Burn sources beyond Pro subscriptions

Additional burn sources contribute to supply reduction:

| Source | Mechanism | Estimated Year 5 Burn |
|:-------|:----------|:----------------------|
| Pro subscriptions | 100% of EURC -> GC swap -> burn | 6,000,000 EURC/yr |
| Enterprise SLA contracts | 30% of fiat revenue converted to GC and burned | 1,080,000 EURC/yr |
| Slashing penalties | Slashed stake burned (not redistributed) | Variable, ~100,000 GC/yr |
| Disqualified node held-back | 100% held-back burn on disqualification | Variable, ~50,000 GC/yr |
| AI Service revenue | 20% of revenue converted to GC and burned | 240,000 EURC/yr |

### 4.3 Net supply dynamics by year

Assumes network grows and token price appreciates per projections:

| Year | Emission (GC) | Burn Value (EURC) | Burn at avg price | Net change (GC) | Circulating (end of year) |
|:-----|:--------------|:------------------|:------------------|:----------------|:--------------------------|
| Launch | - | - | - | - | 30,000,000 |
| Year 1 | 4,800,000 | 30,000 | 300,000 GC @ 0.10 | +4,500,000 | 34,500,000 |
| Year 2 | 4,800,000 | 210,000 | 1,400,000 GC @ 0.15 | +3,400,000 | 37,900,000 |
| Year 3 | 4,000,000 | 720,000 | 3,600,000 GC @ 0.20 | +400,000 | 38,300,000 |
| Year 4 | 4,000,000 | 2,400,000 | 8,000,000 GC @ 0.30 | -4,000,000 | 34,300,000 |
| Year 5 | 3,200,000 | 6,000,000 | 12,000,000 GC @ 0.50 | -8,800,000 | 25,500,000 |
| Year 7 | 2,400,000 | 15,000,000 | 20,000,000 GC @ 0.75 | -17,600,000 | Below 20M |

**Key transition:** Around Year 3-4, burn begins to exceed emission. From Year 4 onwards, GoCoin is net deflationary, creating sustained price pressure upward.

### 4.4 Comparison with other burn-and-mint networks

| Network | Fee Denomination | Burn Mechanism | Year to Net Deflation |
|:--------|:-----------------|:---------------|:----------------------|
| Helium | USD (via Data Credits) | HNT -> Data Credits | Year 5 (achieved 2024) |
| Ethereum (EIP-1559) | ETH (native) | Base fee burn | Year 1 (2021) |
| BNB Chain | BNB (native) | Quarterly team burns | Ongoing |
| **GoNode** | **EUR (via EURC)** | **EURC -> GC -> burn** | **Projected Year 4** |

GoNode's design explicitly follows Helium's post-2025 model, which consolidated MOBILE and IOT back into HNT after the sub-token experiment failed.

---

## 5. Operator economics

### 5.1 Starting a node

To operate a GoNode service node, an operator needs:

| Requirement | Cost |
|:------------|:-----|
| 10,000 GC stake | ~$1,000 USD at launch price |
| Hardware (adequate VPS or home server) | $20-50/month or $500 upfront |
| Internet connection (100 Mbps symmetric) | $50-100/month |
| Electricity | $5-15/month |
| Monitoring and maintenance | ~1 hour/week |

Total first-year cost (at minimum): approximately $1,500 USD.

### 5.2 Held-back payment structure

Following Storj's proven model, new operators receive rewards on a graduated schedule:

| Operator Age | % Paid Immediately | % Held Back | Rationale |
|:-------------|:-------------------|:------------|:----------|
| Months 1-3 | 50% | 50% | High abandonment risk in early period |
| Months 4-6 | 75% | 25% | Medium risk, proven short-term commitment |
| Months 7+ | 100% | 0% | Established operator |
| Month 10+ | Held-back unlocked | - | Graceful exit bonus |

**Held-back burn on disqualification:** If an operator is disqualified for misbehaviour before month 10, 100% of their held-back amount is burned. This creates strong economic disincentive to cut corners.

### 5.3 Breakeven analysis

For a typical home operator with moderate hardware:

```
Assumptions:
- Operator ran continuously for 12 months
- Network size: 1,000 active nodes
- Monthly emission: 400,000 GC
- Operator weight: average (1.0)
- No slashing

Year 1 earnings:
- Monthly emission share: 400 GC
- Actual payout months 1-3: 200 GC/mo = 600 GC paid, 600 GC held
- Actual payout months 4-6: 300 GC/mo = 900 GC paid, 300 GC held
- Actual payout months 7-12: 400 GC/mo = 2,400 GC paid
- Year 1 paid: 3,900 GC
- Year 1 held: 900 GC (unlocks month 10+)
- Year 1 total accrued: 4,800 GC

Year 1 revenue at $0.10/GC: $480
Year 1 revenue at $0.25/GC: $1,200
Year 1 revenue at $0.50/GC: $2,400

Year 1 costs: $1,500 (hardware + bandwidth + electricity)

Breakeven at $0.10/GC: Year 2+ (continuing operation reaches profitability)
Breakeven at $0.25/GC: mid-Year 1
Breakeven at $0.50/GC: month 4
```

**Profit amplification from burn:** As the network matures (Year 3+), increasing burn reduces circulating supply. Operator GC holdings appreciate. An operator running from Year 1 to Year 5 could see their held-back GC from Year 1 worth 5-10x by Year 5 if burn-deflation occurs as modeled.

### 5.4 Slashing consequences

| Offense | Stake slash | Held-back action | Result |
|:--------|:------------|:-----------------|:-------|
| Equivocation / double-signing | 5% (500 GC) | 100% burned | Immediate deregistration + reapply |
| Serving corrupted data | 5% (500 GC) | 100% burned | Immediate deregistration + reapply |
| Censorship | 10% (1,000 GC) | 100% burned | Deregistered for 90 days |
| Malicious audit | 20% (2,000 GC) | 100% burned | Permanent ban from network |
| Downtime > 24h | 0% | Kept | Deregistered from active set, can rejoin |

### 5.5 Exit mechanics

Operators can exit at any time, with these timelines:

```
Graceful exit:
  Day 0: Call requestExit() on staking contract
  Days 0-2: Node transfers stored data to replacement nodes
  Day 2: Stake and held-back unlockable
  Day 2+: Call withdrawStake() to retrieve GC

Forced exit (slashing):
  Day 0: Slashing evidence submitted and confirmed
  Day 0: Slash amount burned, node deregistered
  Day 0: Held-back amount burned
  Day 0: Remaining stake unlockable after 48h cooldown

Abandonment (node goes offline without exiting):
  After 7 days offline: node considered abandoned
  Held-back amount kept locked for 9 months
  Stake remains locked until operator returns
  Operator can rejoin by coming back online within 90 days
  After 90 days offline: operator must re-register
```

---

## 6. Protocol fees (future)

From Year 3 onward, the protocol can charge optional fees for advanced features. All fee revenue follows the burn-and-mint pattern.

### 6.1 Planned fee types

| Fee | Charged on | Rate | Purpose |
|:----|:-----------|:-----|:--------|
| Priority routing | Per-message for Pro+ users | 0.001 EURC | Guaranteed delivery speed |
| Archive storage | Per-GB-month for Pro+ files older than 30 days | 0.02 EURC | Long-term file retention |
| Dedicated swarm | Monthly fee for enterprise | 500 EURC | Private swarm for one customer |
| Verified operator | One-time KYC badge | 50 EURC | Operator identity attestation (optional) |
| Cross-chain bridge | Transaction fee for bridging GC | 0.5% | Access to other L2s |

All fees contribute to the burn, creating deflationary pressure independent of Pro subscription volume.

### 6.2 Fee governance

Fees are set by DAO vote (post-Phase 4) or Foundation multisig (Phase 0-3). Changes require:

- 7-day deliberation period
- Quorum of 10% of circulating GC
- 2/3 majority approval
- 30-day implementation delay

---

## 7. Token Generation Event (TGE)

### 7.1 Pre-TGE milestones

Before TGE, these must be complete:

- MiCA whitepaper filed with BaFin (20+ business days before)
- Smart contracts audited by at least 2 reputable firms
- Initial DEX liquidity secured (500,000 EURC)
- Bootstrap nodes operational and stable for 30+ days
- Testnet with 50+ operators and 1,000+ active users
- Community airdrop snapshot taken
- Service Node Bonus Program participants identified

### 7.2 TGE sequence

**Day -14: Whitepaper publication**
- MiCA whitepaper published on simplego.dev
- Community review period begins
- Media announcements

**Day -7: Token contract deployment**
- GoCoin ERC-20 deployed to Arbitrum
- Verified on Arbiscan
- CoinGecko / CoinMarketCap pre-listings submitted

**Day 0: TGE execution**
- 30M GC distributed per allocation table
- Uniswap V3 liquidity pool created (5M GC + 500k EURC)
- Initial price: 0.10 EURC per GC
- Trading begins

**Day 1: Community airdrop**
- 10M GC airdropped to eligible SimpleGo community members
- Claim period opens (90 days)

**Day 1-7: Service Node Bonus Program**
- First 200 operators stake 10k GC each (from their bonus allocation)
- Nodes begin registering and joining swarms
- Network transitions from bootstrap nodes to community-operated

**Day 7+: Full mainnet**
- Pro subscriptions go live in EURC
- Burn mechanism activated
- Reward distribution begins (first payout 30 days after TGE)

### 7.3 Migration from testnet

Testnet participants (Phase 2) who earned incentive points receive GC proportionally at TGE:

```
Incentive points distribution:
  Total pool: 3,000,000 GC (from grants allocation)
  Conversion: 1 testnet point = 0.5 GC (approximately)
  Lockup: 6-month linear vest starting at TGE

Top 200 testnet operators:
  Priority access to Service Node Bonus Program
  Pre-registered swarm memberships
  Migration support from Foundation
```

---

## 8. Liquidity strategy

### 8.1 DEX liquidity (primary)

Initial liquidity on Arbitrum DEXes:

| DEX | Pair | Initial Liquidity | Fee Tier |
|:----|:-----|:------------------|:---------|
| Uniswap V3 (primary) | GC/EURC | 5,000,000 GC + 500,000 EURC | 0.3% |
| Uniswap V3 | GC/ETH | 500,000 GC + equivalent ETH | 0.3% |
| Camelot | GC/EURC | 500,000 GC + 50,000 EURC | 0.3% |

Liquidity Mining Rewards (3M GC from initial circulating) distributed to LP providers over 24 months to maintain depth.

### 8.2 Market maker engagement

Foundation will engage a professional market maker from Day 30 post-TGE:

Candidates: Wintermute, Keyrock, GSR (all have worked with Session, Filecoin, and similar networks).

Terms:
- Token loan structure (no direct treasury payment)
- 6-month initial contract, renewable
- Performance-based (spread maintenance, depth targets)
- Inventory returned at contract end

### 8.3 CEX listings

**Phase 1 (Month 1-3 post-TGE):** Small-tier CEX listings

| Exchange | Listing Cost (approx) | Target |
|:---------|:---------------------|:-------|
| MEXC | $25,000 | Week 2 post-TGE |
| Gate.io | $30,000 | Week 4 post-TGE |
| BitMart | $15,000 | Week 6 post-TGE |
| LBank | $10,000 | Month 2 post-TGE |

**Phase 2 (Month 3-12 post-TGE):** Mid-tier CEX listings

| Exchange | Requirements | Target |
|:---------|:-------------|:-------|
| KuCoin | Volume, community, tech review | Month 3 |
| Bitget | Volume, partnerships | Month 4 |
| HTX (Huobi) | Compliance review | Month 6 |
| Kraken | Full due diligence | Month 9 |

**Phase 3 (Year 2+):** Major exchange listings

| Exchange | Typical Requirements |
|:---------|:---------------------|
| Coinbase | 100k+ users, regulatory clarity, token age |
| Binance | High volume, geographic diversity, security audits |
| Bybit | Regional presence, BD relationship |

---

## 9. Governance

### 9.1 Three-phase governance transition

**Phase A: Foundation Control (Year 0-2)**

Foundation multisig (3-of-5) controls all protocol parameters:
- Emission schedule adjustments
- Fee rates
- Slashing parameters
- Grant recipients
- Upgrade deployments

All decisions published with 7-day deliberation before execution. Community can submit proposals for Foundation review.

**Phase B: Hybrid Governance (Year 2-4)**

DAO voting introduced for non-security parameters:
- Fee adjustments
- Grant recipients
- Emission schedule within defined bounds
- Non-critical parameter tuning

Foundation retains veto power on:
- Security issues
- Cryptographic changes
- Smart contract upgrades

Voting power: 1 GC staked in governance contract = 1 vote.

**Phase C: Full DAO (Year 4+)**

Foundation admin keys burned. All parameters controlled by DAO vote:
- Token upgrades (if any, requires 75% supermajority)
- Parameter changes (66% majority)
- Grant releases (50% majority)

Foundation continues operations (hiring developers, marketing, enterprise sales) but has no special protocol privileges.

### 9.2 Voting mechanics

| Parameter | Required Quorum | Required Majority | Deliberation Period |
|:----------|:----------------|:------------------|:--------------------|
| Protocol upgrade (contract replacement) | 20% of circulating | 75% yes | 30 days |
| Critical parameter (slashing, emission) | 15% of circulating | 66% yes | 14 days |
| Normal parameter (fees, rewards) | 10% of circulating | 50%+1 yes | 7 days |
| Grant allocation (<100k GC) | 5% of circulating | 50%+1 yes | 3 days |

### 9.3 Token voting vs operator voting

To prevent whale dominance, certain votes are weighted by operator status:

| Vote Type | Weighting |
|:----------|:----------|
| Protocol upgrades | 1 GC staked = 1 vote |
| Slashing parameters | 1 operator = 1 vote (regardless of stake) |
| Grant allocations | 50% GC-weighted, 50% operator-weighted |
| Fee changes | 1 GC staked = 1 vote |

---

## 10. Regulatory positioning

### 10.1 MiCA classification

GoCoin is a utility token under MiCA Article 3(1)(9) ("other crypto-assets"). Key evidence:

| Criterion | GoCoin Position |
|:----------|:---------------|
| Pegged to fiat? | No |
| Pegged to basket? | No |
| Promise of redemption? | No |
| Profit-sharing with holders? | No |
| Voting rights with financial value? | No (voting is limited to protocol params) |
| Main purpose | Access to network services (operation, governance) |

This places GoCoin in the same category as Filecoin's FIL, Session's SESH, Arweave's AR, and Helium's HNT - all classified as utility tokens in various jurisdictions.

### 10.2 MiCA Title II whitepaper

Before any public offer, Foundation files a Title II whitepaper with BaFin:

| Section | Content |
|:--------|:--------|
| Part A | Issuer information (Swiss Stiftung details) |
| Part B | Project information (GoNode description) |
| Part C | Rights and obligations (token functions) |
| Part D | Technology (smart contracts, consensus) |
| Part E | Risks (market, technical, regulatory) |
| Part F | Token offer details (distribution, timing) |
| Part G | Sustainability (energy, governance) |

Filing deadline: 20 business days before public offer. BaFin does not approve but can require amendments.

### 10.3 Exemptions

MiCA Article 4(2) provides exemptions useful for phased launch:

| Exemption | Limit | GoNode Use |
|:----------|:------|:-----------|
| Small offer (< 150 persons/MS) | Per member state | Phase 1 testnet, Service Node Bonus Program |
| Small offer (< 1M EUR / 12 months) | Aggregate | Phase 2 pre-TGE private round |
| Qualified investors only | Professional investors | Strategic round if needed |
| Fully decentralised | Art. 2(3) | Target state post-Phase 4 |

---

## 11. Risk factors

### 11.1 Token-specific risks

| Risk | Severity | Mitigation |
|:-----|:---------|:-----------|
| Token price falls below breakeven for operators | Medium | Multiple revenue streams ensure network continues; held-back structure protects long-term operators |
| Insufficient burn volume to offset emission | Medium | Conservative burn projections; enterprise SLAs provide additional burn source; emission decays over time |
| Uniswap pool manipulation affects burn efficiency | Low | Multi-pool routing, MEV protection via private mempool, large pool depth reduces impact |
| Regulatory reclassification as security | Low | Design explicitly avoids Howey factors; utility token classification strong |
| Operator concentration (Sybil attack via stake) | Low | Geographic weighting, VRF randomness, economic cost of 33% attack |

### 11.2 Competitive risks

| Risk | Severity | Mitigation |
|:-----|:---------|:-----------|
| Session relaunches under new management | Low | Session code is AGPL; community migration likely toward better-funded successor |
| XMTP wins enterprise privacy messaging | Medium | Different market focus (GoNode: hardware identity + SimpleX, XMTP: Ethereum-native) |
| Centralized competitor (Threema, Signal) acquires market | Medium | Target segments (government, privacy enthusiasts) value decentralisation |
| New L1/L2 launches with better decentralised messaging | Low | Protocol-level switching cost high; Arbitrum deployment is flexible |

### 11.3 Operational risks

| Risk | Severity | Mitigation |
|:-----|:---------|:-----------|
| Smart contract exploit | High severity, low probability | Multiple audits, bug bounty, timelock, multisig emergency pause |
| Foundation key compromise | High severity, low probability | Multisig governance, hardware security modules, key burn at Phase 4 |
| Key team departure | Medium severity, medium probability | 4-year vesting, team documentation, multiple-contributor model |
| Legal action against Foundation | Medium severity, low probability | Swiss jurisdiction, clear utility token design, no custody |

---

## 12. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [GoNode Architecture](ARCHITECTURE_AND_SECURITY.md) | Technical architecture using GoCoin | This repo |
| [GoNode Business Model](BUSINESS_MODEL.md) | Revenue streams supporting burn mechanism | This repo |
| [GoNode Legal Compliance](LEGAL_COMPLIANCE.md) | MiCA and regulatory analysis | This repo |
| [GoNode Smart Contracts](SMART_CONTRACTS.md) | Solidity implementation details | This repo |
| [SimpleGo ecosystem](https://github.com/saschadaemgen/SimpleGo) | Products using GoNode infrastructure | SimpleGo repo |

---

*GoNode Tokenomics v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
