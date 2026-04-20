# GoNode Legal Compliance

**Document version:** Season 1 | April 2026
**Component:** GoNode regulatory compliance and legal framework
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the legal and regulatory framework under which GoNode operates. Following the redesign of GoCoin from a crypto token to a closed-loop loyalty system, the legal framework has changed substantially. This document covers the applicable frameworks: Payment Services Directive (PSD2) and German ZAG, E-Money Directive, GDPR, Digital Services Act (DSA), German commercial and civil law, tax law, and consumer protection.

**Disclaimer:** This document is not legal advice. It summarises our good-faith understanding of applicable regulations and our compliance approach. A formal legal opinion (Rechtsgutachten) from a qualified German law firm specialising in loyalty programs and digital services will be commissioned before the marketplace launches.

| Jurisdiction | Primary Applicability |
|:-------------|:----------------------|
| Germany | Operating entity jurisdiction (IT and More Systems GmbH) |
| European Union | GDPR, DSA, PSD2, Consumer Rights Directive |
| Switzerland | Optional Foundation jurisdiction for international operations (future) |

---

## 1. Entity structure

### 1.1 Operating entity

The primary operating entity is **IT and More Systems GmbH** in Recklinghausen, Germany. This entity:

- Issues GoCoin loyalty points to users and operators
- Operates the peer-to-peer marketplace
- Provides customer support and manages disputes
- Handles tax reporting obligations
- Maintains the GoCoin ledger (database or permissioned blockchain)
- Develops the open-source software
- Contracts with enterprise customers

The two-entity structure from the previous crypto-token design (Swiss Foundation + German GmbH) is **no longer required** because:

- No token issuance triggering MiCA Title II obligations
- No Foundation treasury holding volatile assets
- No need for Swiss crypto-friendly banking
- Lower operational complexity and cost

A Swiss Foundation may still be established later for international expansion, but this is optional and not on the critical path.

### 1.2 Corporate responsibility

IT and More Systems GmbH is responsible for:

| Area | Responsibility |
|:-----|:--------------|
| Loyalty program administration | Primary issuer |
| Marketplace operations | Platform operator |
| Data protection (GDPR) | Data Controller |
| DSA compliance | Platform operator |
| Tax reporting (DAC7) | Platform operator |
| Consumer protection | Seller of ecosystem goods |
| Software publication | Publisher under AGPL-3.0 |

### 1.3 Governance

Governance is standard corporate governance under German GmbH law (GmbHG), with additional transparency commitments:

- Monthly transparency reports on coin supply and transactions
- Annual audited financial reports
- Quarterly community reports on development progress
- Public disclosure of material Terms of Service changes with 6 months notice

---

## 2. Loyalty program classification

### 2.1 The limited network exception

GoCoin is designed to qualify for the **limited network exception** under European payment services law. This exception is the legal basis for virtually every loyalty program in the EU.

**Payment Services Directive 2 (Directive 2015/2366), Article 3(k):**

PSD2 excludes from its scope:

> "services based on specific payment instruments that can be used only in a limited way, that meet one of the following conditions:
>
> (i) instruments allowing the holder to acquire goods or services only in the premises of the issuer or within a limited network of service providers under direct commercial agreement with a professional issuer;
>
> (ii) instruments which can be used only to acquire a very limited range of goods or services;
>
> (iii) instruments valid only in a single Member State provided at the request of an undertaking or a public sector entity and regulated by a national or regional public authority for specific social or tax purposes to acquire specific goods or services from suppliers having a commercial agreement with the issuer."

GoCoin qualifies under Art. 3(k)(i): users can only redeem coins within the SimpleGo ecosystem, from a single issuer (IT and More Systems GmbH).

**German Zahlungsdiensteaufsichtsgesetz (ZAG), § 2 Abs. 1 Nr. 10:**

The German implementation of PSD2 Art. 3(k) excludes services based on instruments usable only in a limited network, for a limited range of goods/services, or under specific tax/social purposes agreements.

### 2.2 BaFin notification requirement

**Important procedural note:** Even when the exemption applies, § 2 Abs. 2 ZAG requires **notification to BaFin** if annual transaction volume exceeds **1 million EUR** in the preceding 12 months.

For GoCoin:

- **Below 1M EUR transaction value per year:** No BaFin notification required
- **Above 1M EUR:** Notification to BaFin (informational, not an authorisation)
- **Above 1M EUR:** Annual report to BaFin demonstrating continued qualification for exemption

The notification is a simple administrative filing - it is not an authorisation process. BaFin does not approve or reject, but can request additional information if concerns arise.

### 2.3 E-Money Directive non-applicability

**E-Money Directive (2009/110/EC)** defines electronic money in Art. 2(2):

> "electronically, including magnetically, stored monetary value as represented by a claim on the issuer which is issued on receipt of funds for the purpose of making payment transactions, and which is accepted by a natural or legal person other than the electronic money issuer"

GoCoin is **not** e-money because:

- Not issued on receipt of funds from the holder (earned as loyalty, not purchased)
- Not accepted by persons other than the issuer (redeemable only within SimpleGo ecosystem)
- Does not represent a monetary claim on the issuer (fixed redemption for goods, not money)

**Recital 14 E-Money Directive** explicitly excludes:

> "monetary value stored on specific pre-paid instruments, designed to address precise needs that can be used only in a limited way, either because it allows the specific instrument holder to purchase goods or services only in the premises of the electronic money issuer or within a limited network of service providers under direct commercial agreement with a professional issuer"

This confirms the closed-loop loyalty exemption.

### 2.4 MiCA non-applicability

**MiCA Regulation (EU 2023/1114)** applies to crypto-assets. Art. 3(1)(5) defines a crypto-asset as:

> "a digital representation of a value or of a right that is able to be transferred and stored electronically using distributed ledger technology or similar technology"

Whether GoCoin falls within this depends on technology choice:

**If internal database (recommended for Phase 1):**
- Not distributed ledger technology
- Not a crypto-asset under MiCA
- MiCA does not apply at all

**If permissioned blockchain (possible Phase 3+):**
- Uses DLT
- But MiCA Art. 2(4) excludes limited-use instruments
- Analogous to PSD2 Art. 3(k), limited network scope excludes from MiCA scope
- The exemption is less explicit than in PSD2, so legal opinion required

**Conservative approach:** Use internal database for Phase 1 to avoid any MiCA ambiguity. Revisit if permissioned blockchain becomes strategically important.

### 2.5 Comparison with existing German loyalty programs

| Program | Provider | Legal Basis | Transaction Volume (annual) |
|:--------|:---------|:------------|:----------------------------|
| Payback | Loyalty Partner Solutions GmbH | § 2 ZAG exemption | 500M+ EUR |
| Lufthansa Miles & More | Miles & More GmbH | § 2 ZAG exemption | Billions EUR |
| BahnBonus | DB Vertrieb GmbH | § 2 ZAG exemption | 100M+ EUR |
| Deutsche Telekom Magenta Moments | Deutsche Telekom AG | § 2 ZAG exemption | 50M+ EUR |
| Amazon Coins | Amazon Services Europe | § 2 ZAG exemption | Confidential |

None of these programs hold e-money licenses or payment service authorisations. They all operate under the same exemption framework GoCoin will use.

---

## 3. Gaming precedents

The peer-to-peer marketplace aspect of GoCoin is closest in structure to gaming industry closed economies.

### 3.1 Steam Marketplace (Valve)

Valve operates Steam Marketplace in the EU through Valve S.a.r.l. (Luxembourg):

- Steam Wallet credits classified under Luxembourg payment services exemption (equivalent to PSD2 Art. 3(k))
- Peer-to-peer trading of digital items allowed
- Items cannot be withdrawn as money (except through informal third-party channels Valve does not endorse)
- 7-day trade lock on items (similar to our 30-day operator holding period)
- Marketplace fee approximately 15% (we charge 2-5%)
- Annual EU transaction volume estimated in billions of EUR

Valve operates without e-money license or payment service authorisation based on the closed-loop structure.

### 3.2 World of Warcraft Gold (Blizzard)

Blizzard Entertainment operates WoW Gold as an in-game currency in the EU. WoW Token (peer-to-peer tradeable for time credit) operates under Irish payment services exemption.

Key lesson: Even peer-to-peer tradeable items qualify as closed-loop loyalty when they cannot be redeemed for money directly.

### 3.3 Fortnite V-Bucks (Epic Games)

Epic Games operates V-Bucks in the EU. Recent US FTC settlement (2022) over dark patterns in purchasing does not affect EU classification.

Key lesson: Clear, transparent redemption rules and user-friendly terms are critical for maintaining loyalty program status. GoCoin's fixed redemption rates address this.

### 3.4 EVE Online (CCP Games)

CCP Games operates EVE Online's complex closed economy (ISK, PLEX) in the EU from Iceland:

- 20+ years of operation without regulatory intervention
- Published monthly economic reports (transparency)
- Peer-to-peer trading and complex player markets
- PLEX convertible between real-money-purchased and in-game-earned states
- Regulators treat it as a closed-loop loyalty/gaming system

Key lesson: Long operational history demonstrates that closed-loop systems with active peer-to-peer markets can operate indefinitely under existing regulatory frameworks.

### 3.5 Roblox Robux

Roblox Corporation operates Robux in the EU through Roblox Netherlands B.V.

Key legal feature: DevEx program allows developers to convert earned Robux to USD, but through specific commercial agreements and KYC verification - not a general marketplace function. This is a structure GoCoin explicitly avoids to maintain simpler classification.

---

## 4. Digital Services Act (DSA)

### 4.1 Regulatory background

**Regulation:** Regulation (EU) 2022/2065 (Digital Services Act).
**Applicability:** Fully applicable since 17 February 2024.
**Relevance to GoNode:** The peer-to-peer marketplace qualifies as an intermediary service.

### 4.2 Intermediary categorisation

| Activity | DSA Classification | Obligations |
|:---------|:------------------|:------------|
| Hosting user-generated marketplace listings | Art. 6 (hosting service) | Notice-and-action, clear terms |
| Connecting buyers and sellers | Art. 3(i) (online platform) | Transparency, illegal content reporting |
| Not reaching 45M EU users | Not a VLOP | Standard obligations only |

### 4.3 Key DSA obligations

**Art. 11 (single point of contact for authorities):**
- Email: authorities@gonode.dev
- Response within 24 hours for authority requests
- Documented escalation process

**Art. 12 (single point of contact for users):**
- Marketplace support email and web form
- Response within 72 hours for user reports
- Accessible dispute resolution mechanism

**Art. 14 (terms and conditions):**
- Marketplace Terms clearly posted
- Available in German and English
- Written in plain language
- Changes announced 14 days in advance

**Art. 16 (notice-and-action mechanism):**
- Web form and email for reporting illegal content
- Structured information collection
- Acknowledgment within 48 hours
- Decision within 7 days with reasoning

**Art. 17 (statement of reasons):**
- When removing content or restricting accounts
- Legal basis cited
- Internal appeal mechanism

**Art. 20-22 (internal complaints, out-of-court dispute resolution):**
- Internal complaint handling process (free to users)
- Decision within 6 months maximum
- Information about certified external dispute resolution bodies

**Art. 24 (transparency reporting):**
- Annual transparency report
- Statistics on content moderation and user suspensions

### 4.4 Marketplace-specific obligations

**Art. 30 (traceability of traders):**

Applies if the marketplace hosts commercial sellers (not just consumers):
- Most users are consumers trading personal items - Art. 30 does not apply
- If commercial users participate, traceability requirements apply (collect and verify trader identity)

**Art. 31 (compliance by design):**

- Marketplace design makes it easy to comply with legal obligations
- Clear categories for listings
- Automatic checks for prohibited items

**Art. 32 (right to information):**

- If illegal offers are identified, users who purchased must be informed
- Contact information for enforcement authorities when relevant

### 4.5 Content moderation principles

The marketplace will:

- Prohibit listings that violate law
- Prohibit listings that violate Terms of Service (e.g., attempts to sell coins for money)
- Automatically flag suspicious patterns
- Manually review reported listings
- Maintain audit log of moderation decisions

---

## 5. GDPR compliance

### 5.1 Legal basis for processing

GoCoin operations process personal data on these legal bases:

| Data type | Legal basis | GDPR article |
|:----------|:------------|:-------------|
| Account information | Contract performance | Art. 6(1)(b) |
| Transaction history | Contract + legal obligation | Art. 6(1)(b), (c) |
| Marketplace listings | Contract performance | Art. 6(1)(b) |
| Dispute records | Legitimate interest | Art. 6(1)(f) |
| Anti-fraud monitoring | Legitimate interest | Art. 6(1)(f) |
| Tax reporting data | Legal obligation | Art. 6(1)(c) |
| Marketing (optional) | Consent | Art. 6(1)(a) |

### 5.2 Data minimisation

The Foundation collects only necessary data:

- Account creation: email (verified), pseudonym (optional)
- Marketplace participation: account link only
- Transaction records: sender, recipient, amount, timestamp, type
- Tax reporting: required DAC7 fields only

Not collected by default:
- Real name (unless required for DAC7 above thresholds)
- Physical address (unless hardware shipping requested)
- Phone number (optional)
- Government ID (unless required for dispute escalation or DAC7)

### 5.3 User rights

| Right | Article | Implementation |
|:------|:--------|:---------------|
| Access | Art. 15 | Dashboard + full data export in JSON |
| Rectification | Art. 16 | Self-service for most fields |
| Erasure | Art. 17 | Account deletion with 30-day grace period |
| Restriction | Art. 18 | Account suspension mechanism |
| Portability | Art. 20 | Machine-readable export |
| Objection | Art. 21 | Marketing opt-out |
| Automated decision-making | Art. 22 | No fully automated significant decisions |

### 5.4 Data retention

| Data category | Retention period | Reason |
|:-------------|:-----------------|:-------|
| Active account data | Duration of account + 30 days | User convenience |
| Transaction records | 10 years | German commercial law (HGB § 257) |
| Tax reporting data | 10 years | § 147 AO |
| Marketplace listings | 2 years after completion | Dispute resolution |
| Moderation actions | 5 years | DSA audit requirements |
| Anonymised analytics | Indefinite | Service improvement |

### 5.5 Data protection impact assessment (DPIA)

Under Art. 35 GDPR, a DPIA is required for high-risk processing:

**DPIA required for:**
- Peer-to-peer marketplace (large-scale processing of user activities)
- DAC7 reporting (transfer to tax authorities)
- Permissioned blockchain (if implemented in Phase 3+)

A formal DPIA will be conducted before Phase 3 marketplace launch.

### 5.6 International data transfers

Data stays within the EU by default:

- Servers located in Germany
- Backup services in other EU countries
- Support staff located in EU
- No default transfer to third countries

If international transfers become necessary:
- Standard Contractual Clauses (SCCs) per EU Commission Decision 2021/914
- Transfer impact assessments
- Explicit user consent where required

---

## 6. Consumer protection

### 6.1 Consumer Rights Directive compliance

**Directive 2011/83/EU** and German implementation (§§ 312 ff. BGB) apply to:

- Purchase of Pro subscriptions (service contracts)
- Purchase of hardware devices (distance selling)
- Peer-to-peer marketplace transactions (partially)

### 6.2 Withdrawal rights

**For purchases from the Foundation:**

Users have the right to withdraw from purchases within 14 days under § 355 BGB:
- Digital services (Pro subscriptions): withdrawal possible unless user explicitly waives it after service begins
- Hardware: full 14-day withdrawal right with return shipping
- Special edition redemptions: withdrawal possible if digital goods not yet accessed

**For peer-to-peer marketplace trades:**
- Consumer-to-consumer trades: no statutory withdrawal right
- Commercial-to-consumer trades: 14-day withdrawal right applies
- Foundation dispute resolution available as backup

### 6.3 Warranty rights

**Statutory warranty (§§ 434 ff. BGB):**
- Applies to hardware sold by the Foundation
- 2-year warranty period for consumers
- 1-year warranty period for commercial buyers

**Digital content:**
- Foundation guarantees continued accessibility of purchased digital goods
- Bug fixes and security updates provided during support period
- 6 months notice for service discontinuation

### 6.4 Unfair terms

Terms avoid clauses considered unfair under § 309 BGB and UCP Directive:
- No unilateral changes without notice
- No exclusion of statutory consumer rights
- No disproportionate penalties
- Clear language, not legal jargon

---

## 7. Age verification and minors

### 7.1 Legal basis

**German Jugendschutzgesetz (JuSchG)** and **Jugendmedienschutz-Staatsvertrag (JMStV)** apply. **Article 8 GDPR** requires parental consent for children under 16 in Germany.

### 7.2 Age verification approach

**For basic account creation:**
- Age self-declaration (like most web services)
- Age 16+ for independent accounts
- Under 16: account requires parental consent

**For marketplace participation:**
- Minimum age 18 for independent marketplace use
- Age 16-17: marketplace use with verified parental consent
- Under 16: marketplace access blocked entirely

**For purchases:**
- Age 18 required for direct Foundation purchases (§ 107 BGB requires consent of legal representative for minors)
- Hardware devices available to minors 16+ with parental consent

### 7.3 Content restrictions

Marketplace listings are moderated to prevent:
- Adult content (JuSchG compliance)
- Violent or harmful content
- Content requiring age verification by law
- Gambling-adjacent content

---

## 8. Taxation

### 8.1 Tax treatment for users

**Purchase reward GoCoin:**

Bonus coins received as reward for purchasing services/goods are treated as **price reduction (Rabatt)** under German tax law:
- Not separate taxable income for the user
- Effectively reduces the purchase price
- No immediate taxable event
- Reference: BMF guidance on loyalty programs (analogous treatment to Payback points)

**Redemption of GoCoin:**

When users redeem coins for ecosystem goods:
- Not a new taxable event for consumers (like redeeming Payback points)
- Foundation collects VAT on the goods/services at delivery
- If coins are redeemed for physical goods above 250 EUR value, potential income tax consideration - typically covered by personal exemptions

**Peer-to-peer marketplace trades:**

When users trade items/coins between each other:
- Private sales up to 600 EUR/year tax-free under § 23 Abs. 3 EStG
- Commercial frequency may trigger business classification
- Long-held items (1+ year) generally tax-free for private users
- DAC7 reporting above 2,000 EUR per user per year or 30+ transactions

### 8.2 Tax treatment for node operators

Node operator rewards are taxable income:

**Commercial operators (gewerblich):**
- Revenue under § 15 EStG
- Gewerbeanmeldung required if profit-oriented and continuous
- Subject to Gewerbesteuer above thresholds
- Proper bookkeeping required
- Valuation at fair market value on receipt date

**Hobby operators (Liebhaberei):**
- Income below 256 EUR/year: tax-free under § 22 Nr. 3 EStG
- Above threshold: sonstige Einkünfte
- Simpler reporting via personal tax return

**Valuation of rewards:**

Since GoCoin has fixed redemption values (not market prices), valuation is straightforward: the EUR-equivalent redemption value at the time of receipt.

**Foundation reporting to operators:**

Annual earnings statements provided to all operators with monthly coin receipts, EUR valuation, and year-to-date totals.

### 8.3 VAT / Umsatzsteuer

**Foundation VAT obligations:**
- Pro subscriptions: standard German VAT (19%)
- Hardware sales: standard German VAT
- Marketplace fees: VAT if above small-business threshold (§ 19 UStG)
- EU cross-border: OSS (One Stop Shop) registration for consumer sales in other EU countries

**GoCoin transactions:**
- Issuance of loyalty coins: not a VAT event
- Redemption of coins for goods: VAT on the goods/services delivered
- Peer-to-peer trades: outside VAT scope for private users
- Commercial P2P trades: VAT may apply for commercial seller

### 8.4 DAC7 reporting

**Directive (EU) 2021/514 (DAC7)** requires platform operators to report user transactions to tax authorities.

**Applicability to GoNode:**
- Platform operator: IT and More Systems GmbH
- Reportable activities: peer-to-peer marketplace transactions above thresholds
- Reporting frequency: annual
- Reporting threshold: 2,000 EUR per user per year OR 30+ transactions

**Implementation:**
- Data collection: user tax residence, TIN, transaction volumes
- Annual report to Bundeszentralamt für Steuern (BZSt)
- User notification about reporting
- Records retained 10 years

### 8.5 Corporate tax

IT and More Systems GmbH pays standard German corporate taxes:
- Körperschaftsteuer 15% + Solidaritätszuschlag 5.5% = 15.825%
- Gewerbesteuer approximately 14-17% depending on municipality
- Total effective corporate tax rate: approximately 30-32%

---

## 9. Insolvency considerations

### 9.1 User protection if operator fails

If IT and More Systems GmbH becomes insolvent, user coin balances are treated under German insolvency law (§§ 1 ff. Insolvenzordnung):
- Contractual claims against the Foundation for future services
- Not deposits requiring separate protection
- Similar treatment to Payback points, airline miles, gift cards, Steam Wallet balances
- In insolvency proceedings: users join the general creditor pool

### 9.2 Mitigating measures

The Foundation commits to:
- Separate customer deposit funds for pending services where possible
- Minimum 6 months operating reserve
- Business interruption and cyber insurance
- Monthly transparency reports on financial health
- Early warning if financial difficulties arise

### 9.3 Prepaid services concern

For users paying in advance (annual subscriptions, prepaid orders):
- Funds held as deposits until service delivered
- Users have priority claim for undelivered services under consumer protection law
- Foundation maintains operational reserves to fulfil existing obligations

---

## 10. Anti-money laundering (AML)

### 10.1 GwG non-applicability

The Geldwäschegesetz (GwG) applies to "Verpflichtete" listed in § 2. GoNode is not:
- Not a financial institution
- Not a payment service provider (PSD2 exemption)
- Not a crypto-asset service provider (closed-loop exemption)
- Not subject to GwG Verpflichteter status

### 10.2 Voluntary AML measures

Despite GwG non-applicability, the Foundation implements voluntary AML measures:
- Suspicious activity monitoring with automated flagging
- Transaction velocity limits
- Volume thresholds triggering review
- Behavioural analysis for illicit patterns
- Voluntary reporting of suspicious activity to authorities

### 10.3 Why AML matters even without GwG

- Reputational risk from illicit use
- Regulatory monitoring
- Enterprise customers require clean compliance record
- DAC7 reporting creates tax authority visibility
- Banking relationships require AML policies

---

## 11. Intellectual property and licensing

### 11.1 Open source licensing

GoNode software is licensed under **AGPL-3.0**:
- Source code must be made available to users of network services
- Derivative works must be licensed under AGPL-3.0
- No warranty or liability for code
- Commercial use permitted with copyleft obligations

### 11.2 Trademark considerations

Trademarks to be registered:
- "GoCoin" (word mark, classes 9, 35, 38, 42)
- "GoNode" (word mark, classes 9, 38, 42)
- "SimpleGo" (word mark + logo, multiple classes)
- EU Trade Mark (EUTM) registration preferred

### 11.3 Third-party IP

Open source dependencies comply with respective licenses:
- All dependencies audited for license compatibility with AGPL-3.0
- No proprietary dependencies incorporated
- Attribution maintained as required
- SBOM (Software Bill of Materials) published

---

## 12. Compliance program

### 12.1 Implementation timeline

**Phase 0 (Months 0-3):**
- Legal opinion on loyalty program classification
- Terms of Service drafting
- Privacy policy (GDPR compliance)
- DSA notice-and-action mechanism design
- Trademark applications

**Phase 1 (Months 3-9):**
- DPIA for marketplace and DAC7 reporting
- Marketplace Terms of Service
- Dispute resolution procedures
- Age verification implementation

**Phase 2 (Months 9-15):**
- Full DSA compliance documentation
- DAC7 reporting infrastructure
- AML policy documentation
- External compliance audit

**Phase 3 (Months 15-21):**
- Marketplace launch with full compliance
- Ongoing monitoring and reporting
- Annual transparency report

### 12.2 Ongoing compliance

**Monthly:** Transaction pattern monitoring, suspicious activity review, content moderation reports

**Quarterly:** Internal compliance audit, regulatory update review, policy adjustments

**Annually:** External compliance audit, transparency report, DAC7 reporting to BZSt, insurance renewal, legal opinion refresh

### 12.3 Incident response

**Data breaches:**
- Identification within 24 hours
- Supervisory authority notification within 72 hours (Art. 33 GDPR)
- User notification as required (Art. 34 GDPR)

**Security incidents:**
- Initial response within 1 hour
- Stakeholder communication per severity
- Coordinated response per SECURITY.md

**Regulatory inquiries:**
- Acknowledgement within 48 hours
- Substantive response per deadline
- Legal counsel engagement for significant matters

---

## 13. Comparison: old crypto-token compliance vs. new loyalty compliance

| Area | Old (Crypto Token) | New (Loyalty System) |
|:-----|:-------------------|:---------------------|
| Primary regulation | MiCA Title II | PSD2 Art. 3(k) / ZAG § 2 |
| Pre-launch filing | MiCA whitepaper to BaFin | Simple notification (if volume > 1M EUR) |
| Classification effort | Significant legal opinion cost | Established precedent, lower cost |
| Ongoing reporting | MiCA Art. 82 reporting | Simple annual notification |
| Compliance team size | 2-3 FTE needed | 0.5-1 FTE sufficient |
| Legal opinion cost | 50,000 - 150,000 EUR | 10,000 - 30,000 EUR |
| Audit requirements | Smart contract audits (50-200k EUR) | Standard software audits (10-30k EUR) |
| CASP risk | High (Tornado Cash precedent) | Not applicable |
| GwG Verpflichteter | Possible | Not triggered |
| BaFin relationship | Active oversight | Minimal (notification only) |
| International complexity | Varies by jurisdiction | Standard EU loyalty framework |
| User data requirements | Standard + crypto-specific | Standard only |
| Settlement risk | Blockchain finality concerns | Normal contract law |
| Total annual compliance cost | 200,000 - 400,000 EUR | 30,000 - 80,000 EUR |

---

## 14. Regulatory risk assessment

### 14.1 Classification reclassification risk

**Risk:** Regulators reclassify GoCoin as e-money or crypto-asset.
**Likelihood:** Low. Closed-loop structure well-established.
**Mitigation:** Conservative design, legal opinion documenting classification basis, early engagement with BaFin, ability to modify design if regulatory guidance changes.

### 14.2 DSA enforcement risk

**Risk:** DSA compliance issues trigger sanctions.
**Likelihood:** Low-medium for new platforms.
**Mitigation:** Strong initial DSA compliance framework, clear Terms of Service, responsive notice-and-action system, transparency reporting from launch.

### 14.3 Tax classification risk

**Risk:** Tax authorities challenge loyalty program treatment.
**Likelihood:** Low. Guidance well-established.
**Mitigation:** Follow BMF guidance, proper documentation of transactions, conservative valuation approaches, annual tax review.

### 14.4 Consumer protection risk

**Risk:** Consumer protection authorities find unfair practices.
**Likelihood:** Low with proper Terms of Service.
**Mitigation:** Terms drafted by consumer protection specialist, regular review, proactive dispute resolution, no aggressive retention or dark patterns.

### 14.5 Cross-border risk

**Risk:** Different interpretation in other EU member states.
**Likelihood:** Low for established loyalty framework.
**Mitigation:** Stay within EU-harmonised rules, legal review for major market expansions, no country-specific sensitive features.

---

## 15. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [Tokenomics](TOKENOMICS.md) | Economic design of loyalty system | This repo |
| [Architecture and Security](ARCHITECTURE_AND_SECURITY.md) | Technical implementation | This repo |
| [Business Model](BUSINESS_MODEL.md) | Revenue structure supporting compliance | This repo |
| [Security Policy](../SECURITY.md) | Vulnerability disclosure process | This repo |
| [Code of Conduct](../CODE_OF_CONDUCT.md) | Community standards | This repo |

---

*GoNode Legal Compliance v2 - April 2026 (redesigned for loyalty system)*
*IT and More Systems, Recklinghausen, Germany*
