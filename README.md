# GoNode

**Decentralised infrastructure and loyalty layer for the SimpleGo messaging ecosystem**

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Status: Concept](https://img.shields.io/badge/Status-Concept_Phase-orange.svg)]()
[![Docs: Complete](https://img.shields.io/badge/Docs-Complete-green.svg)]()

---

## What GoNode is

GoNode is the decentralised infrastructure layer that ties the SimpleGo ecosystem together. It runs the servers, stores the files, routes the messages, and rewards the people who make it all possible - without relying on cryptocurrency markets, volatile tokens, or opaque financial engineering.

**The core model in one sentence:** Users pay stable euros for premium features, node operators earn loyalty points for running infrastructure, and those loyalty points can be redeemed for ecosystem goods or traded with other users on an internal marketplace - never for money.

This is not a crypto project. It is a privacy infrastructure project that uses a closed-loop loyalty system (similar to Payback, Steam Wallet, or Miles & More) to reward participation in its operation.

---

## Why this design

Every token-funded decentralised messenger before us has failed. Session announced shutdown in April 2026 despite 1.7M users, because token rewards pay operators but developers still need real money. We inverted this from day one: real EUR revenue from Pro subscriptions, enterprise SLAs, AI services and grants funds the Foundation. The loyalty point system rewards operators for running nodes, but does not fund development.

This approach eliminates the problems that killed Session:
- No pressure on users to hold volatile assets
- No dependency on token markets that can crash
- No regulatory ambiguity about crypto classification
- No 500k EUR needed for DEX liquidity on day one

And it keeps the architectural strengths:
- Sybil-resistant operator network
- Incentivised distributed infrastructure
- Privacy-preserving message routing
- Post-quantum ready cryptography

---

## Architecture summary

GoNode builds on SimpleX's proven SMP protocol and adds:

- **Swarm-based operator network** adapted from Session (5-10 nodes per swarm, VRF-based rotation every 24 hours)
- **3-hop Sphinx onion routing** providing traffic analysis resistance
- **Reed-Solomon RS(10, 16) erasure coding** for file storage (11-nines durability at 1.6x overhead)
- **Six-layer encryption** inheriting SimpleX's five layers plus adding onion hop encryption
- **Post-quantum ready** via ML-KEM-768 hybrid with X25519
- **Hardware-anchored identity** via GoKey (ESP32-S3, eFuse-bound keys) for premium operators
- **Loyalty ledger** on PostgreSQL (Phase 1) or optional permissioned blockchain (Phase 3+)

All details in [ARCHITECTURE_AND_SECURITY.md](docs/ARCHITECTURE_AND_SECURITY.md).

---

## Loyalty system summary

GoCoin is a closed-loop loyalty point, not a cryptocurrency:

- **100 million soft cap**, policy-enforced at application level
- **Users earn coins** as bonuses when purchasing services, hardware, or premium features with real EUR
- **Operators earn coins** monthly based on uptime, data served, and audit correctness
- **Coins are redeemable** only for ecosystem goods: special edition firmware, premium features, exclusive content, hardware discounts
- **Peer-to-peer marketplace** allows users to trade coins for other ecosystem items (never for money)
- **Foundation is never counterparty** - only marketplace operator with a small fee
- **Node operators** have a 30-day holding period before coins can be traded
- **No DEX, no CEX listings, no public trading markets**

Legal basis: PSD2 Art. 3(k) and German ZAG § 2 Abs. 1 Nr. 10 - the same limited-network exemption under which Payback, Lufthansa Miles & More, Deutsche Bahn BahnBonus, and Steam Wallet operate.

All details in [TOKENOMICS.md](docs/TOKENOMICS.md).

---

## Business model summary

Four revenue streams fund the Foundation:

| Stream | Role |
|:-------|:-----|
| Pro subscriptions | 5 EUR/month from individuals for premium features |
| Enterprise SLAs | 500-10,000+ EUR/month from organisations |
| AI Developer Support | Consulting and custom development services |
| Grants | EU, NLnet, BMBF, Sovereign Tech Fund, etc. |

**Financial targets:**

- Initial funding: 555,000 EUR (vs 1.59M in old crypto-token design)
- Break-even: Year 3
- Year 5 revenue: 11.1 million EUR
- Year 5 margin: 68%

All details in [BUSINESS_MODEL.md](docs/BUSINESS_MODEL.md).

---

## Documentation

Complete documentation suite, ~5,200 lines of Markdown:

| Document | Purpose |
|:---------|:--------|
| [README.md](README.md) | You are here - project overview |
| [CONCEPT.md](docs/CONCEPT.md) | Strategic rationale, why we will succeed |
| [ARCHITECTURE_AND_SECURITY.md](docs/ARCHITECTURE_AND_SECURITY.md) | Full technical architecture and threat model |
| [TOKENOMICS.md](docs/TOKENOMICS.md) | Loyalty system economics and mechanics |
| [BUSINESS_MODEL.md](docs/BUSINESS_MODEL.md) | Revenue, costs, 5-year projection |
| [LEGAL_COMPLIANCE.md](docs/LEGAL_COMPLIANCE.md) | MiCA, GDPR, DSA, tax analysis |
| [WIRE_PROTOCOL.md](docs/WIRE_PROTOCOL.md) | Node-to-node and client protocol specification |
| [SMART_CONTRACTS.md](docs/SMART_CONTRACTS.md) | Loyalty ledger architecture (database-based) |
| [ROADMAP.md](docs/ROADMAP.md) | 5-phase execution plan |
| [DISTRIBUTED_CONTENT_DEFENSE.md](docs/DISTRIBUTED_CONTENT_DEFENSE.md) | Content integrity protocols |
| [SECURITY.md](SECURITY.md) | Responsible disclosure policy |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to contribute |
| [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) | Community standards |

---

## Ecosystem integration

GoNode is the infrastructure backbone for the full SimpleGo ecosystem:

- **SimpleGo** (native C SMP implementation on ESP32-S3 hardware) uses GoNode as its relay infrastructure
- **SimpleGoX** (the Rust-based rebuild) extends SimpleGo with ecosystem integration
- **GoBot** (moderation and automation) runs on GoNode swarms
- **GoKey** (hardware identity) provides operator authenticity anchors
- **GoUNITY** (Ed25519 certificate authority) delivers user identity certificates
- **GoLab** (community platform, Twitter/Git hybrid) uses GoNode for distribution
- **GoMarket** (ecosystem marketplace) runs as a service on top of GoNode
- **Future:** GoShop, GoTube, GoBook, GoOS all build on this foundation

---

## Current status

**Concept phase.** No code yet, no token, no fundraising, no operational network.

What exists:
- Complete documentation (this repository)
- Technical design validated against precedent (Session, SimpleX, Payback, Steam)
- Legal framework analysed for Germany and EU
- Team of operator-experienced engineers ready to build

What comes next:
- Phase 0 (Months 0-3): Foundation, legal opinion, grant applications
- Phase 1 (Months 3-9): Core infrastructure, internal alpha
- Phase 2 (Months 9-15): Operator rewards, public testnet
- Phase 3 (Months 15-21): Marketplace launch, full platform
- Phase 4 (Months 21+): Scale and ecosystem expansion

Detailed timeline in [ROADMAP.md](docs/ROADMAP.md).

---

## Key differentiators

What makes GoNode different from Session, Status.im, and other token-funded decentralised messengers:

**Architectural:**
- Built on SimpleX (the strongest metadata-resistant protocol available)
- Hardware identity option via GoKey (no competitor has this at this price point)
- Post-quantum ready from day one
- Six-layer encryption (five from SimpleX + one hop encryption)

**Economic:**
- Revenue funds development (not token sales)
- Loyalty rewards for operators (not volatile token rewards)
- Stable EUR pricing for users (not fluctuating crypto)
- No 500k liquidity requirement on launch
- No CEX listing costs

**Legal:**
- Single legal entity (IT and More Systems GmbH, Recklinghausen, Germany)
- Established loyalty program legal framework (like Payback, Miles & More)
- GDPR-native architecture
- No CASP authorisation required
- Full EU compliance from day one

**Operational:**
- Pattern: decentralised technology, centralised accountability where required
- Transparent operation (monthly public reports planned)
- Clear Terms of Service under German law
- Predictable, boring bookkeeping (not blockchain consensus)

---

## License and copyright

**License:** AGPL-3.0

GoNode source code, when it exists, will be licensed under AGPL-3.0. This is a strong copyleft license requiring that derivative works and network services using the software be made available under the same license.

**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen, Germany

Trademarks (GoNode, GoCoin, SimpleGo, SimpleGoX) are held by IT and More Systems GmbH.

---

## Community and contact

- **Repository:** https://github.com/saschadaemgen/GoNode
- **Issues:** GitHub Issues for bug reports and feature requests
- **Discussions:** GitHub Discussions for broader questions
- **Security:** security@gonode.dev (coming soon) or GitHub private advisories
- **Business inquiries:** IT and More Systems GmbH, Recklinghausen

A dedicated community space for GoNode-specific discussions is being set up separately from the main SimpleGo channels.

---

## Get involved

**If you want to help build:**
- Review the documentation and open issues for gaps or errors
- Contribute code once Phase 1 development begins
- Join the development community

**If you want to operate a node (in future):**
- Read operator requirements in [ARCHITECTURE_AND_SECURITY.md](docs/ARCHITECTURE_AND_SECURITY.md)
- Consider hardware procurement (ESP32-S3 based or standard servers)
- Register interest through the repository

**If you are an enterprise customer:**
- Contact us through IT and More Systems for Enterprise SLA options
- AI Developer Support services available from Phase 1

**If you are a researcher:**
- Security research welcome per [SECURITY.md](SECURITY.md)
- Academic collaboration on privacy and decentralisation research
- Grant reviewers: documentation structured for your evaluation

**If you are a grant reviewer:**
- Business model, roadmap, and technical documentation structured for your needs
- Specific grant applications planned for EU Digital Europe, NLnet, BMBF, Sovereign Tech Fund
- Contact for detailed discussions

---

## Acknowledgements

GoNode learns from and builds on:

- **SimpleX Chat** - for the SMP protocol and metadata-resistant design principles
- **Session** - for the swarm architecture (AGPL code available) and for demonstrating what fails in token-funded messenger projects
- **Signal** - for the Double Ratchet and general security engineering excellence
- **Payback, Lufthansa Miles & More, Steam** - for demonstrating that loyalty programs can operate at scale within EU legal frameworks
- **EVE Online** - for showing that closed-loop economies with peer-to-peer markets can work for 20+ years
- **Open source community** - for all the foundational libraries and tools

---

*Build the values first. Worry about tokenisation later. Or never. If we never need it, that's a success, not a failure.*

---

**GoNode v2 - April 2026 (redesigned as loyalty system)**
*IT and More Systems, Recklinghausen, Germany*
