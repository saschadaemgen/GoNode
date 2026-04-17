<p align="center">
  <strong>GoNode</strong>
</p>

<p align="center">
  <strong>The decentralised infrastructure layer for the SimpleGo ecosystem.</strong><br>
  Anyone can run a node. Anyone can earn. Users pay stable euros, operators earn tokens.<br>
  Decentralisation without speculation.
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-AGPL--3.0-blue.svg" alt="License"></a>
  <a href="#status"><img src="https://img.shields.io/badge/status-concept-yellow.svg" alt="Status"></a>
  <a href="https://github.com/saschadaemgen/SimpleGo"><img src="https://img.shields.io/badge/ecosystem-SimpleGo-green.svg" alt="SimpleGo"></a>
  <a href="#tokenomics"><img src="https://img.shields.io/badge/token-GoCoin-orange.svg" alt="GoCoin"></a>
  <a href="#legal-structure"><img src="https://img.shields.io/badge/compliance-MiCA%20%7C%20GDPR%20%7C%20DSA-purple.svg" alt="Compliance"></a>
</p>

---

> "Every decentralised messenger with a token has failed financially. Session launched with 25,000 token stakes, 2,000 service nodes, 1.7 million users - and announced shutdown in April 2026 because token rewards pay operators, not developers. GoNode inverts this: users pay stable euros for the service, operators earn tokens for running infrastructure, and the foundation survives on real revenue plus grants. The token serves the business, not the other way around."

GoNode is the economic and infrastructure backbone of the SimpleGo ecosystem. It transforms the SimpleX-based messaging network from a federation of a few volunteer-run relay servers into a globally distributed, economically self-sustaining, Sybil-resistant network of independent operators.

Anyone can download GoNode, stake 10,000 GoCoin as collateral, run the node software on a home computer or server, and earn GoCoin rewards for providing storage and bandwidth to the network. Users never touch GoCoin - they subscribe to GoNode Pro for 5 EURC per month (stable, 1:1 to euro), and smart contracts automatically buy and burn GoCoin to fund operations. This architecture ties token value to real usage instead of speculation, insulates users from volatility, and keeps the foundation focused on shipping real products instead of managing token price.

GoNode inherits the full SimpleGo cryptographic stack (five-layer encryption, post-quantum KEM, Double Ratchet) and integrates hardware identity from [GoKey](https://github.com/saschadaemgen/SimpleGo) for the strongest operator authenticity model in the decentralised infrastructure space.

---

## The problem

Three unsolved problems motivate GoNode:

**Metadata is still leaking.** Signal and WhatsApp encrypt content but not metadata. SimpleX Chat is the first protocol designed without user identifiers, but it still runs on a handful of centrally-operated relays. The "your IP will be visible to this server" warning on every file download is the symptom.

**The infrastructure is still centralised.** SimpleX depends on SimpleX Chat Ltd. and a few community operators. No economic incentive exists for third parties to run relays, so nobody does. If SimpleX Chat Ltd. shuts down or is compromised, the default relay list collapses.

**No token-funded decentralised messenger has survived.** Session (shutdown announced 8 July 2026), Status.im (declining), Secret Network (pivoted away from messaging), Nym (stable but under 5% staking participation) - every token-funded project has failed to generate revenue independent of token speculation. When the bear market hits, development funding dries up.

GoNode solves these three problems by combining SimpleX's superior protocol with Session's proven service-node architecture, Storj's production-tested erasure-coded storage, and Helium's burn-and-mint tokenomics - operated through a Swiss Stiftung with revenue-first economics and German engineering.

---

## How it works

```
                    [User (Max) in Berlin]
                            |
                    5 EURC/month (stable)
                            |
                            v
                    [GoNode Subscription Contract on Arbitrum One]
                            |
                    +-------+-------+
                    |               |
              Buy GoCoin        Activate Pro
              on Uniswap        for Max
                    |
                    v
              Burn the GoCoin
              (supply shrinks, value rises)


     [Service Node Layer - swarms of 5 to 10 operators]
     +------------------------------------------------+
     |                                                |
     |   Swarm A          Swarm B          Swarm N    |
     |   16 KB blocks     16 KB blocks     16 KB b.   |
     |   replicated 3-5x  replicated 3-5x  replicat.  |
     |                                                |
     |   XFTP files: Reed-Solomon RS(10, 16)          |
     |   Onion routing: 3 hops, nobody sees both ends |
     |   Audit challenges: HMAC every hour            |
     |                                                |
     +------------------------------------------------+
                            |
                            |
                    [Protocol Layer]
     +------------------------------------------------+
     |   Unchanged SimpleX: SMP, XFTP, 16 KB blocks   |
     |   Double Ratchet with post-quantum KEM hybrid  |
     |   Five-layer encryption inherited from SimpleGo|
     +------------------------------------------------+
```

**What the user sees:** a flat 5 EUR/month subscription. Reliable service. No token, no wallet anxiety, no price volatility. Exactly like Netflix or Spotify, except the infrastructure is decentralised.

**What the operator sees:** a 10,000 GoCoin stake deposit, a Go binary running on commodity hardware, and monthly GoCoin rewards that increase in value as the user base grows (because Pro subscriptions burn GoCoin from circulation).

**What the foundation sees:** predictable EUR revenue from Pro subscriptions, enterprise SLAs, AI developer support services, and grants - independent of token price. The token is an internal accounting and incentive instrument, not a funding mechanism.

---

## Why GoNode will succeed where others failed

| Dimension | Previous projects | GoNode |
|:----------|:-----------------|:-------|
| User pricing | Token-denominated, volatile | EURC-denominated, stable 5 EUR/month |
| Revenue before token | None or speculative | Pro subs + enterprise + grants from day one |
| Legal structure | Ambiguous, pre-MiCA | Swiss Stiftung + German GmbH, MiCA-compliant |
| Hardware identity | None | GoKey integration for operator authenticity |
| Protocol foundation | Custom, unproven | SimpleX, production-tested |
| Tokenomics | Inflationary or speculative | Burn-and-mint, value from real usage |
| Survival during bear market | Token-dependent, fragile | EUR revenue + grants carry the project |

**Session's April 2026 shutdown** creates a unique historical moment: proven architectural patterns become freely available (AGPL/GPL), ~2,000 experienced node operators become unhomed and open to alternatives, and a clear gap opens in the decentralised-messenger-with-token market. GoNode is positioned to capture this moment while building on a superior foundation.

See [CONCEPT.md](docs/CONCEPT.md) for the full technical and business rationale.

---

## Four components, one system

GoNode integrates with the existing SimpleGo ecosystem. It is the last missing piece of an architecture that has been carefully built over several years.

| Component | What it does | Where it runs | Repository |
|:----------|:-------------|:-------------|:-----------|
| **GoNode** | Decentralised relay and storage network with economic incentives | Anyone's computer | This repo |
| [SimpleGo](https://github.com/saschadaemgen/SimpleGo) | Native C SMP implementation on ESP32-S3 hardware | T-Deck Plus | [SimpleGo repo](https://github.com/saschadaemgen/SimpleGo) |
| [GoBot](https://github.com/saschadaemgen/GoBot) | Hardware-secured moderation bot for groups | VPS (Go service) | [GoBot repo](https://github.com/saschadaemgen/GoBot) |
| [GoKey](https://github.com/saschadaemgen/SimpleGo) | Hardware crypto engine and identity anchor | ESP32-S3 at home | [SimpleGo template](https://github.com/saschadaemgen/SimpleGo) |
| [GoUNITY](https://github.com/saschadaemgen/GoUNITY) | Ed25519 certificate authority for identity | VPS (Go service) | [GoUNITY repo](https://github.com/saschadaemgen/GoUNITY) |
| [GoLab](https://github.com/saschadaemgen/GoLab) | Developer community platform | Uses GoBot as relay | [GoLab repo](https://github.com/saschadaemgen/GoLab) |
| [GoRelay](https://github.com/saschadaemgen/GoRelay) | Encrypted relay server (SMP + GRP) | Any VPS | [GoRelay repo](https://github.com/saschadaemgen/GoRelay) |
| [GoChat](https://github.com/saschadaemgen/GoChat) | Browser-native encrypted chat widget | Any website | [GoChat repo](https://github.com/saschadaemgen/GoChat) |

---

## Technical architecture

GoNode consists of four layers, each with a distinct role:

| Layer | Component | Role |
|:------|:----------|:-----|
| **4** | Economic Layer | Arbitrum One smart contracts for staking, rewards, Pro subscriptions, GoCoin burn |
| **3** | Consensus Layer | BFT appchain for swarm assignment, VRF epochs, fast slashing quorums |
| **2** | Service Node Layer | Swarms of 5 to 10 nodes, replication for messages, Reed-Solomon for files |
| **1** | Protocol Layer | Unchanged SimpleX: SMP, XFTP, 16 KB padded blocks, Double Ratchet, PQ KEM |

**Swarm model (borrowed from Session, adapted for SimpleX's stateless queues).** The network partitions queue identifier space into subsets. Each subset is assigned to a swarm of 5 to 10 service nodes via a Verifiable Random Function recomputed every epoch. When a user creates a queue, the identifier deterministically maps to a specific swarm, and messages are replicated across swarm members. Up to 4 swarm members can go offline without message loss.

**File storage with Reed-Solomon RS(10, 16).** XFTP file chunks are split into 10 data shards and 6 parity shards. Any 10 of 16 shards reconstruct the original. Durability: eleven nines (99.999999999%). Storage overhead: 1.6x, compared to 3x for simple replication.

**Audit-based storage proofs (not Filecoin PoRep/PoSt).** Each node receives approximately 10 audit challenges per hour. Challenge: `HMAC-SHA256(node-key, block-id)` for a random stored block. Fast, correct response means continued good standing. Incorrect or missing responses lead to reduced rewards, then deregistration, then disqualification with full held-back burn.

**Onion routing for all messages.** 3-hop onion encryption. First hop sees sender IP but not recipient. Last hop sees recipient but not sender. No single node sees both ends of a conversation. This eliminates the "IP address visible" warning that plagues current SimpleX file downloads.

See [ARCHITECTURE_AND_SECURITY.md](docs/ARCHITECTURE_AND_SECURITY.md) for the full technical architecture and threat model.

---

## Tokenomics

**GoCoin (GC)** is an ERC-20 utility token on Arbitrum One with a fixed maximum supply of 100,000,000.

| Parameter | Value |
|:----------|:------|
| Max supply | 100,000,000 GoCoin |
| Initial circulating (TGE) | 30,000,000 GoCoin |
| Node reward pool | 40,000,000 GoCoin (emitted over 10 years) |
| Foundation treasury | 15,000,000 GoCoin (4-year vest, 1-year cliff) |
| Team and advisors | 10,000,000 GoCoin (4-year vest, 1-year cliff) |
| Ecosystem grants | 5,000,000 GoCoin (DAO-released) |
| Node stake requirement | 10,000 GoCoin per node |
| Initial DEX price target | 0.10 EURC per GoCoin |

**The burn-and-mint equilibrium.** Every GoNode Pro subscription pays 5 EURC to the subscription smart contract. The contract buys GoCoin on Uniswap with the 5 EURC and burns all of it. Node operators separately receive monthly GoCoin emissions from the reward pool. Token value is tied to real service demand: more subscriptions means more burn means scarcer token means more valuable operator rewards.

**Emission schedule.** The 40M reward pool emits on a modified Bitcoin halving curve: ~12% of pool per year in years 1-2, decaying to ~4% per year in years 9-10. Target equilibrium year: approximately year 5, after which annual burn exceeds annual emission and GoCoin becomes net deflationary.

**Operator rewards and held-back.** Following Storj's production-proven model: 50% paid / 50% held in months 1-3, 75% / 25% in months 4-6, 100% / 0% from month 7, with held-back amounts released at month 10. Disqualification for misbehaviour results in 100% held-back burn.

See [TOKENOMICS.md](docs/TOKENOMICS.md) for the full token economic design.

---

## Legal structure

GoNode is structured for compliance with MiCA (EU Markets in Crypto-Assets Regulation), GDPR, the EU Digital Services Act, and relevant German law from day one.

| Entity | Role | Jurisdiction |
|:-------|:-----|:-------------|
| **GoNode Foundation** | Protocol operation, token issuance, grant management | Swiss Stiftung in Zug |
| **IT and More Systems GmbH** | Publishing, development, BaFin compliance | German GmbH in Recklinghausen |

**Why this structure:**
- Protects individual developers from protocol-level liability (Tornado Cash lessons)
- Provides funding diversification (Swiss brand sells to enterprise, German GmbH for regional contracts)
- Aligns with proven templates (Ethereum Foundation, Session Technology Foundation, Nym Technologies)
- Foundation never holds user funds (no custody, no CASP authorisation needed)
- Foundation never operates fiat on/off-ramp (exchanges handle fiat conversion)

**MiCA classification.** GoCoin qualifies as a utility token under Art. 3(1)(9) of Regulation (EU) 2023/1114 ("other crypto-assets"). Title II whitepaper required, notified to BaFin 20 business days before public offer. Art. 59 CASP authorisation is not triggered because the Foundation does not provide exchange, custody, or trading services.

**GDPR approach.** Personal data stays off-chain. Messages are client-side encrypted with random keys (zero-knowledge architecture). Node operators sign an Art. 26 joint controllership agreement with the Foundation as single point of contact. EDPB Guidelines 02/2025 compliance throughout.

**DSA safe harbour.** Relay nodes qualify as mere conduits under Art. 4 DSA. Storage nodes qualify as hosting under Art. 6 DSA but safe harbour is preserved because operators cannot have "actual knowledge" of illegal content when they cannot decrypt. Art. 16 notice-and-action implemented via Foundation's single point of contact (Art. 11 DSA).

See [LEGAL_COMPLIANCE.md](docs/LEGAL_COMPLIANCE.md) for the full regulatory analysis.

---

## Business model

Four independent revenue streams ensure no single dependency:

| Stream | Target Customer | Pricing | Status |
|:-------|:----------------|:--------|:-------|
| **GoNode Pro** | Privacy-conscious individuals | 5 EURC/month | Launch in Phase 2 |
| **Enterprise SLA** | Government, NGO, healthcare, finance | 500 - 5,000 EUR/month | Pilot customers in Phase 1 |
| **AI Developer Support** | Developers integrating the ecosystem | 20 - 50 EUR/seat/month | Launch in Phase 1 |
| **Non-dilutive Grants** | Arbitrum, Ethereum, NLnet, EU Digital Europe | 50k - 2M per grant | Active in Phase 0 |

**Financial targets:**

| Year | Revenue | Costs | Net (EUR) |
|:-----|:--------|:------|:----------|
| Year 1 | 460,000 | 690,000 | -230,000 |
| Year 2 | 990,000 | 1,200,000 | -210,000 |
| Year 3 | 1,900,000 | 2,000,000 | -100,000 |
| Year 4 | 4,640,000 | 2,700,000 | **+1,940,000** |
| Year 5 | 11,000,000 | 3,390,000 | **+7,610,000** |

**Initial funding requirement:** 1,600,000 EUR to cover years 1-3 operating deficit, legal setup, security audits, initial DEX liquidity and runway buffer. Target sources: Arbitrum Foundation grant (500k - 1M USD), Ethereum Foundation ESP (150k USD), NLnet NGI Zero (2 x 50k EUR), EU Digital Europe Programme (300k - 800k EUR).

See [BUSINESS_MODEL.md](docs/BUSINESS_MODEL.md) for the full business plan and financial projections.

---

## Build and run

**Note:** GoNode is currently in concept phase. Source code will be published in Phase 1 (months 3-9).

**Planned requirements:** Go 1.24+, 4 CPU cores, 8 GB RAM, 500 GB SSD, 100 Mbps symmetric internet.

```bash
# Clone (planned, not yet available)
git clone https://github.com/saschadaemgen/GoNode.git
cd GoNode

# Build
make build

# Configure
cp config.example.yaml config.yaml
# Edit config.yaml with your Arbitrum wallet, swarm preferences, storage paths

# Run
make run

# Stake your 10,000 GoCoin (Phase 3+, after TGE)
gonode stake --amount 10000 --operator-address 0x...

# Check earnings
gonode earnings
```

**Configuration** via environment variables or config file:

| Variable | Default | Description |
|:---------|:--------|:------------|
| GONODE_LOG_LEVEL | info | Log verbosity: debug, info, warn, error |
| GONODE_DATA_DIR | ~/.gonode | Directory for storage and state |
| GONODE_STORAGE_QUOTA | 500GB | Maximum storage to provide |
| GONODE_BANDWIDTH_LIMIT | unlimited | Maximum monthly bandwidth |
| GONODE_RPC_ARBITRUM | (public) | Custom Arbitrum RPC endpoint |
| GONODE_WALLET_KEYSTORE | ~/.gonode/keystore | Operator wallet location |

---

## Current status

| Component | Status |
|:----------|:-------|
| GoNode concept and architecture | Season 1 - complete |
| MiCA whitepaper draft | Season 1 - in progress |
| Foundation setup (Swiss Stiftung) | Season 1 - planned |
| Grant applications (Arbitrum, EF, NLnet, EU) | Season 1 - planned |
| Service node runtime (Go) | Season 2 - planned |
| Swarm protocol implementation | Season 2 - planned |
| Reed-Solomon file sharding | Season 2 - planned |
| Arbitrum smart contracts | Season 3 - planned |
| Permissioned testnet | Season 3 - planned |
| Public testnet with incentive points | Season 4 - planned |
| Token Generation Event (TGE) | Season 5 - planned |
| Mainnet with full network | Season 5 - planned |
| DAO governance transition | Season 6+ - planned |

### Dependencies

| Dependency | Status |
|:-----------|:-------|
| SimpleGo SMP stack (47 files, 21,863 LOC) | Complete |
| GoBot Go service (Wire Protocol counterpart) | In development (Season 2) |
| GoKey hardware identity (device certificates) | Planned (Season 3) |
| GoUNITY certificate authority | Planned (Season 4) |
| Arbitrum One (deployment target) | Production |
| Circle EURC (user payment currency) | Production |
| libsodium (ChaCha20, Ed25519) | Available |
| Reed-Solomon erasure library (Go) | Available |

---

## Roadmap

| Phase | Focus | Timeline |
|:------|:------|:---------|
| Phase 0 | Legal skeleton, Foundation setup, grant applications, team building | Months 0-3 |
| Phase 1 | Permissioned testnet, 20-50 operators, first enterprise pilots, AI service launch | Months 3-9 |
| Phase 2 | Public testnet with incentive points, MiCA whitepaper filed with BaFin | Months 9-15 |
| Phase 3 | Token Generation Event on Arbitrum, community airdrop, Pro subscription in EURC | Months 15-24 |
| Phase 4 | DAO governance, deployer key burn, integration expansion to GoShop/GoTube/GoBook | Months 24+ |

See [ROADMAP.md](docs/ROADMAP.md) for detailed phase planning and [Season Index](docs/seasons/SEASON-INDEX.md) for season-by-season execution documentation.

---

## Documentation

| Document | Description |
|:---------|:-----------|
| [Concept](docs/CONCEPT.md) | High-level technical and business concept, design decisions |
| [Architecture and Security](docs/ARCHITECTURE_AND_SECURITY.md) | Full technical architecture, threat model, cryptographic design |
| [Tokenomics](docs/TOKENOMICS.md) | GoCoin supply, distribution, emission schedule, burn mechanism |
| [Business Model](docs/BUSINESS_MODEL.md) | Revenue streams, financial projections, pricing strategy |
| [Legal Compliance](docs/LEGAL_COMPLIANCE.md) | MiCA, GDPR, DSA, German law analysis |
| [Roadmap](docs/ROADMAP.md) | Phase planning, milestones, deliverables |
| [Wire Protocol](docs/WIRE_PROTOCOL.md) | Node-to-node and client-to-node communication protocol |
| [Smart Contracts](docs/SMART_CONTRACTS.md) | Arbitrum contract specifications and interfaces |
| [Season Index](docs/seasons/SEASON-INDEX.md) | Links to all season documentation |

### Related documentation in other repos

| Document | Description |
|:---------|:-----------|
| [GoBot Architecture](https://github.com/saschadaemgen/GoBot/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) | Moderation bot using GoNode for relay capacity |
| [GoKey Architecture](https://github.com/saschadaemgen/SimpleGo/blob/main/templates/gokey/docs/ARCHITECTURE_AND_SECURITY.md) | Hardware identity anchor for GoNode operators |
| [GoUNITY Architecture](https://github.com/saschadaemgen/GoUNITY/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) | Certificate authority for identity verification |
| [GoLab Architecture](https://github.com/saschadaemgen/GoLab/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) | Community platform using GoNode for fan-out |

---

## SimpleGo ecosystem

| Project | What it does |
|:--------|:-------------|
| [SimpleGo](https://github.com/saschadaemgen/SimpleGo) | Dedicated hardware messenger on ESP32-S3 |
| [GoRelay](https://github.com/saschadaemgen/GoRelay) | Encrypted relay server (SMP + GRP) |
| [GoChat](https://github.com/saschadaemgen/GoChat) | Browser-native encrypted chat widget |
| [GoBot](https://github.com/saschadaemgen/GoBot) | Hardware-secured moderation bot |
| [GoKey](https://github.com/saschadaemgen/SimpleGo) | Hardware crypto engine for GoBot (ESP32-S3) |
| [GoUNITY](https://github.com/saschadaemgen/GoUNITY) | Certificate authority for identity verification |
| [GoLab](https://github.com/saschadaemgen/GoLab) | Privacy-first developer community platform |
| **GoNode** | **Decentralised infrastructure with token incentives** |
| [GoShop](https://github.com/saschadaemgen/GoShop) | End-to-end encrypted e-commerce |
| [GoTube](https://github.com/saschadaemgen/GoTube) | Encrypted video platform |
| [GoBook](https://github.com/saschadaemgen/GoBook) | Encrypted publishing platform |
| [GoOS](https://github.com/saschadaemgen/GoOS) | Privacy-focused Linux (Buildroot, RK3566) |

---

## Contributing

GoNode is AGPL-3.0 open source. Contributions welcome once the codebase is public in Phase 1.

See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for community standards.

Security issues should be reported privately via [SECURITY.md](SECURITY.md).

---

## License

AGPL-3.0

---

<p align="center">
  <i>GoNode is part of the <a href="https://github.com/saschadaemgen/SimpleGo">SimpleGo ecosystem</a> by IT and More Systems, Recklinghausen, Germany.</i>
</p>

<p align="center">
  <strong>Anyone can run a node. Anyone can earn. Users pay stable euros, operators earn tokens. Decentralisation without speculation.</strong>
</p>
