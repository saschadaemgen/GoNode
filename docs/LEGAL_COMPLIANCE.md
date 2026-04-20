# GoNode Legal Compliance

**Document version:** Season 1 | April 2026
**Component:** GoNode regulatory compliance and legal framework
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the legal and regulatory framework under which GoNode operates. It covers the primary legal basis for the GoCoin loyalty system (PSD2 limited network exemption, German ZAG, BGB), the peer-to-peer marketplace requirements under the EU Digital Services Act (DSA), GDPR compliance, German tax law, German criminal law considerations, and related compliance obligations.

GoNode is designed from day one to comply with all applicable regulations. The architecture choices, corporate structure, and loyalty system design all incorporate compliance considerations. This document explains each compliance area, how GoNode addresses it, and the specific evidence of compliance.

**Important redesign notice:** Following internal review in April 2026, the GoCoin design was fundamentally changed from a crypto-asset model (MiCA Art. 3(1)(9) utility token) to a closed-loop loyalty rewards system (PSD2 Art. 3(k) / ZAG § 2 limited network exemption). This document reflects the redesigned model. The earlier crypto-token approach has been superseded.

**Disclaimer:** This document is not legal advice. It summarises our good-faith understanding of applicable regulations and the compliance approach. A formal Rechtsgutachten (legal opinion) from a qualified German law firm will be commissioned before public launch of the GoCoin loyalty system.

| Jurisdiction | Primary Applicability |
|:-------------|:----------------------|
| Germany | Primary operational base, loyalty program issuance |
| European Union | PSD2, DSA, GDPR, E-Money Directive, Consumer Rights |
| Switzerland | Foundation jurisdiction (if Swiss Stiftung chosen) |

---

## 1. Entity structure

### 1.1 Two-entity design (unchanged from earlier version)

GoNode operates through two legally separate entities with distinct roles:

```
+-------------------------------------------------------------+
|  GoNode Foundation (Swiss Stiftung or German Stiftung)      |
|                                                             |
|  Roles:                                                     |
|  - Protocol operation and governance                        |
|  - GoCoin loyalty program issuance                          |
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
|  - GoCoin loyalty program operational administration        |
+-------------------------------------------------------------+
```

### 1.2 Foundation domicile (Swiss vs German)

The earlier plan assumed Swiss Stiftung for protocol operations. With the redesign to a loyalty system, the case for Swiss domicile is weaker and a German Stiftung or gGmbH may be more appropriate:

| Factor | Swiss Stiftung | German Stiftung |
|:-------|:---------------|:----------------|
| Setup cost | 50-80k CHF | 15-25k EUR |
| Minimum capital | 50k CHF | 10-50k EUR |
| Regulatory clarity | Good (FINMA) | Excellent (well-established) |
| Tax treatment | Favourable | Good (subject to Gemeinnützigkeit status) |
| Grant eligibility (EU) | Limited | Full |
| Operational synergy with GmbH | Lower | Higher |
| Relevance post-redesign | Reduced | Increased |

**Recommendation:** Evaluate German Stiftung option given that MiCA and crypto-specific considerations no longer drive the choice. Final decision deferred to Phase 1 after legal opinion.

### 1.3 Operational separation of duties

Critical operations require different entities or multiple parties:

| Operation | Performed by | Authorisation required |
|:----------|:-------------|:-----------------------|
| GoCoin issuance (purchase rewards) | GmbH automated system | Standard business operation |
| GoCoin issuance (operator rewards) | GmbH automated system | Monthly reconciliation |
| GoCoin issuance (community rewards) | Foundation discretion | Foundation board approval |
| Burn/reclamation operations | Foundation | Board approval, audit trail |
| Marketplace fee collection | GmbH | Standard business operation |
| Code commits | GmbH developers | PR review + 1 approval |
| Reserve coin movement | Foundation | Multi-party approval |

---

## 2. GoCoin legal classification

### 2.1 Primary classification: Limited network exemption

GoCoin is designed as a **closed-loop loyalty point** under the limited network exemption. This is the same legal basis that covers Payback, Miles & More, Deutsche Bahn BahnBonus, Steam Wallet, and most German/EU loyalty programs.

**Primary legal basis:**

- **Article 3(k) Payment Services Directive 2 (Directive (EU) 2015/2366)** - exemption for "payment transactions based on payment instruments that can be used... to acquire a very limited range of goods or services, or... within the premises of the issuer or under a commercial agreement with the issuer, either within a limited network of service providers"

- **§ 2 Absatz 1 Nummer 10 Zahlungsdiensteaufsichtsgesetz (ZAG)** - German implementation. Exempts instruments used only within a limited network of service providers or for a limited range of goods/services.

- **Recital 14 Electronic Money Directive (2009/110/EC)** - closed-loop schemes where electronic money is issued for a specific purpose within a limited network are generally outside e-money regulation scope.

### 2.2 Why GoCoin qualifies for the exemption

The limited network exemption applies because GoCoin satisfies these criteria:

| Criterion | GoCoin status | Evidence |
|:----------|:-------------|:---------|
| Issued by single entity | Yes | Only IT and More Systems GmbH issues GoCoin |
| Limited range of goods/services | Yes | Only SimpleGo ecosystem goods |
| Not generally accepted as payment | Yes | Cannot be used outside the ecosystem |
| No redemption in money | Yes | Foundation never buys coins back for EUR |
| No external trading venues | Yes | No DEX, no CEX, no public market |
| Commercial agreement with issuer | Yes | Terms of Service defines acceptance |

### 2.3 ZAG thresholds

German law (§ 2 Abs. 1 Nr. 10 ZAG) places certain reporting obligations on limited network instruments exceeding thresholds:

| Threshold | Obligation |
|:----------|:-----------|
| Under 1 million EUR annual transaction volume | No specific reporting |
| 1-5 million EUR annual volume | Notification to BaFin recommended |
| Over 5 million EUR annual volume | Formal notification to BaFin required |
| Over 2 million EUR with significant general use | May lose exemption, require regulation |

**GoNode approach:** File voluntary notification to BaFin once transaction volume approaches 1 million EUR, proactively establish compliance posture with the regulator before it becomes mandatory.

### 2.4 What GoCoin is NOT under various regimes

GoCoin's classification under various regulatory regimes:

| Regulation | Classification | Why |
|:-----------|:--------------|:----|
| MiCA (EU 2023/1114) | Not a crypto-asset | No DLT tradability, no public markets, closed-loop |
| E-Money Directive (2009/110/EC) | Not e-money | Not redeemable in cash, limited network exemption applies |
| PSD2 (2015/2366) | Not a payment service | Art. 3(k) limited network exemption |
| MiFID II | Not a financial instrument | No investment character, no profit participation |
| KAGB | Not a fund unit | No pooled investment |
| ZAG | Not a payment instrument | § 2 Abs. 1 Nr. 10 exemption |
| KWG | Not banking/financial service | No lending, deposit-taking, or trading |
| WpHG | Not a security | No securities characteristics |
| Prospectus Regulation | No prospectus needed | Not offered as investment |

### 2.5 Regulatory precedent

German and EU regulators have consistently treated loyalty points as outside the scope of financial regulation:

**BaFin guidance on customer loyalty programs:** BaFin has historically confirmed that loyalty programs operating within a limited network (single issuer, limited acceptance) are not subject to ZAG, ZAG licensing, or prudential supervision. Examples confirmed in informal guidance:

- Payback (30+ million users)
- Miles & More (36+ million members)
- Deutsche Bahn BahnBonus
- Deutsche Telekom Magenta Moments
- Various supermarket and retail loyalty programs

**EU regulatory approach:** The European Banking Authority (EBA) and European Commission have published guidance confirming that limited network instruments remain outside PSD2 scope when they satisfy the Art. 3(k) criteria.

**Case law:** No German or EU court has reclassified a limited-network loyalty program as e-money or payment service when properly structured. The legal territory is well-established.

---

## 3. GoCoin issuance legal basis

### 3.1 Purchase rewards as Rabatt/Bonus

When users earn GoCoin as a bonus on EUR purchases, the legal characterisation is:

**Rabattgewährung (rebate):** The GoCoin bonus is a form of rebate on the purchase, reducing the effective price paid by the customer. Rebates are standard commercial practice and do not trigger financial regulation.

**Legal basis:**

- § 312a BGB (general consumer protection for distance contracts)
- § 1 PreisangabenVerordnung (price transparency requirements)
- § 7 UWG (unfair competition - rebates must be genuine, not misleading)

**Tax basis:**

- BMF-Schreiben on loyalty programs (10 December 2015) - rebates are generally not taxable income for the consumer
- § 3 Nr. 11 EStG considerations for employer-related bonuses (not applicable here)

**Commercial basis:**

- GTCs clearly disclose the bonus rate before purchase
- Bonus is automatically awarded, no separate contract needed
- User can refuse the bonus (opt out of loyalty program)

### 3.2 Operator rewards as service compensation

Node operator rewards have a different legal character:

**Service compensation:** Operators provide computing services to the network. The GoCoin reward is payment for that service. The legal character is Dienstleistungsvergütung (service payment).

**Legal basis:**

- § 611 BGB (service contract) or § 631 BGB (work contract) depending on structure
- Terms of Service define the contractual relationship
- Automatic calculation based on measurable service parameters (uptime, audit response)

**Tax consequences:**

- Taxable income for operators (see section 8)
- Foundation provides annual statements for tax reporting
- DAC7 reporting may apply above thresholds

### 3.3 Community rewards as discretionary gifts

Community contribution rewards are discretionary grants:

**Legal character:** Schenkung unter Auflage (gift subject to conditions) or zweckgebundene Zuwendung (purpose-tied grant).

**Tax consequences:**

- Generally taxable for recipient under § 22 Nr. 3 EStG
- Small amounts (under 256 EUR/year) may fall under Freibetrag
- Foundation issues statements if over threshold

---

## 4. Peer-to-peer marketplace compliance (DSA)

### 4.1 Regulatory background

The GoNode marketplace enables users to trade GoCoin and ecosystem items between each other. This makes GoNode an "online marketplace" for DSA purposes, triggering specific obligations.

**Regulation:** Digital Services Act (Regulation (EU) 2022/2065).

**Applicability:** Fully applicable since 17 February 2024.

**GoNode's classification under DSA:**

- **Not a mere conduit** - we process transactions
- **Not pure caching** - we store user listings
- **Hosting service** under Art. 6 - users post content (listings), we host it
- **Online platform** under Art. 3(i) - we enable user-to-user transactions
- **Online marketplace** under Art. 6(c) - we facilitate consumer-to-consumer trades
- **NOT a VLOP** - below 45M EU users threshold

### 4.2 Key DSA obligations for the marketplace

**Article 14 (terms and conditions):**

- Clear, easily accessible terms of service
- Language requirements (German for Germany, local languages where relevant)
- Specific information about content moderation policies
- Annual reports on content moderation (when user base grows)

**Article 16 (notice-and-action mechanism):**

Users can report illegal content/listings through:

- In-app reporting button on every listing
- Web form at marketplace.gonode.dev/report
- Email: notice@gonode.dev

Process:

```
Notice received
  |
  v
Acknowledgment (within 24 hours)
  |
  v
Review by moderation team (within 7 days)
  |
  +-> Valid: take action (remove listing, notify user)
  |
  +-> Invalid: inform reporter, explain reasoning
  |
  +-> Requires more info: request clarification
```

**Article 20 (internal complaint-handling system):**

Users affected by moderation decisions can appeal:

- Online system for submitting appeals
- 6-month window after moderation decision
- Free of charge for users
- Final decision within 14 days

**Article 23 (measures against misuse):**

- Warnings and temporary suspensions for abusive behaviour
- Permanent bans for repeated violations
- Specific measures for counterfeit goods (not applicable to loyalty points)

**Article 27 (recommender system transparency):**

If we use algorithmic ranking in the marketplace, main parameters must be disclosed in the ToS.

**Article 30 (traceability of traders):**

**Critical decision:** Are users on our marketplace "traders" (commercial users) or "consumers"?

- **Consumer-to-consumer (C2C):** Users trading their own earned coins/items. Art. 30 does not apply.
- **Business-to-consumer (B2C):** If some users trade commercially, traceability obligations apply.

**GoNode design:** We explicitly design the marketplace for C2C trading. Commercial use is discouraged through Terms of Service. This keeps us outside Art. 30 obligations, at least initially.

**Article 31 (compliance by design):**

If B2C trading becomes relevant, we implement:

- Trader identification verification
- Self-declaration interface
- Monitoring for commercial patterns

**Article 32 (obligation to inform consumers):**

When illegal listings are found, affected users who purchased/bid are notified.

### 4.3 Single point of contact (Art. 11 DSA)

GoNode designates a single point of contact for EU authorities:

- Email: authorities@gonode.dev
- Phone: [to be published with Foundation details]
- Address: IT and More Systems GmbH, Recklinghausen, Germany
- Languages: English, German

### 4.4 Legal representative (Art. 12 DSA)

IT and More Systems GmbH serves as legal representative in the EU for Foundation activities. Already established.

---

## 5. GDPR compliance

### 5.1 Personal data categories

The loyalty system processes:

| Data category | Purpose | Legal basis |
|:--------------|:--------|:------------|
| Account data (email, username) | Authentication | Contract (Art. 6(1)(b)) |
| Purchase history | Reward calculation | Contract (Art. 6(1)(b)) |
| GoCoin balance | Account management | Contract (Art. 6(1)(b)) |
| Marketplace listings | Platform operation | Contract (Art. 6(1)(b)) |
| Marketplace transactions | Trade execution | Contract (Art. 6(1)(b)) |
| Node operator data | Reward calculation | Contract (Art. 6(1)(b)) |
| Audit logs | Security, fraud prevention | Legitimate interest (Art. 6(1)(f)) |
| Tax data | DAC7 reporting | Legal obligation (Art. 6(1)(c)) |

### 5.2 Data subject rights

Standard GDPR rights fully implemented:

| Right | Article | Implementation |
|:------|:--------|:--------------|
| Information | 13, 14 | Privacy notice at signup |
| Access | 15 | Account settings export |
| Rectification | 16 | Profile editing |
| Erasure | 17 | Account deletion (with retention exceptions) |
| Restriction | 18 | Flag account |
| Portability | 20 | JSON export of data |
| Objection | 21 | Opt-out of optional processing |

### 5.3 Right to erasure considerations

The loyalty system design supports GDPR Art. 17 (right to be forgotten):

**Database-based ledger:**

- Account and balance data deletable on request
- Retention exceptions for legal obligations (tax records for 10 years)
- Transaction history can be pseudonymised

**Permissioned blockchain (future):**

- Immutable by design - direct deletion impossible
- Pseudonymisation at onboarding
- EDPB Guidelines 02/2025 compliance: key destruction + offchain anchoring

The database option is preferred partly because GDPR compliance is simpler.

### 5.4 International transfers

If marketplace allows EU-to-non-EU trades, Standard Contractual Clauses (SCCs) apply. Initial launch is EU-only to avoid this complexity.

### 5.5 DPIA (Article 35)

Data Protection Impact Assessment required because:

- Systematic processing of user data
- Novel technology (marketplace for digital items)
- Potentially high-risk for user rights

DPIA commissioned in Phase 1, before marketplace public launch.

---

## 6. Taxation

### 6.1 User taxation - purchase rewards

GoCoin earned as purchase bonus:

- **Generally tax-free** under established German loyalty program precedent
- Treated as a rebate (Rabatt) reducing the effective purchase price
- No 1099-equivalent reporting required in Germany
- Reference: BMF-Schreiben 10 December 2015 on loyalty programs

**Exception:** If purchase is business-related (company paying for employee tools), company accounting treatment applies.

### 6.2 Operator taxation

Node operators receive taxable income:

**Classification options:**

- **§ 22 Nr. 3 EStG (Sonstige Einkünfte):** Small operators, casual activity, under 256 EUR annual Freigrenze
- **§ 15 EStG (Gewerbliche Einkünfte):** Regular commercial operation, requires Gewerbeanmeldung
- **Hobby-Einkünfte:** Very minor, no reporting needed

**Valuation for tax purposes:**

The GoCoin reward is valued at its **redemption value** at the time of receipt. Example: if 100 GoCoin redeems for 100 EUR of ecosystem goods when received, the operator's taxable income is 100 EUR.

**Reporting:** Foundation provides annual statements (January of following year) showing:

- Total GoCoin earned
- Monthly breakdown
- EUR equivalent valuation
- Suggested tax classification

**DAC7:** Platform operator reporting requirement to tax authorities. Applies when:

- Operator earns over 2,000 EUR equivalent/year, OR
- Operator conducts over 30 transactions/year

Foundation implements DAC7-compliant reporting.

### 6.3 Marketplace trade taxation

When users trade GoCoin and ecosystem items between each other:

**Private sales (§ 23 EStG):**

- Gains may be tax-free if items held longer than 1 year
- Freibetrag of 600 EUR/year for total private sales gains
- Losses can offset gains in same year

**Commercial trading:**

- Regular pattern of trading = Gewerbliche Tätigkeit
- Requires Gewerbeanmeldung
- Subject to full income tax and Gewerbesteuer

**Foundation reporting (DAC7):**

- Transactions over 2,000 EUR equivalent require user verification and reporting
- High-volume users tracked per DAC7 requirements

### 6.4 VAT treatment

**Umsatzsteuer (VAT) application:**

| Transaction | VAT status |
|:-----------|:-----------|
| User purchase with EUR | Full VAT (19% standard) |
| GoCoin as purchase bonus | Not separately taxed |
| Operator receives GoCoin rewards | Outside VAT scope (no identifiable recipient at issuance) |
| User redeems GoCoin for goods | VAT applies at redemption point |
| Marketplace trades user-to-user | Typically outside VAT for private users |
| Marketplace fees | Foundation fee income, VAT applies above thresholds |

**CJEU Hedqvist (C-264/14):** Relevant for potential future euro conversions, but not applicable to closed-loop loyalty points.

### 6.5 Foundation tax treatment

**If Swiss Stiftung:**

- Cantonal tax exemption possible if public-interest status granted
- Subject to Swiss regulatory framework
- International recognition of tax-exempt status

**If German gemeinnützige Stiftung:**

- Körperschaftsteuer exemption under § 5 Abs. 1 Nr. 9 KStG
- Gewerbesteuer exemption under § 3 Nr. 6 GewStG
- Requires clear Gemeinwohl purpose in Stiftungssatzung

**GmbH:**

- Standard corporate taxation
- Services to Foundation must be at arm's length pricing
- German Körperschaftsteuer (15%) + Solidaritätszuschlag + Gewerbesteuer

---

## 7. Consumer protection

### 7.1 Applicable regulations

| Regulation | Applicability |
|:-----------|:--------------|
| EU Consumer Rights Directive (2011/83/EU) | Yes - online sales, digital content |
| Digitale-Inhalte-Richtlinie (EU 2019/770) | Yes - digital content delivery |
| BGB §§ 312-312k | Yes - distance contracts, digital content |
| PreisangabenVerordnung (PAngV) | Yes - price transparency |
| UWG (Unfair Competition) | Yes - marketing practices |

### 7.2 Withdrawal right

Users generally have 14-day withdrawal right for:

- Pro subscriptions purchased online
- Hardware devices
- Digital content (with exceptions per § 356 BGB)

**GoCoin specific:**

- Purchased directly with EUR: 14-day withdrawal applies to the underlying purchase (e.g., Pro subscription)
- Earned as bonus on EUR purchase: GoCoin bonus follows underlying purchase - if user withdraws purchase, bonus is reversed
- Redemption of GoCoin: immediate execution, user acknowledges no withdrawal right (per § 356 Abs. 5 BGB for digital content)
- Marketplace trades: immediate execution, no withdrawal right between private users

### 7.3 Guarantee and warranty

| Item | Guarantee |
|:-----|:----------|
| EUR-purchased digital subscriptions | 2-year legal warranty (Gewährleistung) |
| EUR-purchased hardware | 2-year legal warranty + possibly manufacturer guarantee |
| GoCoin balance | Loyalty program Terms of Service commitments |
| Redeemed items | Standard product warranty |
| Marketplace trades user-to-user | No Foundation warranty - disputes between parties |

### 7.4 Clear Terms of Service

Required ToS elements for EU consumer protection:

- Clear identification of provider (Impressum)
- Complete description of loyalty program rules
- Unambiguous statement of non-monetary nature of GoCoin
- Fair changes-to-terms procedure (6+ months notice for material changes)
- Account termination procedures protecting accumulated value
- Dispute resolution mechanisms
- Jurisdiction and applicable law

---

## 8. Anti-money laundering

### 8.1 GwG applicability

German Geldwäschegesetz (GwG) applies to specific obligated entities (Verpflichtete). GoNode's position:

**GoCoin loyalty system:** Not AML-obligated because:

- Not redeemable in cash (key criterion for GwG exemption)
- Limited network instrument
- No cross-currency transactions
- Not a financial service provider under GwG § 2

**Marketplace operator:** May have obligations for high-volume or unusual activity:

- § 261 StGB (money laundering) applies to everyone
- Reporting suspicious activity to FIU (Financial Intelligence Unit)
- Customer due diligence for high-value trades (though not formally required for closed-loop)

### 8.2 Abuse monitoring

Even without formal GwG obligations, GoNode implements abuse monitoring:

| Trigger | Action |
|:--------|:-------|
| Unusual trading patterns | Automated flag, manual review |
| Rapid coin accumulation + offloading | Enhanced monitoring |
| Multiple accounts same identity | Investigation |
| Large value peer transfers | Verification request |
| DAC7 threshold exceeded | Reporting triggered |

### 8.3 KYC approach

**Standard user:** Email verification only (appropriate for loyalty program)

**Elevated activity:** Enhanced verification if:

- Marketplace transactions exceed 1,000 EUR equivalent per year
- Node operator earning significant rewards
- Commercial pattern detected

**Hardware-bound accounts (GoKey):** Already hardware-verified, lower monitoring burden.

---

## 9. Platform liability

### 9.1 Hosting provider protection

As a hosting provider under DSA Art. 6:

- Not liable for user-generated content until actual knowledge of illegality
- Prompt action on notice (per Art. 16)
- No general monitoring obligation (Art. 8)

### 9.2 Marketplace-specific liability

For peer-to-peer trades:

- Foundation not party to the trade
- No implied warranty on traded items
- Dispute resolution provided as service, not guarantee
- Clear ToS disclaiming trade warranties

### 9.3 Payment processing liability

For EUR purchases that generate GoCoin bonuses:

- Standard payment service provider (Stripe, etc.) handles payments
- GoNode not a payment service provider itself
- Refunds/chargebacks handled by payment processor
- GoCoin bonus reversal follows underlying purchase

### 9.4 Insolvency protection

If the Foundation or GmbH becomes insolvent:

- User GoCoin balances: Foundation commitment, may lose value in insolvency
- EUR-purchased subscriptions: Standard insolvency treatment
- Hardware orders: Consumer protection per German InsO

**Mitigation:**

- Foundation maintains reserve funds
- Clear ToS on insolvency treatment
- Option to redeem coins promptly to hedge risk
- No pooled customer EUR (payments flow immediately to operational accounts)

---

## 10. Intellectual property

### 10.1 Open source licensing

All GoNode software is licensed under AGPL-3.0:

- Source code freely available
- Derivatives must remain AGPL-3.0
- Network use triggers disclosure obligations
- Patent grant from contributors

### 10.2 Trademarks

Planned trademark registrations:

- GoNode (word mark) - EU and international classes
- GoCoin (word mark) - EU classes for loyalty programs
- SimpleGo ecosystem marks
- Logo marks as developed

### 10.3 User-generated content

User listings on marketplace remain user property:

- ToS grants platform license to display
- No ownership transfer to Foundation
- Removal on user request (with limited exceptions)

---

## 11. Criminal law considerations

### 11.1 Developer liability (lessons from Tornado Cash)

Recent crypto-related prosecutions (Alexey Pertsev, Roman Storm, Samourai Wallet founders) established patterns of developer liability. The common factors:

- Retained admin/upgrade keys after launch
- Received fees from protocol operation
- Continued active involvement as illegal use occurred
- Custody or exchange-like functionality
- Marketing emphasising anonymity for illegal use

**GoNode's protection strategy (adapted for loyalty system):**

| Risk Factor | GoNode Mitigation |
|:------------|:------------------|
| Admin key retention | Not applicable - no smart contracts, database-based |
| Fee extraction | Marketplace fees burned, not retained by Foundation |
| Custody | Foundation holds no user money |
| Exchange functionality | No money exchange possible by design |
| Anonymity marketing | Focus on privacy, not anonymity for illegal use |
| Active involvement in illegal use | Clear ToS, prompt takedown on notice |

### 11.2 Relevant German criminal law

| Section | Offense | Relevance |
|:--------|:--------|:----------|
| StGB § 261 | Geldwäsche (money laundering) | Closed-loop mitigates risk significantly |
| StGB § 263 | Betrug (fraud) | User fraud on marketplace - report to authorities |
| StGB § 202a | Ausspähen von Daten | Unauthorised account access - our security prevents |
| TKG § 88 | Fernmeldegeheimnis | Protects GoNode's encrypted communications |

### 11.3 Constitutional protections

Grundgesetz Article 10 (Fernmeldegeheimnis) protects the underlying SimpleX communications. BVerfGE 125, 260 extends this to internet traffic.

The loyalty program itself does not have special constitutional protection - it operates under standard commercial law.

---

## 12. Compliance program

### 12.1 Pre-launch activities

**Phase 0 (months 0-3):**

- Foundation incorporation
- GmbH scope update for loyalty program administration
- Rechtsgutachten from qualified German law firm confirming limited network exemption
- Terms of Service drafting
- Initial compliance documentation

**Phase 1 (months 3-9):**

- DPIA completion
- BaFin proactive notification (if approaching 1M EUR threshold)
- DSA compliance implementation (notice-and-action system)
- Privacy policy finalisation
- Tax reporting infrastructure (DAC7)

**Phase 2 (months 9-15):**

- Legal review of marketplace terms
- Security audit of ledger system
- Consumer protection compliance verification
- Trademark registrations

### 12.2 Ongoing compliance

**Monthly:**
- Transaction monitoring
- Security incident review
- Content moderation statistics

**Quarterly:**
- Compliance self-audit
- Legal framework review (for regulatory changes)
- Risk assessment update

**Annually:**
- External legal review
- DPIA refresh
- Penetration testing
- Tax reporting (DAC7 to tax authorities)

### 12.3 Incident response

**Data breaches:**

- Identification within 24 hours
- Supervisory authority notification within 72 hours (GDPR Art. 33)
- User notification without undue delay if high risk (Art. 34)
- Post-incident review within 30 days

**Marketplace fraud:**

- Immediate listing suspension
- User investigation
- Criminal complaint if warranted
- Restitution between parties (not Foundation-guaranteed)

**Regulatory inquiries:**

- 48-hour acknowledgement
- Substantive response per deadline
- Legal counsel involvement for significant inquiries

---

## 13. Comparison to old crypto-based model

| Compliance Area | Old (crypto token) | New (loyalty system) |
|:----------------|:-------------------|:---------------------|
| MiCA compliance | Extensive (Title II whitepaper, Art. 59 CASP) | None required |
| BaFin interaction | Whitepaper filing, ongoing oversight | Light notification only |
| KWG considerations | Multiple provisions to manage | Minimal |
| GwG | Significant concerns | Largely inapplicable |
| Tax complexity | Complex crypto taxation for users | Standard loyalty treatment |
| DSA | Applicable | Applicable (mostly marketplace) |
| GDPR | Complex (blockchain immutability) | Standard (database is deletable) |
| Tornado Cash risk | Significant | Minimal |
| Legal opinion cost | ~100,000 EUR | ~30,000 EUR |
| Ongoing legal counsel | ~200,000 EUR/year | ~50,000 EUR/year |
| Total legal setup | ~600,000 EUR | ~150,000 EUR |

**Savings from redesign: approximately 450,000 EUR in initial legal costs, 150,000 EUR/year ongoing.**

---

## 14. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [Tokenomics](TOKENOMICS.md) | GoCoin loyalty system design | This repo |
| [Business Model](BUSINESS_MODEL.md) | Revenue streams and funding | This repo |
| [Architecture and Security](ARCHITECTURE_AND_SECURITY.md) | Technical implementation | This repo |
| [Smart Contracts](SMART_CONTRACTS.md) | Ledger technical specs | This repo |
| [Security Policy](../SECURITY.md) | Vulnerability disclosure | This repo |

---

*GoNode Legal Compliance v2 - April 2026 (redesigned from crypto-based v1)*
*IT and More Systems, Recklinghausen, Germany*
