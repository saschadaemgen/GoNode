# GoNode Legal Compliance

**Document version:** Season 1 | April 2026
**Component:** GoNode regulatory compliance and legal framework
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the legal and regulatory framework under which GoNode operates. It covers MiCA (EU Markets in Crypto-Assets Regulation), GDPR (General Data Protection Regulation), DSA (Digital Services Act), German Banking Act (KWG), German Money Laundering Act (GwG), EU Transfer of Funds Regulation (TFR), German tax law, and related compliance obligations.

GoNode is designed from day one to comply with all applicable regulations. The architecture choices, corporate structure, and economic design all incorporate compliance considerations. This document explains each compliance area, how GoNode addresses it, and the specific evidence of compliance.

**Disclaimer:** This document is not legal advice. It summarises our good-faith understanding of applicable regulations and the compliance approach. A formal Rechtsgutachten (legal opinion) from a qualified German law firm will be commissioned before TGE.

| Jurisdiction | Primary Applicability |
|:-------------|:----------------------|
| Switzerland | Foundation jurisdiction, token issuance |
| Germany | Development entity jurisdiction, primary operational base |
| European Union | MiCA, GDPR, DSA, TFR (cross-border) |
| International | Wherever node operators reside |

---

## 1. Entity structure

### 1.1 Two-entity design

GoNode operates through two legally separate entities with distinct roles:

```
+-------------------------------------------------------------+
|  GoNode Foundation (Swiss Stiftung)                         |
|  Jurisdiction: Switzerland (Zug)                            |
|  Legal form: Stiftung (foundation under Swiss Civil Code)   |
|                                                             |
|  Roles:                                                     |
|  - Protocol operation and governance                        |
|  - GoCoin token issuance                                    |
|  - Treasury management                                      |
|  - Grant funding administration                             |
|  - International relationships                              |
|  - Strategic direction                                      |
+-------------------------------------------------------------+
                         |
                  contractual relationship
                         |
                         v
+-------------------------------------------------------------+
|  IT and More Systems GmbH                                   |
|  Jurisdiction: Germany (Recklinghausen)                     |
|  Legal form: GmbH (limited liability company)               |
|                                                             |
|  Roles:                                                     |
|  - Software development and engineering                     |
|  - Publishing (GitHub repositories)                         |
|  - BaFin correspondence and German compliance              |
|  - Employment of German-based developers                    |
|  - Contract services to the Foundation                      |
+-------------------------------------------------------------+
```

### 1.2 Why two entities

**Swiss Stiftung for protocol operations:**

- Clear regulatory treatment of foundations under Swiss law
- Zug is the established crypto jurisdiction with banking access
- Swiss brand sells to enterprise customers internationally
- Strong constitutional protection of financial privacy (Swiss Federal Constitution Article 13)
- Proven template (Ethereum Foundation, Session Technology Foundation, Nym Technologies, Threema, Tor Project)
- Separation protects individual developers from protocol-level liability

**German GmbH for development:**

- Continues existing business operations without disruption
- German tax treatment for local development activities
- BaFin compliance counterparty in Germany
- Cultural and linguistic fit for German-based team
- Publishing entity for open-source repositories

### 1.3 Foundation governance

**Swiss Stiftung structure:**

| Role | Responsibility | Term |
|:-----|:--------------|:-----|
| Stiftungsrat (Board) | Strategic direction, major decisions | 3 years, renewable |
| Präsident | Day-to-day representation, signing authority | 3 years |
| Executive Director | Operations, team management | Indefinite |
| Beirat (Advisory Board) | Technical and legal guidance | 2 years |
| Revisor (Auditor) | Financial audit, compliance review | Annual |

**Founding Board composition (proposed):**

- 1 founder (Sascha Daemgen)
- 1 technical expert (cryptographer or systems engineer)
- 1 legal/regulatory expert (Swiss lawyer with crypto experience)
- 1 independent community representative
- 1 business/financial expert

### 1.4 Separation of duties

Critical operations require different entities or multiple parties to prevent single points of failure:

| Operation | Performed by | Signatures required |
|:----------|:-------------|:--------------------|
| Protocol deployment | Foundation | 3 of 5 multisig |
| Token transfers (treasury) | Foundation | 3 of 5 multisig, 24h timelock |
| Code commits | GmbH developers | PR review + 1 approval |
| BaFin submissions | GmbH | Authorised signatory |
| Smart contract upgrades | Foundation | Full timelock + DAO vote (post Phase 4) |
| Grant disbursement | Foundation | 2 of 5 signatures |

---

## 2. MiCA compliance

### 2.1 Regulatory background

**Regulation:** Regulation (EU) 2023/1114 (Markets in Crypto-Assets Regulation, "MiCA" or "MiCAR").

**Application timeline:**
- Titles III-IV (ART and EMT): applicable since 30 June 2024
- Titles II, V, VI, VII: applicable since 30 December 2024
- Full application: in effect

**Competent authorities:**
- EU-wide: European Securities and Markets Authority (ESMA)
- Germany: Bundesanstalt für Finanzdienstleistungsaufsicht (BaFin)
- Switzerland: FINMA (for Swiss-based issuers passporting into EU)

### 2.2 GoCoin classification

GoCoin qualifies as a utility token under MiCA Article 3(1)(9) ("other crypto-assets"). The classification is determined by the absence of specific features that would trigger more stringent regimes.

**Classification decision tree:**

| Criterion | MiCA Article | GoCoin Position |
|:----------|:-------------|:---------------|
| Pegged to single fiat currency? | Title IV (EMT) | No |
| Pegged to basket of fiat, commodities, crypto? | Title III (ART) | No |
| Redemption promise at par? | Title IV (EMT) | No |
| Represents ownership of other asset? | Title III (ART) | No |
| Financial instrument under MiFID II? | Out of MiCA scope | No |
| NFT (unique, non-fungible)? | Out of MiCA scope | No |
| Issued by public body? | Out of MiCA scope | No |
| **Classification** | **Art. 3(1)(9) "other crypto-assets"** | **Yes** |

This places GoCoin in the same category as Filecoin's FIL, Session's SESH, Arweave's AR, and Helium's HNT.

### 2.3 Title II whitepaper obligations

**Requirement:** Article 6-8 of MiCA require a crypto-asset whitepaper before public offer.

**Whitepaper structure** (Article 6 and Annex I):

| Part | Content | Status |
|:-----|:--------|:-------|
| A | Information about the issuer | Foundation details drafted |
| B | Information about the project | CONCEPT.md covers this |
| C | Rights and obligations attached to token | This document set |
| D | Information about technology | ARCHITECTURE_AND_SECURITY.md |
| E | Risks | Dedicated chapter in whitepaper |
| F | Information about the offer | Phase 3 specifics |
| G | Sustainability | Energy analysis (Arbitrum L2 is efficient) |

**Filing requirement:** Article 8 MiCA requires notification to the competent authority 20 business days before the public offer. For GoNode:

- **Competent authority:** BaFin (as GmbH is German-based, though Foundation is Swiss)
- **Notification method:** Electronic submission to BaFin
- **Contact:** whitepaper@bafin.de (for whitepaper notifications)
- **Timeline:** Filed at start of Phase 3 (approximately 15 months in)

**BaFin review:** BaFin does not "approve" whitepapers but can:
- Require changes if deficient
- Suspend or prohibit offers violating MiCA
- Impose administrative fines (up to 5% of annual turnover or 5M EUR)

### 2.4 Article 4(2) exemptions

MiCA Article 4(2) provides exemptions from whitepaper obligations for small offers. GoNode uses these during phases before TGE:

| Exemption | Threshold | GoNode Use |
|:----------|:----------|:-----------|
| Art. 4(2)(a) | < 150 persons per Member State | Phase 1 testnet (50 operators) |
| Art. 4(2)(b) | < 1,000,000 EUR over 12 months | Service Node Bonus Program (5M GC × 0.20 = 1M EUR) |
| Art. 4(2)(c) | Qualified investors only | Strategic round if needed |
| Art. 4(2)(d) | Offer solely to limited circle | Internal alpha testing |

**Important:** Exemptions apply per Member State. Multi-country Phase 1 and Phase 2 must track participant counts per country to stay within thresholds.

### 2.5 Title V (CASP) non-applicability

**Background:** Article 3(1)(16) MiCA defines Crypto-Asset Service Providers (CASPs). Title V requires CASP authorisation for persons providing listed services.

**CASP services (Article 3(1)(17-26)):**

- Custody and administration of crypto-assets
- Operation of a trading platform
- Exchange of crypto-assets for funds or other crypto-assets
- Execution of orders
- Placing of crypto-assets
- Reception and transmission of orders
- Providing advice on crypto-assets
- Providing portfolio management
- Providing transfer services

**GoNode Foundation's position:** Does not provide any of these services.

| CASP Service | GoNode Foundation | Rationale |
|:-------------|:------------------|:----------|
| Custody | No | User keys never touched by Foundation |
| Trading platform | No | Users trade on Uniswap, Binance, etc. directly |
| Exchange | No | Smart contract buys GoCoin from Uniswap; Foundation not counterparty |
| Order execution | No | No user orders handled |
| Placing | No | Self-service token distribution |
| Advice | No | Public documentation, not personalised advice |
| Portfolio management | No | Users manage own holdings |
| Transfer services | No | Users self-transfer via wallets |

**Result:** Foundation does not need CASP authorisation under Article 59.

**Node operators' position:** Individual node operators are not CASPs either. Running infrastructure for a decentralised network is not a CASP service per BaFin and ESMA guidance on decentralised protocols.

### 2.6 Article 2(3) / Recital 22 decentralisation exemption

**Provision:** MiCA Article 2(3) excludes from scope "crypto-assets that are unique and not fungible with other crypto-assets" AND, per Recital 22, services provided in a "fully decentralised manner without any intermediary".

**GoNode target state (post-Phase 4):**

- Deployer keys burned (no entity can modify smart contracts)
- DAO governance (all parameter changes via on-chain vote)
- Foundation operates at protocol level without special privileges
- No intermediary between users and smart contracts

**Phase-by-phase status:**

| Phase | Decentralisation Level | Recital 22 Exemption Available |
|:------|:----------------------|:-------------------------------|
| 0 (months 0-3) | Foundation-controlled | No |
| 1 (months 3-9) | Foundation-controlled | No |
| 2 (months 9-15) | Foundation-controlled | No |
| 3 (months 15-24) | Foundation + emerging DAO | Partial |
| 4 (months 24+) | Fully DAO | **Yes** |

**Conservative approach:** Even in Phase 4+, we will maintain MiCA compliance rather than rely on the exemption, because:
- Case law on "fully decentralised" is not yet established
- ESMA has indicated skepticism of early claims of decentralisation
- Conservative approach preserves enterprise customer confidence
- Cost of maintaining whitepaper compliance is low

---

## 3. German financial regulation

### 3.1 KWG (Kreditwesengesetz) - German Banking Act

**Key provisions:**

| Section | Content | GoNode Impact |
|:--------|:--------|:--------------|
| § 1 Abs. 11 S. 1 Nr. 10 | Definition of Kryptowerte | GoCoin qualifies as Kryptowert |
| § 1 Abs. 1a S. 2 Nr. 6 | Kryptoverwahrgeschäft (custody) | Does NOT apply (Foundation has no custody) |
| § 32 Abs. 1 | License requirement for banking/financial services | Does NOT apply (no banking or regulated services) |

**Kryptowerte classification:** Being a Kryptowert triggers certain reporting obligations but does not by itself require BaFin authorisation. Since MiCA took effect, KWG's crypto provisions are being progressively superseded or harmonised with MiCA.

**Grandfathering:** Germany's FinmadiG (Finanzmarktdigitalisierungsgesetz) provides grandfathering for pre-MiCA licensees until 30 December 2025. GoNode launches after this deadline, so applies directly under MiCA without grandfathering.

### 3.2 KMAG (Kryptomärkteaufsichtsgesetz)

**Background:** KMAG is Germany's implementing legislation for MiCA, embedded in the FinmadiG package. It designates BaFin as competent authority and specifies procedural rules for German entities under MiCA.

**Key provisions for GoNode:**

- BaFin has direct supervisory authority over crypto-asset offerings in Germany
- Administrative penalties up to 5% of group turnover
- Cross-border cooperation with other EU competent authorities via ESMA
- Whitepaper notifications to whitepaper@bafin.de

### 3.3 GwG (Geldwäschegesetz) - Money Laundering Act

**Applicability:** The GwG binds Verpflichtete (obligated entities) listed in § 2 GwG. Categories include banks, financial service providers, tax advisors, real estate agents, and crypto service providers.

**GoNode Foundation's position:** Not a Verpflichteter because:

- Does not provide crypto custody (no § 2 Abs. 1 Nr. 1e applicability)
- Does not operate as crypto exchange (no § 2 Abs. 1 Nr. 2a applicability)
- Is not a payment service provider (no § 2 Abs. 1 Nr. 1a applicability)
- Does not issue crypto-assets for third parties

**Operators' position:** Individual node operators are not Verpflichtete either. Running infrastructure is not a listed obligation-triggering activity.

**Result:** No KYC/AML obligations at the protocol level. Users acquire GoCoin from regulated CASPs (Uniswap via DEX, Binance via CEX), who handle their own Travel Rule compliance.

### 3.4 Transfer of Funds Regulation (TFR)

**Regulation:** Regulation (EU) 2023/1113 (recast of the Funds Transfer Regulation).

**Applicability:** Effective 30 December 2024. Requires crypto-asset service providers (CASPs) to transmit originator and beneficiary information with each transfer.

**GoNode position:** TFR binds CASPs, which GoNode Foundation is not (see Section 2.5). Therefore TFR does not directly apply to Foundation operations.

**Indirect compliance:** Exchanges where users acquire GoCoin (Binance, Kraken, etc.) implement Travel Rule compliance. Users transferring GoCoin between wallets are not subject to Travel Rule obligations.

### 3.5 KWG § 32 and license requirements

**Standard position:** Operating a decentralised node network is not a regulated activity under § 32 KWG requiring BaFin authorisation.

**Supporting rationale:**

- BaFin has published guidance that infrastructure provision for decentralised protocols is not financial service provision
- Analogous to internet service providers, who do not need banking licenses for routing encrypted traffic
- Smart contract operations are automated, not banking services
- No fiat payments are processed by the Foundation

---

## 4. GDPR (Data Protection)

### 4.1 Regulatory background

**Regulation:** Regulation (EU) 2016/679 (GDPR / DSGVO).

**Relevant guidance:**

- EDPB Guidelines 02/2025 on Processing of Personal Data Through Blockchain Technologies (adopted 8 April 2025)
- Article 29 Working Party legacy opinions
- BfDI (German Federal Commissioner for Data Protection) guidance on blockchain

### 4.2 What personal data is processed

GoNode's architecture is designed to minimise personal data processing:

| Data category | Processed? | Where | Retention |
|:--------------|:-----------|:------|:----------|
| Message content | Encrypted client-side | Ciphertext only on nodes | 30 days |
| User identifiers | No persistent IDs (SimpleX model) | N/A | N/A |
| IP addresses (user) | Transiently, via onion routing | First-hop node only | Not stored |
| IP addresses (operator) | Yes | Public in node directory | While operator active |
| Operator email | Yes | Foundation-managed | As long as operator active |
| Payment data (Pro) | EURC transactions on-chain | Arbitrum blockchain | Permanent (blockchain) |
| Subscription status | Pro expiry timestamp | Arbitrum blockchain | Permanent (blockchain) |

**Key property:** The Foundation and node operators cannot access message content. Messages are client-side encrypted with random AEAD keys. Even if compelled by law enforcement, the Foundation cannot produce message content.

### 4.3 Data controller determination

**EDPB Guidelines 02/2025 position:** In decentralised networks, data controllership is complex. The guidelines provide a framework:

| Role | Controller Status |
|:-----|:-----------------|
| User (sender of messages) | Controller for their own data |
| User (recipient) | Joint controller upon receipt |
| Node operator | Controller if involved in governance; processor if purely technical |
| GoNode Foundation | Joint controller (governance influence) |

### 4.4 Joint controllership agreement

**Requirement:** GDPR Article 26 requires joint controllers to determine their respective responsibilities.

**GoNode approach:** Foundation publishes a joint controllership agreement that:

- Designates Foundation as single point of contact for data subject requests
- Specifies node operators' responsibilities (provide uptime, respond to audit challenges)
- Allocates liability (Foundation covers protocol-level issues; operators cover local issues)
- Includes mandatory DPIA template for operators to adopt

**Template agreement:** Published in docs/legal/JOINT_CONTROLLER_AGREEMENT.md (planned for Phase 1).

### 4.5 Legal basis for processing

| Processing | Legal basis | Article |
|:-----------|:------------|:--------|
| Message delivery (encrypted) | Contract performance | Art. 6(1)(b) |
| Operator identification | Contract performance | Art. 6(1)(b) |
| Pro subscription payment | Contract performance | Art. 6(1)(b) |
| Audit response logs | Legitimate interest (network integrity) | Art. 6(1)(f) |
| Anti-abuse measures | Legitimate interest | Art. 6(1)(f) |

### 4.6 Data subject rights

GDPR Articles 15-22 grant various rights. GoNode's approach:

| Right | Article | Implementation |
|:------|:--------|:---------------|
| Access | 15 | Dashboard showing all data Foundation holds about user |
| Rectification | 16 | Edit profile, contact Foundation |
| Erasure (right to be forgotten) | 17 | Key destruction (see below) |
| Restriction | 18 | Flag subscription as restricted |
| Portability | 20 | Export Pro history and subscription data |
| Objection | 21 | Opt out of legitimate interest processing |

### 4.7 Right to erasure on blockchain

**Challenge:** Blockchain data is immutable. How to respect Article 17?

**EDPB Guidelines 02/2025 position:** For encrypted data, key destruction provides effective erasure. If no one holds the decryption key, the ciphertext is effectively anonymous data under Recital 26 GDPR.

**GoNode approach:**

```
User requests erasure:
  1. Foundation destroys all non-blockchain data (email, support tickets)
  2. User's encryption keys are destroyed client-side
  3. Ciphertext on blockchain becomes unrecoverable (effective erasure)
  4. Foundation provides confirmation document
  5. If user has active Pro subscription, it expires normally
```

For the on-chain Pro subscription status, which only records "address X is Pro until timestamp Y", this is considered non-personal data because:
- The address is pseudonymous
- The data reveals no substantive personal information
- The data is required for protocol function (cannot be removed without breaking smart contract)

### 4.8 International data transfers

**Issue:** Nodes may operate outside the EEA, creating international transfers under Chapter V GDPR.

**GoNode approach:**

- Foundation publishes Standard Contractual Clauses (SCCs) per EU Implementing Decision 2021/914
- Node operators agree to SCCs as part of joining the network
- Operators outside EEA identify their jurisdiction and applicable safeguards
- High-risk jurisdictions (per EDPB list) excluded from default swarm assignment

### 4.9 DPIA requirements

**Obligation:** Article 35 GDPR requires a Data Protection Impact Assessment for high-risk processing.

**Trigger criteria for GoNode:**
- Systematic and extensive processing? No (limited to technical operation)
- Large-scale processing of special categories? No (no sensitive data)
- Systematic monitoring? No (users are pseudonymous)
- Novel technologies? Yes (decentralised messaging infrastructure)

**Conclusion:** DPIA is advisable (not strictly required) due to novel technology. Foundation commissions full DPIA in Phase 1.

---

## 5. Digital Services Act (DSA)

### 5.1 Regulatory background

**Regulation:** Regulation (EU) 2022/2065 (Digital Services Act).

**Applicability:** Fully applicable since 17 February 2024.

**Relevance to GoNode:** GoNode service nodes qualify as intermediaries. Understanding their role under DSA determines liability and obligations.

### 5.2 Intermediary categorisation

DSA Chapter II defines three tiers of intermediary:

| Tier | Article | Activity | Liability |
|:-----|:--------|:---------|:----------|
| Mere conduit | Art. 4 | Transmits, routes, no storage beyond transmission need | Minimal liability |
| Caching | Art. 5 | Temporary storage for transmission efficiency | Minimal liability |
| Hosting | Art. 6 | Stores information at user's request | Conditional liability |

### 5.3 GoNode classification

GoNode nodes perform different functions depending on the operation:

| Operation | DSA Tier | Safe Harbour Available |
|:----------|:---------|:-----------------------|
| Onion routing (message forwarding) | Art. 4 (mere conduit) | Yes (unconditional) |
| Short-term message storage (30 days) | Art. 5 (caching) | Yes (conditional on standard requirements) |
| Long-term file storage | Art. 6 (hosting) | Yes (conditional on no actual knowledge) |

**The zero-knowledge architecture is critical here:** Hosting safe harbour under Art. 6(1) requires the operator to not have "actual knowledge" of illegal content. When operators cannot decrypt stored data, they technically cannot have actual knowledge of its content.

### 5.4 Notice-and-action obligations

**Requirement:** Art. 16 DSA requires hosting services to implement electronic notice-and-action mechanisms.

**GoNode implementation:**

```
Notice submission:
  URL: https://simplego.dev/dsa-notice
  Alternative: dsa@gonode.dev (email)
  Required fields:
    - Submitter's identity
    - Specific content complained of (encrypted reference)
    - Legal basis for claim
    - Statement of good faith

Processing:
  Day 0: Notice received, acknowledgement sent
  Day 1-7: Foundation reviews validity
  Day 7: Decision:
    (a) Valid, actionable: request content key revocation
    (b) Invalid/insufficient: inform submitter of decision
    (c) Requires more information: request clarification

Content removal method:
  - Foundation cannot decrypt, so cannot "delete content"
  - Instead, Foundation coordinates with user's client to revoke
    the relevant encryption key
  - After key revocation, ciphertext is computationally meaningless
  - Ciphertext eventually expires (30 days) from nodes
```

### 5.5 Art. 11 single point of contact

**Requirement:** Art. 11 DSA requires online services to designate a single point of contact for EU authorities.

**GoNode SPoC:**

- Email: authorities@gonode.dev
- Phone: +49 [number]
- Address: IT and More Systems GmbH, Recklinghausen, Germany
- Languages: English, German

### 5.6 Art. 12 legal representative

**Requirement:** Art. 12 DSA requires non-EU services to appoint a legal representative in the EU.

**GoNode approach:** IT and More Systems GmbH serves as the legal representative for the Swiss Foundation within the EU. This is analogous to how Matrix (UK Foundation) uses Element France as EU representative.

### 5.7 No general monitoring obligation

**Protection:** Art. 8 DSA preserves the no-general-monitoring principle from the old E-Commerce Directive.

**What this means:** Foundation is not obligated to:
- Monitor all messages for illegal content
- Decrypt user traffic for content analysis
- Implement upload filters
- Proactively identify illegal content

This is critical for GoNode's zero-knowledge design.

### 5.8 VLOP classification

**Requirement:** Very Large Online Platforms (VLOPs) have additional obligations under Arts. 33-43 DSA.

**Threshold:** 45 million average monthly active recipients in the EU.

**GoNode position:** Far below the VLOP threshold. Even at target growth (100k Pro subscribers + 10M free users in 5 years), well below 45M EU recipients. VLOP obligations do not apply.

### 5.9 Comparison with NetzDG

**Background:** Germany's Netzwerkdurchsetzungsgesetz (NetzDG) imposed notice-and-takedown obligations on social networks since 2017.

**Status:** Largely superseded by DSA since 17 February 2024. NetzDG procedures harmonised with DSA Art. 16.

**GoNode position:** DSA Art. 16 implementation (see Section 5.4) satisfies NetzDG requirements.

---

## 6. Tax compliance

### 6.1 German tax law

**Key provisions:**

| Section | Topic | GoNode Position |
|:--------|:------|:---------------|
| EStG § 15 | Income from trade (gewerblich) | Applies to commercial node operators |
| EStG § 22 Nr. 3 | Other income (sonstige Einkünfte) | Applies to hobbyist operators (< 256 EUR/yr Freigrenze) |
| EStG § 23 | Private speculative transactions (Spekulationsfrist) | 1-year holding period for GC |
| KStG § 1 | Corporate income tax | Applies to Foundation (if German resident) |
| GewStG | Trade tax | Applies to gewerbliche operators |

### 6.2 Node operator tax treatment

**BMF-Schreiben (Federal Ministry of Finance guidance):**

- BMF-Schreiben of 10 May 2022 (initial guidance)
- BMF-Schreiben of 6 March 2025 (supplementary guidance)

**Tax treatment:**

```
Hobbyist operator (< 256 EUR/yr, not profit-oriented):
  - Treated as § 22 Nr. 3 EStG (other income)
  - Freigrenze of 256 EUR per year
  - No trade registration (Gewerbeanmeldung) needed
  - No GewSt

Commercial operator (continuous, profit-oriented):
  - Treated as § 15 EStG (gewerbliche Einkünfte)
  - Gewerbeanmeldung required
  - Subject to GewSt
  - Must keep proper books (FIFO or similar)

All operators:
  - Receipt of reward: income at market value at receipt
  - Holding period starts at receipt
  - Sale before 1 year: Spekulationsgewinn/verlust per § 23 EStG
  - Sale after 1 year: tax-free
```

**Foundation recommendation:** Full-time operators should register Gewerbe and maintain proper records. Foundation publishes template bookkeeping guidance.

### 6.3 VAT (Umsatzsteuer)

**CJEU Hedqvist ruling (C-264/14, 22 October 2015):** Fiat-to-crypto exchange is VAT-exempt as currency transaction under Art. 135(1)(e) VAT Directive.

**GoNode implications:**

| Transaction | VAT Status |
|:------------|:-----------|
| User exchanges EUR for EURC | Exempt (Hedqvist) |
| User pays EURC for Pro subscription | **VAT applicable** (service provided by Foundation) |
| Operator receives GoCoin reward | Out-of-scope (no identifiable recipient; no service) |
| Operator sells GoCoin on exchange | Exempt (Hedqvist) |

**Pro subscription VAT:**

- Foundation must charge VAT on Pro subscriptions to EU consumers
- EU consumer: destination-country VAT rate (up to 25% in Hungary, 19% in Germany, etc.)
- Business customer: reverse charge mechanism
- Mini One-Stop Shop (MOSS) registration for cross-border EU sales

### 6.4 Foundation tax treatment

**Swiss taxation:** Swiss Stiftung typically exempt from federal corporate income tax if public-interest status granted by cantonal authority.

**Zug canton:** Pro-crypto jurisdiction with favorable foundation treatment.

**German source income:** If GmbH generates profits from services to Swiss Foundation, these are taxed in Germany. Arms-length pricing required.

---

## 7. Criminal law considerations

### 7.1 Developer liability precedents

Recent cases have shaped developer liability in crypto:

| Case | Outcome | Relevance to GoNode |
|:-----|:--------|:--------------------|
| Alexey Pertsev (Tornado Cash) | Convicted May 2024 in Netherlands, 5 years 4 months for money laundering | Pertsev retained admin keys, operated service, received fees |
| Roman Storm (Tornado Cash) | Convicted August 2025 SDNY for operating unlicensed money transmitter | Similar pattern - retained control |
| Keonne Rodriguez + William Hill (Samourai Wallet) | Pleaded guilty July 2025, operating unlicensed money transmitter | Custody component, fee extraction |
| Roman Sterlingov (Bitcoin Fog) | Convicted 2024 for operating unlicensed mixer | Operated service, retained fees |
| Larry Harmon (Helix) | Pleaded guilty 2020 for operating unlicensed mixer | Same pattern |

### 7.2 Through-line: what gets developers prosecuted

**Common elements in convictions:**

- Developer retained admin/upgrade keys after launch
- Developer received fees from protocol operation
- Developer continued active involvement after users began using for illegal purposes
- Custody or exchange-like functionality
- Marketing that emphasised anonymity for illegal use

**GoNode's protection strategy:**

| Risk Factor | GoNode Mitigation |
|:------------|:------------------|
| Admin key retention | Deployer keys burned at Phase 4 |
| Fee extraction | All fees flow to operators or are burned; Foundation collects grants and enterprise contracts only |
| Custody | Never takes custody |
| Exchange functionality | Never provides; users use third-party exchanges |
| Anonymity marketing | Marketing focuses on privacy, not anonymity for illegal use |
| Active involvement in illegal use | Clear terms of service prohibit illegal use; Foundation coordinates takedowns |

### 7.3 Relevant German criminal law

| Section | Offense | Relevance |
|:--------|:--------|:----------|
| StGB § 261 | Geldwäsche (money laundering) | Infrastructure provision not typically criminal |
| StGB § 263 | Betrug (fraud) | Not applicable (no deception) |
| StGB § 202a | Ausspähen von Daten | Not applicable (no unauthorized access) |
| TKG § 88 | Fernmeldegeheimnis (telecom secrecy) | PROTECTS GoNode operations |

### 7.4 Constitutional protections

**Grundgesetz Article 10:** Fernmeldegeheimnis (telecommunications secrecy).

**BVerfGE 125, 260 (Vorratsdatenspeicherung):** Extended Art. 10 protection to internet traffic. GoNode's encrypted messaging falls within this constitutional protection.

**TKG § 88:** Statutory implementation. Provides additional legal basis for encrypted communications.

**Practical effect:** GoNode enjoys constitutional-level protection against compelled decryption or mass surveillance requirements in Germany.

### 7.5 Chat Control (EU CSAM Scanning Regulation)

**Status as of April 2026:** The proposed EU Child Sexual Abuse Regulation (COM(2022) 209, "Chat Control") remains blocked in Council. Germany among consistent opponents due to its breaking of end-to-end encryption.

**GoNode position:** Not immediately affected. Tracks developments closely. Would resist implementation of scanning mandates as incompatible with architecture.

---

## 8. Open-source licensing

### 8.1 AGPL-3.0

**License:** GNU Affero General Public License v3.0 (SimpleX Chat's own license).

**Key provisions:**

| Provision | Effect |
|:----------|:-------|
| Article 6 | Source code must be provided with distributed binaries |
| Article 11 | Royalty-free patent grant from all contributors |
| Article 13 | Network use triggers source code availability obligation |

### 8.2 Patent considerations

**AGPL Article 11** provides a patent grant from every contributor covering their contribution. This protects downstream users from patent lawsuits by contributors.

**GoNode patent strategy:**

- No patent applications filed by Foundation
- Contributor License Agreement (CLA) confirms patent grant under AGPL-3.0
- No proprietary dependencies that could block open-source distribution

### 8.3 Contributor License Agreement

**Purpose:** Ensure all contributions can be licensed under AGPL-3.0 and that contributors grant necessary rights.

**Template:**

```
By submitting a contribution, I certify that:
1. I have the right to make this contribution
2. I license this contribution under AGPL-3.0
3. I grant a patent license per AGPL-3.0 Article 11
4. The contribution does not violate third-party rights
5. The contribution is original or properly attributed
```

Implemented via DCO (Developer Certificate of Origin) sign-off on every commit:

```
Signed-off-by: Alice Developer <alice@example.com>
```

### 8.4 Third-party licensing

All dependencies must be compatible with AGPL-3.0. GoNode's dependency list is audited for compatibility:

| Dependency | License | AGPL-3.0 Compatible |
|:-----------|:--------|:-------------------|
| Go standard library | BSD-3 | Yes |
| BadgerDB | Apache-2.0 | Yes |
| libsodium | ISC | Yes |
| klauspost/reedsolomon | MIT | Yes |
| ethereum/go-ethereum | LGPL-3.0 + GPL-3.0 | Yes |
| tendermint/tendermint | Apache-2.0 | Yes |

---

## 9. Compliance program

### 9.1 Pre-launch activities

**Phase 0 (months 0-3):**

- Foundation incorporation (Zug)
- GmbH scope update for GoNode activities
- Rechtsgutachten from qualified German law firm
- AGPL/CLA implementation
- Initial compliance documentation

**Phase 1 (months 3-9):**

- DPIA completion
- Joint Controller Agreement draft
- Standard Contractual Clauses for non-EEA operators
- MiCA whitepaper draft
- DSA notice-and-action system

**Phase 2 (months 9-15):**

- Legal review of all documentation
- Security audits (smart contracts)
- MiCA whitepaper filing with BaFin
- Final Rechtsgutachten
- Trademark registration (GoCoin, GoNode)

### 9.2 Ongoing compliance

**Monthly:**
- Transaction monitoring (for unusual patterns)
- Security incident review
- Community moderation reports

**Quarterly:**
- Internal compliance audit
- Risk assessment update
- Documentation review

**Annually:**
- External compliance audit
- Rechtsgutachten refresh
- Penetration testing
- DPIA review

### 9.3 Incident response

**Security incidents:**
- Initial detection: automated monitoring alerts
- Triage: within 1 hour
- Disclosure to stakeholders: per severity matrix
- Coordinated response: Foundation + GmbH + legal counsel

**Data breaches:**
- Identification: within 24 hours
- Supervisory authority notification: within 72 hours (GDPR Art. 33)
- Data subject notification: without undue delay (GDPR Art. 34)
- Post-incident review: within 30 days

**Regulatory inquiries:**
- Acknowledgment: within 48 hours
- Substantive response: per deadline (typically 4-8 weeks)
- Legal counsel involvement: mandatory for significant inquiries

---

## 10. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [GoNode Architecture](ARCHITECTURE_AND_SECURITY.md) | Technical implementation of compliance | This repo |
| [GoNode Tokenomics](TOKENOMICS.md) | Token classification basis | This repo |
| [GoNode Business Model](BUSINESS_MODEL.md) | Revenue structure and tax treatment | This repo |
| [Security Policy](../SECURITY.md) | Vulnerability disclosure process | This repo |
| [GoUNITY Architecture](https://github.com/saschadaemgen/GoUNITY/blob/main/docs/ARCHITECTURE_AND_SECURITY.md) | User identity layer (separate controller) | GoUNITY repo |

---

*GoNode Legal Compliance v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
