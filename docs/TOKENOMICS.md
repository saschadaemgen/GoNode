# GoNode Loyalty System

**Document version:** Season 1 | April 2026
**Component:** GoCoin - closed-loop loyalty rewards system for the GoNode ecosystem
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

GoCoin is the loyalty and rewards unit of the GoNode ecosystem. It is **not a cryptocurrency**, not a utility token, not a security, and not electronic money. GoCoin is a **closed-loop loyalty system** - comparable in legal and operational structure to Payback points, Lufthansa Miles & More, Deutsche Bahn BahnBonus, Steam Wallet credits, or in-game currencies like Fortnite V-Bucks.

The design principles are deliberately conservative:

- **No sale of GoCoin for money.** Not by the Foundation, not peer-to-peer, not for EUR, not for any other currency or crypto asset.
- **No public trading markets.** No DEX liquidity, no CEX listings, no external exchanges.
- **Coins stay in the ecosystem.** Redemption is only possible for goods and services within the SimpleGo ecosystem.
- **Foundation is never counterparty.** Users earn from purchases or node operation, redeem within the ecosystem, or exchange with other users for ecosystem items. The Foundation only operates the marketplace infrastructure.
- **Peer-to-peer barter, not trade.** Users can offer coins for other items/coins on an internal auction marketplace, but cannot sell them for money.

This design places GoCoin firmly within the established legal framework for loyalty programs in Germany and the EU, avoiding the regulatory complexity and legal risks of crypto tokens.

---

## 1. What GoCoin is (and is not)

### 1.1 What GoCoin is

GoCoin is a **digital loyalty point** issued by IT and More Systems GmbH to reward:

- Users who purchase services (Pro subscriptions, hardware, premium features) in EUR
- Node operators who contribute computing resources to the network
- Community contributors who add value (moderated content, development, translations)

GoCoin functions as:

- **A reward currency** within the SimpleGo ecosystem
- **A redemption instrument** for special editions, exclusive content, hardware, premium features
- **A barter token** on the peer-to-peer marketplace for trading ecosystem items between users
- **A recognition signal** for active community participants

### 1.2 What GoCoin is NOT

GoCoin is explicitly **not**:

| What it's NOT | Why this matters legally |
|:--------------|:-------------------------|
| A cryptocurrency | Avoids MiCA Title II whitepaper obligations |
| A utility token | Avoids MiCA Art. 3(1)(9) classification |
| Electronic money | Avoids E-Money Directive 2009/110/EC |
| A payment instrument | Avoids PSD2 licensing requirements |
| A security | Avoids MiFID II and Wertpapierhandelsgesetz |
| An investment asset | Avoids KAGB and investment fund regulations |
| A store of value | Avoids being classified as currency |
| Redeemable in EUR | Cannot become E-Money under Art. 11 EMD |
| Tradeable on exchanges | No CASP authorisation needed under MiCA Title V |

### 1.3 Legal classification

GoCoin is designed to fall within the **limited network exception** under:

- **Article 3(k) Payment Services Directive 2 (2015/2366)** - "limited network of service providers, or for a very limited range of goods and services"
- **§ 2 Abs. 1 Nr. 10 Zahlungsdiensteaufsichtsgesetz (ZAG)** - German implementation of the limited network exemption
- **Recital 14 E-Money Directive (2009/110/EC)** - exemption for closed-loop schemes

This is the same legal basis under which Payback, Miles & More, BahnBonus, Deutsche Telekom Magenta Moments, and similar German loyalty programs operate without needing e-money licenses or payment service authorisation.

---

## 2. How GoCoin works

### 2.1 Earning GoCoin

Users and operators earn GoCoin through four distinct channels:

**Channel 1: Purchase rewards**

When users purchase services in EUR, they receive a proportional GoCoin bonus as a loyalty reward:

| Purchase | GoCoin reward (indicative) |
|:---------|:---------------------------|
| Pro subscription (5 EUR/month) | 5 GoCoin |
| Pro annual (50 EUR/year) | 75 GoCoin (25% bonus for annual commitment) |
| Hardware device (varies) | 10% of purchase value in GoCoin |
| Premium plugin | 20% of purchase value in GoCoin |
| Enterprise SLA | Custom rewards schedule per contract |

The reward is a **standard loyalty bonus** similar to "for every 10 EUR spent, you earn 1 Payback point". The legal basis is a voluntary gift (Rabatt/Bonus) from the seller to the buyer, not a separate financial instrument.

**Channel 2: Node operator rewards**

Operators running GoNode infrastructure earn monthly GoCoin based on:

- Uptime percentage
- Data volume served
- Audit response correctness
- Geographic/network diversity bonus

Operator rewards are treated as **service compensation** - payment for a service rendered (infrastructure provision). These rewards are taxable income for the operator under German tax law (see section 8).

**Channel 3: Community contributions**

Community members earn GoCoin for verified valuable contributions:

- Moderated high-quality content in GoLab
- Bug reports that lead to accepted fixes
- Translations of ecosystem documentation
- Security research (per bug bounty program)
- Third-party integrations published on our marketplace

Community rewards are issued at the Foundation's discretion based on objective quality criteria.

**Channel 4: Peer-to-peer marketplace**

Users can **acquire** GoCoin from other users by offering them ecosystem items, other GoCoin, or services within the ecosystem. This is explained in detail in section 3.

### 2.2 Spending GoCoin

GoCoin can only be redeemed for goods and services **within the SimpleGo ecosystem**:

| Redemption option | Example |
|:------------------|:--------|
| Special edition firmware | Limited run of SimpleGo devices with exclusive features |
| Premium profile features | Verified badge, custom themes, priority support |
| Exclusive content access | Premium tutorials, early access to new features |
| Hardware discounts | Partial payment for next GoKey or SimpleGo device |
| Conference tickets | Entry to IT and More events, workshops |
| Physical merchandise | T-shirts, stickers, limited print editions |
| Priority features | Front-of-queue for new service activations |

Redemption is at a **fixed EUR-equivalent rate** set by the Foundation. Example: 100 GoCoin = one special edition firmware unlock. Users always know exactly what their coins are worth in ecosystem goods.

**Important:** Users cannot redeem GoCoin for EUR or any other currency. The Foundation will never buy back GoCoin. This is essential for maintaining the legal classification as a loyalty program.

### 2.3 The peer-to-peer marketplace

The marketplace allows users to trade GoCoin and ecosystem items between each other - but never for money.

**What users can do:**

- Offer GoCoin in exchange for other users' ecosystem items
- Auction rare special edition items with GoCoin as the bidding currency
- Trade unlocked content access between users
- Gift GoCoin to other users (no fee, just a simple transfer)

**What users cannot do:**

- Sell GoCoin for EUR, USD, USDT, Bitcoin, or any other currency
- List their coins on external exchanges (technically impossible: no public blockchain)
- Cash out through the Foundation
- Use GoCoin as payment for services outside the ecosystem

**How the marketplace works:**

Users browse listings, place bids, and complete barter trades. The Foundation operates the marketplace infrastructure (like eBay operates an auction platform) but does not act as buyer or seller. All trades are directly between users, with the marketplace as escrow and dispute resolution venue.

**Marketplace fee structure:**

The Foundation charges a small fee (e.g., 2-5% of transaction value in GoCoin) on completed trades. This fee is burned (removed from circulation) to control supply inflation. The Foundation does not profit monetarily from trades - the fee is sink mechanism, not revenue.

---

## 3. Node operator economics

### 3.1 Holding period

Node operators face a **30-day holding period** on newly earned GoCoin before they can:

- List coins on the marketplace
- Trade coins with other users
- Transfer coins to others

During the holding period, operators can:

- Redeem their coins directly with the Foundation for ecosystem goods
- Accumulate coins for long-term holding
- Continue earning additional coins from ongoing operation

**Why a holding period:** Prevents operators from dumping fresh earnings onto the marketplace immediately, which would destabilise the internal coin/item price equilibrium. Similar mechanisms are used in Steam Marketplace (7-day lock on traded items) and are standard in loyalty programs.

### 3.2 Operator earnings projections

At network maturity (Year 3-5), typical monthly earnings for a standard operator:

| Network size | Monthly emission | Operators | Average earnings |
|:-------------|:----------------|:----------|:-----------------|
| Year 1 | 40,000 GoCoin | 100 | 400 GoCoin/node |
| Year 2 | 60,000 GoCoin | 300 | 200 GoCoin/node |
| Year 3 | 80,000 GoCoin | 600 | 133 GoCoin/node |
| Year 4 | 100,000 GoCoin | 1,000 | 100 GoCoin/node |
| Year 5 | 120,000 GoCoin | 1,500 | 80 GoCoin/node |

**Important:** Because GoCoin has no monetary market value, these numbers are in ecosystem-utility terms, not currency. 100 GoCoin means "credit for 100 EUR worth of ecosystem redemption value" - not "100 EUR that can be withdrawn".

### 3.3 No DEX pool, no initial liquidity required

Because GoCoin is not tradeable for money, **no liquidity pool is needed**. This eliminates:

- 500,000 EUR Foundation liquidity requirement (from the old model)
- Market maker engagement costs
- CEX listing fees (10,000 - 30,000 EUR per listing)
- Uniswap V3 setup and management
- Smart contract deployment on Arbitrum for token economics
- Ongoing gas cost obligations

This saves the Foundation approximately **600,000 - 800,000 EUR in setup costs** compared to the original crypto token design.

---

## 4. Supply management

### 4.1 Total issuance cap

The Foundation commits to a **soft cap of 100,000,000 GoCoin** total issuance. Unlike a crypto token, this cap is not cryptographically enforced - it is a **policy commitment** in the Terms of Service. The Foundation cannot technically exceed the cap, because the database (or private chain) enforces it at the application level.

**Why a cap:** Prevents unlimited inflation that would devalue existing holdings. Users know that their coins represent a meaningful fraction of the total supply. This transparency is important for user trust in the loyalty program.

### 4.2 Issuance schedule

GoCoin issuance follows a controlled schedule:

| Category | Allocation | Release schedule |
|:---------|:-----------|:-----------------|
| Purchase rewards | 40,000,000 | Earned by users over 10+ years |
| Node operator rewards | 40,000,000 | Emitted monthly over 10+ years (decaying) |
| Community contributions | 10,000,000 | Discretionary Foundation issuance |
| Foundation reserve | 10,000,000 | Held for future initiatives (never sold) |

The 40M operator reward pool emits on a decaying curve similar to Bitcoin halving - more in early years when fewer operators exist, less as the network matures.

### 4.3 Burn mechanisms

GoCoin is removed from circulation through multiple channels:

- **Redemption burn:** When users redeem coins for special editions, those coins are burned (removed from circulation)
- **Marketplace fee burn:** The 2-5% marketplace fee is burned on every trade
- **Inactive account reclamation:** After 5 years of inactivity, accounts may be archived with coins returned to the Foundation reserve
- **Discretionary burns:** The Foundation may burn coins from its reserve to control supply inflation

### 4.4 Transparency commitments

The Foundation publishes monthly:

- Total GoCoin in circulation
- Coins issued in the past month (by category)
- Coins burned in the past month (by mechanism)
- Active account count
- Marketplace transaction volume

This transparency is equivalent to what Payback and similar loyalty programs publish in their annual reports. It provides accountability without requiring a public blockchain.

---

## 5. Technology choice

### 5.1 Database vs. permissioned blockchain

Two technology options are viable for the GoCoin ledger. Both are under evaluation, with the final choice to be made in Phase 1:

**Option A: Internal database (PostgreSQL or similar)**

- **Approach:** Standard ACID-compliant relational database maintained by the Foundation
- **Used by:** Payback, Miles & More, Steam Wallet, PSN, most major loyalty programs
- **Advantages:**
  - Simple to implement and operate
  - Very high performance (millions of transactions per second possible)
  - Lower operational cost
  - Standard enterprise software practices
  - No blockchain-related regulatory questions
- **Disadvantages:**
  - Users must trust Foundation's bookkeeping
  - No independent verification of balances
  - Single point of technical failure (mitigated by backup and replication)

**Option B: Permissioned blockchain (Hyperledger Fabric or similar)**

- **Approach:** Distributed ledger with pre-approved validator nodes
- **Used by:** IBM Food Trust, some banking consortia, supply chain systems
- **Advantages:**
  - Transparent ledger that multiple parties can independently verify
  - Tamper-evident transaction history
  - Decentralises trust from the Foundation to a validator consortium
  - Aligns philosophically with the decentralisation theme of GoNode
- **Disadvantages:**
  - Higher operational complexity and cost
  - Slower transaction throughput (though still adequate for loyalty program needs)
  - Requires governance decisions about who runs validator nodes
  - Adds regulatory considerations (though permissioned chains are generally treated as databases for regulatory purposes)

### 5.2 Recommendation

**Phase 1 (initial implementation):** Start with internal PostgreSQL database. This is the fastest path to a working system and what 99% of loyalty programs use successfully.

**Phase 3+ (if community demand):** Consider migrating to or supplementing with a permissioned blockchain for transparency. This is a future architectural decision, not a launch requirement.

The specific technology does not change the legal classification. Whether the ledger lives in PostgreSQL or Hyperledger, GoCoin remains a loyalty point under PSD2 Art. 3(k) and ZAG § 2.

### 5.3 Integration with GoNode infrastructure

Regardless of the ledger technology, GoCoin operations integrate with the GoNode ecosystem through:

- **Authentication:** GoUNITY certificates identify users
- **Authorisation:** Smart permissions define who can earn, spend, transfer
- **Transport:** SMP protocol carries coin transactions (encrypted)
- **Hardware binding:** Optional GoKey device provides hardware-anchored identity for higher-value operations

---

## 6. User experience

### 6.1 What users see

For end users, GoCoin is as simple as Payback points. Their experience:

- Buy a Pro subscription for 5 EUR → automatically earn 5 GoCoin
- Open profile → see GoCoin balance and earning history
- Browse marketplace → see what special items can be redeemed or traded for
- Redeem coins → click "redeem", select item, receive it
- Trade with other users → post offer, accept bids, complete trades

No wallets required. No private keys. No seed phrases. No gas fees. No confusion about what the coins are "worth" in money terms.

### 6.2 What operators see

Operators have a similar experience with additional features:

- Earnings dashboard showing monthly GoCoin accrual
- Performance metrics (uptime, audit response, diversity bonus)
- Holding period countdown for marketplace access
- Direct redemption to Foundation for ecosystem goods
- Historical earnings statements for tax purposes

### 6.3 Terms of Service commitments

The Foundation's Terms of Service commit to:

- **No unilateral devaluation:** Redemption ratios cannot be worsened without 6 months notice
- **No arbitrary cancellation:** Accounts cannot be closed without cause, giving users time to redeem
- **Reasonable expiry policy:** Coins do not expire except after 5+ years of account inactivity
- **Transparent reporting:** Monthly supply and transaction reports
- **Dispute resolution:** Clear procedure for marketplace disputes

These commitments align with German consumer protection law and EU Consumer Rights Directive requirements.

---

## 7. Legal framework

### 7.1 Limited network exemption

GoCoin qualifies for the limited network exemption because:

- It is issued by a single entity (IT and More Systems GmbH)
- It can only be redeemed within the SimpleGo ecosystem
- It is not generally accepted for payment outside the ecosystem
- The Foundation does not purchase coins back for money
- No external market is permitted or facilitated

This places GoCoin alongside:

- Payback Punkte (since 2000, never regulated as e-money)
- Lufthansa Miles (since 1993, standard airline loyalty)
- Amazon Coins (digital credit for Kindle/Appstore purchases)
- Steam Wallet (gaming platform closed economy)
- BahnBonus (Deutsche Bahn loyalty since 2000)

None of these require e-money licenses or payment service authorisation.

### 7.2 MiCA does not apply

MiCA Regulation (EU 2023/1114) applies to "crypto-assets", defined in Art. 3(1)(5) as digital representations of value that can be transferred and stored electronically using distributed ledger technology.

GoCoin:

- Is not a crypto-asset under MiCA - it's a closed-loop loyalty point
- Is not traded on public markets (MiCA Title III/IV do not apply)
- Is not offered to the public as an investment (MiCA Title II does not apply)
- Does not involve Crypto-Asset Service Providers (MiCA Title V does not apply)

Even if GoCoin were hypothetically classified as a crypto-asset, it would fall under the **Art. 2 exclusions** for limited-network instruments, similar to PSD2 Art. 3(k).

### 7.3 DSA obligations (marketplace)

The Digital Services Act (EU 2022/2065) applies to the peer-to-peer marketplace:

- **Art. 16 (notice-and-action):** The Foundation implements a reporting mechanism for illegal content/offers
- **Art. 14 (terms and conditions):** Clear marketplace rules, easily accessible
- **Art. 30 (traceability of traders):** Not applicable if all users are consumers; if commercial users participate, traceability requirements apply
- **Art. 32 (specific obligations for online marketplaces):** Design choices for safe and transparent marketplace

The marketplace is **not a VLOP** (Very Large Online Platform - 45M+ EU users threshold), so VLOP-specific obligations do not apply.

### 7.4 GDPR compliance

Standard GDPR compliance applies:

- User accounts and transaction history are personal data
- Legal basis for processing: contract performance (Art. 6(1)(b))
- Data minimisation: only necessary data collected
- Right to access, rectification, erasure respected
- Data retention policies published
- DPO designation per Art. 37 if applicable

The decision between internal database vs. permissioned blockchain affects GDPR implementation:

- **Database:** Simple GDPR compliance - data can be deleted on request per Art. 17
- **Permissioned blockchain:** More complex - EDPB Guidelines 02/2025 address blockchain immutability, generally requires pseudonymisation and justified retention

This is another reason to start with the database option.

---

## 8. Taxation

### 8.1 Tax treatment for node operators

Node operator GoCoin rewards are taxable income. The specific classification depends on the operator's circumstances:

**Gewerbliche Tätigkeit (commercial activity):** If operating nodes as a business, income falls under § 15 EStG. Requires Gewerbeanmeldung, subject to Gewerbesteuer above thresholds.

**Sonstige Einkünfte (other income):** For small-scale operators, rewards may fall under § 22 Nr. 3 EStG, with a Freibetrag of 256 EUR/year.

**Valuation:** Rewards are valued at their fair market value at the time of receipt - the "redemption value" of GoCoin at that moment (e.g., if 100 GoCoin redeems for 100 EUR of ecosystem goods, each GoCoin is valued at 1 EUR for tax purposes).

The Foundation provides operators with annual earnings statements for tax reporting.

### 8.2 Tax treatment for users earning purchase bonuses

Purchase reward GoCoin is treated like any other loyalty bonus:

- **Typically tax-free** as a Rabatt (rebate) reducing the effective purchase price
- Similar treatment to Payback points, airline miles, cashback programs
- BMF-Schreiben on loyalty programs (2015/12/10) provides guidance
- No taxable event at redemption if redeemed for services from the issuer

### 8.3 Tax treatment for marketplace trades

When users trade GoCoin and ecosystem items between each other:

- **Private sales exception (§ 23 EStG):** Gains may be tax-free if held more than 1 year and under 600 EUR/year threshold
- **Sonstige Leistungen (§ 22 Nr. 3 EStG):** Commercial trading may be subject to income tax
- **DAC7 reporting:** Platform operators must report user transactions above thresholds (1000 EUR or 30 transactions per year)

The Foundation implements DAC7-compliant reporting to tax authorities as required.

### 8.4 VAT treatment

- **Purchase rewards:** Not a separate VAT event - the reward is included in the original purchase
- **Redemption:** VAT applies when goods/services are delivered in exchange for coins
- **Marketplace trades:** Typically outside VAT scope for private users; commercial users may trigger VAT
- **Foundation marketplace fees:** VAT applies to Foundation's fee income if above small-business threshold

---

## 9. Comparison: old crypto token model vs. new loyalty model

| Dimension | Old (crypto token) | New (loyalty system) |
|:----------|:-------------------|:---------------------|
| Legal classification | MiCA Art. 3(1)(9) utility token | PSD2 Art. 3(k) / ZAG § 2 limited network exemption |
| Monetary value | Tradeable, market-priced | Fixed redemption value, not tradeable for money |
| User complexity | Wallet, seed phrase, gas fees | Standard account, like Payback |
| Foundation setup cost | ~600,000 EUR (liquidity, listings, audits) | ~50,000 EUR (database + marketplace) |
| Legal risk | High (Tornado Cash precedent, MiCA compliance) | Low (established loyalty framework) |
| CEX/DEX listings | Required for liquidity | Not needed |
| BaFin whitepaper | Required before public offer | Not required |
| CASP authorisation | Risk of triggering | Not applicable |
| Price volatility | High (user funds at risk) | None (fixed ecosystem value) |
| Technology | Arbitrum smart contracts + DEX | Database or permissioned chain |
| Scale | Limited by Arbitrum TPS | Millions of TPS possible |
| Target market | Crypto-native users | All users (mainstream accessible) |
| Regulatory burden | MiCA + KWG + GwG + potentially CASP | DSA + GDPR + standard loyalty regs |
| Tax complexity (users) | High (every trade is taxable) | Low (loyalty bonuses typically tax-free) |
| Compliance cost ongoing | ~200,000 EUR/year | ~30,000 EUR/year |

---

## 10. Roadmap alignment

The new loyalty model aligns with a revised ecosystem roadmap:

**Phase 0 (Months 0-3): Foundation and concept**

- Foundation setup (Switzerland or Germany)
- Grant applications (same pipeline as before)
- Legal opinion confirming limited network exemption classification
- Terms of Service drafting

**Phase 1 (Months 3-9): First implementation**

- Internal database deployment
- User earnings infrastructure (purchase -> coin issuance)
- Redemption catalog (initial special editions)
- Foundation reserve allocation

**Phase 2 (Months 9-15): Node operator rewards**

- Node operator earnings go live
- Holding period mechanics
- Monthly emission schedule
- Operator dashboard

**Phase 3 (Months 15-21): Marketplace launch**

- Peer-to-peer marketplace beta
- Auction and barter mechanics
- Dispute resolution framework
- DSA compliance implementation

**Phase 4 (Months 21-30): Scale and optimisation**

- Permissioned blockchain evaluation (if demand warrants)
- Expanded redemption options
- Integration with GoShop, GoTube, GoBook as they launch
- International expansion (within EU)

---

## 11. Risks and mitigations

### 11.1 Classification risk

**Risk:** BaFin or another regulator reclassifies GoCoin as e-money or crypto-asset.

**Mitigation:**
- Legal opinion before launch confirming limited network exemption
- Conservative design staying within established precedent (Payback, Miles)
- No redemption in money
- No public markets
- Transparent documentation

### 11.2 Marketplace abuse risk

**Risk:** Users use the marketplace for money laundering or to circumvent loyalty program status.

**Mitigation:**
- AML monitoring for suspicious patterns
- Volume thresholds triggering review
- DAC7 compliance for commercial users
- No cash-out mechanism
- Audit trail in database/chain

### 11.3 User trust risk

**Risk:** Users worry about Foundation manipulating the ledger.

**Mitigation:**
- Monthly transparency reports
- External audit of supply and burns
- Option to migrate to permissioned blockchain later
- Strong Terms of Service commitments
- Legal liability for misconduct

### 11.4 Operator churn risk

**Risk:** Operators find the rewards insufficient and leave.

**Mitigation:**
- Sufficient reward pool (40M coins over 10+ years)
- Holding period prevents immediate dumping
- Real ecosystem utility for earned coins
- Hardware binding (GoKey) creates switching costs

---

## 12. Comparison to real-world precedents

### 12.1 Payback (Germany, since 2000)

- 30+ million users in Germany
- Legal basis: limited network exemption
- Points earned through purchases, redeemable for goods/donations/transfers to partners
- No e-money license
- Annual revenue: ~500M EUR

GoCoin follows the same legal structure but adds a peer-to-peer marketplace (which Payback does not have).

### 12.2 Lufthansa Miles & More (since 1993)

- 36+ million members worldwide
- Miles earned through flights and partner purchases
- Redeemable for flights, upgrades, goods
- Peer-to-peer: Family Sharing allows limited transfers between members
- No e-money regulation

GoCoin follows similar structure with broader peer-to-peer capabilities.

### 12.3 Steam Marketplace (Valve)

- 130+ million active users globally
- Digital items earned through gameplay or purchased
- Marketplace allows peer-to-peer trading with Steam Wallet (not for cash)
- 7-day holding period on traded items (like our operator holding period)
- Marketplace fee ~15% (we charge 2-5%)

GoCoin marketplace structure closely mirrors Steam's approach.

### 12.4 Fortnite V-Bucks (Epic Games)

- 400+ million player accounts
- V-Bucks purchased with money, redeemed in-game
- No peer-to-peer marketplace
- Recent FTC settlement (USA) established some consumer protection requirements

GoCoin learns from V-Bucks in terms of clear redemption and transparent pricing.

### 12.5 EVE Online ISK/PLEX

- 300,000+ active users
- Closed economy with complex player-driven markets
- PLEX acts as premium currency with peer-to-peer trading
- 20+ years of successful operation without regulatory intervention
- Sophisticated economic reports published regularly

GoCoin borrows from EVE's transparency and long-running closed economy model.

---

## 13. Related documents

| Document | Relationship |
|:---------|:-------------|
| [README](../README.md) | Project overview including loyalty system summary |
| [Concept](CONCEPT.md) | Strategic rationale for the ecosystem |
| [Architecture and Security](ARCHITECTURE_AND_SECURITY.md) | Technical foundation |
| [Business Model](BUSINESS_MODEL.md) | Revenue streams that fund the loyalty program |
| [Legal Compliance](LEGAL_COMPLIANCE.md) | Detailed regulatory analysis |
| [Smart Contracts](SMART_CONTRACTS.md) | Technical specifications for coin issuance/burn |
| [Wire Protocol](WIRE_PROTOCOL.md) | Protocol specifications for coin transactions |
| [Roadmap](ROADMAP.md) | Implementation timeline |

---

*GoNode Loyalty System v2 - April 2026 (replaces v1 crypto token design)*
*IT and More Systems, Recklinghausen, Germany*
