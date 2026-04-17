# GoNode - Technical Concept
# Decentralised Infrastructure Layer for the SimpleGo Ecosystem

**Project:** GoNode (part of SimpleGo ecosystem)
**Author:** Sascha Daemgen / IT and More Systems
**Date:** April 17, 2026
**Status:** Season 1 - Concept

---

## 1. Overview

GoNode is a decentralised network of independent nodes that provide
the relay and file storage infrastructure for the SimpleGo messaging
ecosystem. Anyone with a computer can run a GoNode instance, stake
10,000 GoCoin as collateral, and earn GoCoin rewards for providing
storage and bandwidth. Users subscribe to GoNode Pro for 5 EURC per
month (stable, 1:1 to euro) and never touch the token directly.

GoNode transforms the SimpleX-based ecosystem from a federation of a
few centrally-operated relay servers into a globally distributed,
Sybil-resistant, economically self-sustaining network. It is built
on proven architectural patterns from Session (swarms, onion routing,
service node staking), Storj (Reed-Solomon erasure coding, audit-based
proofs, held-back payments), and Helium (burn-and-mint tokenomics),
adapted for the SimpleX protocol and the SimpleGo ecosystem.

GoNode is the last missing piece of an ecosystem that has been built
piece by piece over several years: the hardware layer (SimpleGo on
ESP32-S3), the moderation layer (GoBot), the identity layer (GoKey
and GoUNITY), the community layer (GoLab), and now the infrastructure
and economic layer (GoNode).

---

## 2. The problem GoNode solves

### 2.1 The metadata problem

Signal and WhatsApp encrypt message content but not metadata. The
servers know who talked to whom, when, from which IP address, and for
how long. This metadata has been used to identify journalists,
activists, whistleblowers and ordinary citizens in every jurisdiction
where privacy matters.

SimpleX Chat, launched in 2021, is the first protocol designed from
the ground up without user identifiers. There are no accounts, no
phone numbers, no usernames. Pairwise encrypted queues handle every
conversation, and servers cannot correlate them. SimpleX is the
strongest metadata-resistant messenger available today and the
foundation of the SimpleGo ecosystem.

But SimpleX has a centralisation problem that GoNode fixes.

### 2.2 The centralisation problem

SimpleX currently runs on a handful of relay servers operated by
SimpleX Chat Ltd., Flux, and a small number of community operators.
Users can run their own relays but few do, because there is no
economic incentive. The result is a protocol with the architecture
of a decentralised network but the infrastructure of a centralised
service.

This creates real operational problems:

- Every file download triggers a warning that the server will see
  the user's IP address
- The network depends on the continued operation of SimpleX Chat Ltd.
- No redundancy - a relay going offline means message loss
- Illegal content in user avatars lands on recipient endpoints without
  any moderation layer, because there is no directory and no reputation

### 2.3 The funding problem

Every major token-funded decentralised messenger has failed to achieve
operational sustainability. Session announced shutdown on 9 April 2026
despite 1.7 million monthly active users, 2,000 service nodes, and
five years of operation. Status.im is declining. Secret Network
pivoted away from messaging. Nym has less than 5 percent staking
participation.

The pattern is consistent: projects that fund themselves entirely on
token speculation die when the bear market hits. Token rewards pay
operators, but they do not pay client developers, legal counsel,
infrastructure costs, or grant writers. Without an independent
revenue stream, the foundation runs out of money regardless of how
many users it has.

GoNode solves these three problems by combining SimpleX's superior
protocol with Session's service-node architecture, Storj's storage
design, Helium's burn-and-mint economics, and a revenue-first business
model operated through a Swiss Stiftung.

---

## 3. The split-layer approach

### 3.1 The core insight

Every previous decentralised messenger asked users to hold a token,
experience its volatility, and care about its price. Most users do
not want to do this. GoNode inverts this model:

```
Users:     pay stable euros        (EURC, 1:1 to EUR)
Operators: earn volatile tokens    (GoCoin)
Smart contract: converts between the two automatically
```

This is the same pattern that made Helium successful after its 2025
consolidation to USD-priced Data Credits. Users get predictable pricing,
operators get upside exposure to network growth, and the foundation
never touches either side directly.

### 3.2 How the money flows

```
Max (user in Berlin)
  |
  | 5 EURC per month (stable, from his wallet)
  v
Subscription smart contract (on Arbitrum One)
  |
  +-- buys GoCoin on Uniswap with the 5 EURC
  |   (quantity depends on current market price)
  |
  +-- burns 100 percent of purchased GoCoin
  |   (removed from circulation forever)
  |
  +-- activates Max's Pro subscription for 30 days

Separate channel:
  Node reward pool (40 million GoCoin)
  emits monthly GoCoin to operators
  proportional to work performed

Net effect over time:
  More subscriptions -> more burn -> scarcer GoCoin
  More operators needed -> more demand for GoCoin
  Operators hold GoCoin -> their holdings appreciate
  Foundation collects grants + enterprise fees in EUR -> pays developers
```

The user experience is simple: pay 5 euros, get one month of Pro.
Exactly like Netflix. The complexity is in the smart contract and
is invisible to the user.

### 3.3 Why this works where Session failed

Session's design required users to hold SESH for Pro features. When
SESH fell 90 percent from its peak, users who prepaid saw their
prepayment's relative value collapse, and the foundation's treasury
denominated in SESH lost most of its purchasing power. Development
stopped when runway ran out.

GoNode's design insulates users from SESH-style volatility (they pay
in EURC), insulates the foundation from SESH-style treasury risk
(operating revenue is in EUR from Pro subs, enterprise SLAs, AI
services, and grants), and gives operators direct exposure to network
growth (their GoCoin holdings appreciate as burn exceeds emission).

When a bear market hits, GoNode loses token-denominated paper value
in operator holdings but continues operating normally because
day-to-day costs are paid in EUR from real revenue.

---

## 4. Design decisions

### 4.1 Arbitrum One over custom blockchain

GoNode deploys on Arbitrum One rather than building its own Layer 1
blockchain. The decision:

- Session proved Arbitrum works for this use case (they migrated to
  it in May 2025 from their own Oxen appchain)
- Arbitrum has Ethereum-level security with transaction costs under
  0.02 USD, suitable for frequent operator rewards
- The Arbitrum Foundation has an active grant program (up to several
  million USD) and pre-existing relationships with privacy projects
- Existing EVM tooling, wallets, and developer ecosystems immediately
  available
- Custom L1 development adds 12 to 24 months of work with no upside
  over a mature rollup

A custom appchain for service-node consensus (swarm assignment, fast
slashing) runs separately because Arbitrum finality (around 1 hour
for full security) is too slow for operational decisions. The
appchain checkpoints to Arbitrum daily.

### 4.2 Swarms over DHTs

GoNode uses deterministic swarm assignment (5 to 10 nodes per queue
subset) rather than a distributed hash table or Kademlia-style
peer-to-peer routing. The decision:

- Swarms provide automatic replication without client coordination
- Clients discover swarms through deterministic hash functions, no
  directory service required
- Swarm membership changes predictably at epoch boundaries
- Fault tolerance is built in - up to 4 swarm members can go offline
  without message loss
- Session proved the model at ~2,000 nodes and 1.7 million users
- DHT approaches (IPFS, Kademlia) have documented problems with
  reliability and eclipse attacks at this scale

### 4.3 Reed-Solomon for files, replication for messages

Different data types get different redundancy strategies:

**16 KB message blocks:** simple 3-to-5x replication across swarm
members. Erasure coding 16 KB into 29 shards of 565 bytes each would
be smaller than the metadata overhead. Replication is the correct
choice at this payload size.

**XFTP file chunks (256 KB to 4 MB):** Reed-Solomon RS(10, 16). Each
chunk becomes 16 shards of which any 10 can reconstruct the original.
1.6x storage overhead for 11-nines durability, compared to 3x for
simple replication. This matches Storj's production-proven approach.

### 4.4 Audit-based proofs over Filecoin PoRep

GoNode does not use Filecoin-style Proof of Replication or Proof of
Spacetime. These proofs are designed for 32 GiB static sectors and
produce overhead that exceeds the payload at 16 KB. Instead, GoNode
uses lightweight audit challenges:

- Every hour, each node receives approximately 10 random challenges
- Each challenge: compute HMAC-SHA256 for a specific block
- Correct fast response maintains reward weight
- Incorrect or missing responses reduce rewards, then trigger
  deregistration, then disqualification with full held-back burn

This matches Storj's production-proven audit model and is sufficient
to detect data loss, corruption, offline nodes, and multi-instance
Sybil attacks.

### 4.5 Client-side random-key encryption over convergent

Every message and file chunk is encrypted with a fresh random key
generated by the client. Keys are transmitted through the SimpleX
queue system separately from the ciphertext.

This rules out convergent encryption despite its deduplication
benefit. Convergent encryption allows confirmation-of-a-file attacks
where an adversary with a candidate plaintext can probe whether the
network stores it. For a messenger where messages are short and
partially predictable, this attack is devastating. Random-key
encryption prevents it completely.

The zero-knowledge architecture also provides critical legal
protection. Under DSA Article 6, hosting intermediaries are protected
from liability for user content unless they have actual knowledge of
illegal content. When operators cannot decrypt, they cannot have
actual knowledge.

### 4.6 Swiss Stiftung over German GmbH for protocol operation

GoNode's protocol is operated by a Swiss Stiftung (foundation) in
Zug, not by the German GmbH in Recklinghausen. The decision:

- Switzerland has clear regulatory treatment of foundations
- Zug is the established crypto jurisdiction with banking access
- Swiss brand sells to enterprise customers internationally
- Separation protects individual German developers from
  protocol-level liability
- Template proven by Ethereum Foundation, Session Technology
  Foundation, Nym Technologies, and Threema
- German GmbH continues for publishing and BaFin compliance

### 4.7 MiCA utility token over security or stablecoin

GoCoin is deliberately designed as a utility token under MiCA Article
3(1)(9), avoiding the ART (asset-referenced token) and EMT (e-money
token) classifications. The decision:

- No peg to fiat or basket (would trigger ART regime, very heavy)
- No redemption promise (would trigger EMT regime, requires e-money
  license with 350,000 EUR capital minimum)
- No pro-rata profit distribution (would trigger securities laws)
- No voting rights that translate to financial rights (keeps away
  from MiFID II)
- Title II whitepaper notification to BaFin is the only MiCA
  requirement

Node stakers and operators are service providers to the network,
not investors in a security. This is the same classification as
Helium's HNT, Session's SESH, and Filecoin's FIL.

### 4.8 Revenue before token, always

The single most important design decision. Every previous
decentralised messenger project launched its token first and hoped
revenue would follow. None succeeded. GoNode inverts this:

- Phase 1 (months 3-9): enterprise pilots and AI developer support
  generate EUR revenue
- Phase 2 (months 9-15): public testnet with points, Pro subscription
  beta in EUR
- Phase 3 (months 15-24): only now does the token launch, with 18
  months of EUR-denominated runway already secured

This means the token is launched into an existing business with
paying customers and proven demand. The token enhances economics; it
does not create them.

### 4.9 Four revenue streams instead of one

GoNode's financial model intentionally avoids dependency on any
single revenue source. Four parallel streams:

- GoNode Pro subscriptions (consumer, predictable, recurring)
- Enterprise SLA contracts (high-value, low-churn, fiat)
- AI Developer Support service (high-margin, specialised)
- Non-dilutive grants (strategic, ongoing)

If any one stream collapses, the remaining three can sustain
operations. Session's mistake was relying entirely on token value;
GoNode diversifies away from this concentration risk.

### 4.10 No custody, no on-ramp, no exceptions

The Foundation never holds user funds and never operates a fiat-to-crypto
exchange. The reasons are legal as much as technical:

- Avoids CASP authorisation under MiCA Title V (massive compliance
  burden)
- Avoids BaFin Kryptoverwahrgeschäft license under KWG
- Avoids Geldwäschegesetz Verpflichteter status
- Avoids the failure mode that sank Tornado Cash developers, Samourai
  Wallet founders, and Helix/Bitcoin Fog operators

Users acquire GoCoin through licensed third-party exchanges (Uniswap
for DEX, MEXC/Gate/KuCoin for CEX). The Foundation only provides
initial DEX liquidity, which is not a regulated activity.

---

## 5. What GoNode does NOT do

- **GoNode does not store message content in plaintext.** All data is
  client-side encrypted with random keys. Nodes store only ciphertext.
- **GoNode does not verify user identity.** That is GoUNITY's job.
  GoNode verifies operator identity, not user identity.
- **GoNode does not moderate content.** That is GoBot's job. GoNode
  provides the infrastructure GoBot runs on.
- **GoNode does not replace SimpleX.** It enhances SimpleX with
  decentralised infrastructure and economic incentives.
- **GoNode does not hold user funds.** All Pro payments go directly
  to smart contracts, not to the Foundation.
- **GoNode does not exchange fiat for crypto.** Users acquire GoCoin
  through licensed third-party exchanges.

---

## 6. Comparison with existing systems

### 6.1 Session

Session is the closest architectural analogue. GoNode borrows the
service-node swarm model, onion routing, and PoS staking pattern.
The key differences:

| Dimension | Session | GoNode |
|:----------|:--------|:-------|
| Protocol | Session protocol (custom) | SimpleX SMP/XFTP |
| Messenger infrastructure | Centralised app + decentralised relays | Decentralised throughout |
| User payment | SESH tokens (volatile) | EURC (stable) |
| Foundation revenue | Token speculation, donations | Pro + enterprise + grants |
| Hardware identity | None | GoKey integration |
| File storage | Limited, swarm-replicated | Reed-Solomon sharded |
| Status | Shutdown announced April 2026 | Concept phase |

### 6.2 Filecoin and Storj

Filecoin and Storj are storage networks, not messaging networks.
GoNode borrows their storage patterns (Reed-Solomon, audit challenges,
held-back payments) but combines them with messaging-specific
requirements (low latency, small payloads, onion routing).

Filecoin's PoRep/PoSt proofs are designed for 32 GiB sectors and do
not fit GoNode's 16 KB message blocks. Storj's audit model scales
down cleanly.

### 6.3 Matrix/Element

Matrix proves that federated privacy infrastructure can be profitable
without a token. German BundesMessenger, French Tchap, NATO ACT,
Swedish SAFOS, and many others are paying customers.

GoNode learns from this: enterprise SLAs are a viable primary revenue
stream. GoNode's advantage over Matrix is true decentralisation (no
federated homeservers to compromise) and hardware identity integration
(GoKey).

### 6.4 Threema

Threema has 12 million users and is profitable through a single 5 EUR
one-time purchase. This proves that paid privacy messengers work at
scale. Threema is centralised (single Swiss operator) and monolithic.

GoNode learns from this: users will pay for privacy. The subscription
model captures greater lifetime value, and decentralisation provides
resilience Threema cannot offer.

### 6.5 Helium

Helium provides the tokenomic template. After the 2025 consolidation
to USD-priced Data Credits minted by burning HNT, Helium's 2 million
monthly daily actives (Helium Mobile) and 450,000 paying subscribers
demonstrate that burn-and-mint equilibrium with USD-denominated end
user pricing works in practice.

GoNode applies the same pattern: EURC-denominated Pro subscriptions,
GoCoin-denominated operator rewards, and a burn mechanism that ties
token value to real usage.

---

## 7. Dependencies and timeline

### What must exist before GoNode development

| Dependency | Why GoNode needs it | Status |
|:-----------|:--------------------|:-------|
| SimpleGo SMP stack | Protocol foundation | Complete (47 files, 21,863 LOC) |
| GoBot Go service | Reference implementation patterns | In development (Season 2) |
| GoKey hardware identity | Optional operator attestation | Planned (Season 3) |
| GoUNITY certificate authority | User identity layer (separate concern) | Planned (Season 4) |
| Arbitrum One | Deployment target for economic layer | Available |
| Circle EURC | User payment currency | Available |
| libsodium and Reed-Solomon libraries | Crypto primitives | Available |

### GoNode development phases

| Phase | Focus | Season |
|:------|:------|:-------|
| Phase 0 | Legal skeleton, Foundation setup, grants, team building | Season 1 |
| Phase 1 | Permissioned testnet, 20-50 operators, enterprise pilots | Season 2 |
| Phase 2 | Public testnet with incentive points, MiCA whitepaper | Season 3 |
| Phase 3 | Token Generation Event, airdrop, mainnet launch | Season 4 |
| Phase 4 | DAO governance transition, ecosystem integration | Season 5+ |

---

## 8. Open questions

| Question | Options | Recommended default |
|:---------|:--------|:-------------------|
| L2 choice | Arbitrum One / Base / Optimism / Cosmos appchain | **Arbitrum One** (Session precedent, grants) |
| Foundation domicile | Switzerland / Liechtenstein / Estonia | **Switzerland Zug** (brand, banking) |
| Pro pricing denomination | Direct EURC / Data Credits | **Direct EURC** (simpler UX) |
| Node stake amount | 5k / 10k / 20k GoCoin | **10k** (testnet-validated) |
| Illegal content strategy | Perceptual hashing / zero-knowledge | **Zero-knowledge** (cleaner legal) |
| Ecosystem positioning | Standalone network / economic backbone | **Economic backbone** of SimpleGo |

Each of these should be validated in Phase 1-2 testnet before mainnet
commitment.

---

## 9. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [SimpleGo](https://github.com/saschadaemgen/SimpleGo) | SMP stack foundation, hardware messenger | [SimpleGo repo](https://github.com/saschadaemgen/SimpleGo) |
| [GoBot](https://github.com/saschadaemgen/GoBot) | Moderation layer running on GoNode relays | [Architecture](https://github.com/saschadaemgen/GoBot/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) |
| [GoKey](https://github.com/saschadaemgen/SimpleGo) | Hardware identity for operators | [Architecture](https://github.com/saschadaemgen/SimpleGo/blob/main/templates/gokey/docs/ARCHITECTURE_AND_SECURITY.md) |
| [GoUNITY](https://github.com/saschadaemgen/GoUNITY) | User identity layer (separate from GoNode) | [Architecture](https://github.com/saschadaemgen/GoUNITY/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) |
| [GoLab](https://github.com/saschadaemgen/GoLab) | Community platform using GoNode for fan-out | [Architecture](https://github.com/saschadaemgen/GoLab/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) |

---

*GoNode Technical Concept v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
