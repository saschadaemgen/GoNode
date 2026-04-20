# GoNode Business Model

**Document version:** Season 1 | April 2026
**Component:** GoNode economic and revenue framework
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document describes the business model sustaining the GoNode infrastructure and the SimpleGo ecosystem. Following the redesign from crypto token to closed-loop loyalty system, the business model has been simplified substantially. Fewer entities, lower setup costs, earlier break-even, lower ongoing compliance burden, and a clearer revenue narrative.

**Core principle:** Real revenue funds the project. The loyalty system rewards users and operators for participation, but does not fund development. Revenue comes from the same four streams as before - Pro subscriptions, enterprise SLAs, AI developer support services, and grants - but without the complications of token markets, DEX liquidity, or market-making obligations.

**Core metric:** break-even targeted in Year 3, with positive cash flow from Year 4. Target revenue by Year 5: 11 million EUR annually at 66% gross margin.

---

## 1. Revenue streams

Four revenue streams support the Foundation's operations:

### 1.1 Pro subscriptions (B2C recurring)

Individual users pay monthly or annual subscriptions for premium features:

| Tier | Price | Target audience |
|:-----|:------|:----------------|
| Basic (free) | 0 EUR | All users |
| Pro | 5 EUR/month or 50 EUR/year | Privacy-conscious individuals |
| Pro+ | 12 EUR/month or 120 EUR/year | Power users with premium needs |
| Hardware bundle | One-time + monthly | Users with GoKey/SimpleGo hardware |

**Pro features include:**
- Hardware-anchored identity via GoKey integration
- Priority message routing
- Extended message retention (90 days vs 24 hours)
- Multi-device synchronisation
- Premium file storage (5 GB vs 500 MB)
- Advanced anti-spam and moderation tools
- Early access to new features

Users paying for Pro also **earn GoCoin as loyalty rewards** (see TOKENOMICS.md) - typically at a rate equivalent to 10-25% of the purchase value in redemption-value GoCoin. This creates a natural flywheel: paying users accumulate points that they redeem for exclusive items or trade on the marketplace.

**Payment methods:**
- SEPA direct debit (primary for EU)
- Credit/debit card
- PayPal
- Apple Pay / Google Pay
- No cryptocurrency payments required

Simple EUR billing. Standard VAT handling. No wallet, no on-ramp friction.

### 1.2 Enterprise SLA (B2B contracts)

Organisations purchase service-level agreements for production use:

| Tier | Monthly | Scale | Features |
|:-----|:--------|:------|:---------|
| Startup | 500 EUR | Up to 100 users | Standard SLA, business hours support |
| Growth | 2,500 EUR | Up to 1,000 users | 99.9% SLA, extended support |
| Enterprise | 10,000+ EUR | 1,000+ users | 99.95% SLA, custom integration, dedicated CSM |
| Government | Custom | Public sector | Extended compliance, on-premise options |

**Enterprise features include:**
- Dedicated swarm clusters (no shared infrastructure with consumers)
- Custom routing rules and policies
- Advanced audit logs and compliance reporting
- Priority security response
- Direct integration with existing IT infrastructure
- Training and onboarding support
- Service Level Agreements with financial penalties for breach

### 1.3 AI Developer Support (B2B services)

Starting Month 3, IT and More Systems offers AI-assisted development support services:

| Service | Typical engagement | Price range |
|:--------|:-------------------|:-----------|
| Initial consultation | 2-4 hours | 500 - 1,500 EUR |
| Architecture review | 2-4 weeks | 10,000 - 50,000 EUR |
| Custom development | Per project | 25,000 - 500,000 EUR |
| Retainer support | Monthly | 5,000 - 25,000 EUR |

This revenue stream draws on expertise developed building SimpleGo and GoNode, using AI-assisted workflows to deliver fast, high-quality results. Margins are strong (60-75%) because much of the work leverages existing IP and tooling.

**Target customers:**
- Privacy-focused startups needing architecture help
- Enterprises building internal communication systems
- Government agencies needing secure communication infrastructure
- Other FOSS projects wanting to integrate with SimpleGo/GoNode

### 1.4 Grants and funding

Strategic grants support non-commercial activities and initial setup:

| Source | Target | Timing | Use |
|:-------|:-------|:-------|:----|
| EU Horizon / Digital Europe | 300-800k EUR | Year 1 | Research, open-source development |
| NLnet | 50-100k EUR | Year 1 | Privacy-focused development |
| BMBF / national grants | 100-300k EUR | Year 1-2 | Infrastructure development |
| Sovereign Tech Fund | 100-500k EUR | Year 1-2 | Open-source sustainability |
| Mozilla Foundation | 50-100k EUR | Year 2 | Privacy tooling |
| Other private grants | 50-200k EUR | Ongoing | Specific initiatives |

**Grant expectations:**
- Year 1 total target: 500k-1M EUR in grants
- Success rate assumed: 30-40% of applications approved
- Applications planned: 10-15 during Year 1

**Important:** Unlike the previous crypto-token design, no treasury-building grant is needed for DEX liquidity (saving 500-800k EUR requirement). This makes grant applications more straightforward - we ask for development funding, not for treasury.

---

## 2. Cost structure

### 2.1 Setup costs (Year 0-1, one-time)

| Category | Amount | Notes |
|:---------|:-------|:------|
| Legal setup (GmbH + legal opinion) | 25,000 EUR | Cheaper than prior dual-entity structure |
| Initial development team ramp | 180,000 EUR | 3 FTE for 6 months before revenue |
| Infrastructure (servers, services) | 30,000 EUR | Initial server purchases and year 1 hosting |
| Compliance implementation | 20,000 EUR | DSA compliance, privacy, age verification |
| Brand and identity | 15,000 EUR | Trademarks, design, website |
| Marketing initial push | 25,000 EUR | Launch campaign |
| Community and ecosystem | 10,000 EUR | Initial seeding of loyalty accounts |
| Security audit (initial) | 30,000 EUR | Standard software audit |
| Initial operating reserve | 200,000 EUR | 6 months operating cushion |
| Contingency (15%) | 20,000 EUR | |
| **Total setup** | **555,000 EUR** | **65% less than crypto-token setup (1.59M)** |

### 2.2 Ongoing operating costs (monthly, Year 3 steady state)

| Category | Monthly | Annual | Notes |
|:---------|:--------|:-------|:------|
| Team (14 FTE at steady state) | 112,000 EUR | 1,344,000 EUR | Down from 15 FTE in old model |
| Infrastructure (cloud + servers) | 12,000 EUR | 144,000 EUR | Scales with user count |
| Compliance and legal | 5,000 EUR | 60,000 EUR | Includes legal retainer |
| Marketing and community | 10,000 EUR | 120,000 EUR | Content, events, sponsorships |
| Insurance | 2,500 EUR | 30,000 EUR | D&O, cyber, business |
| Office and admin | 4,000 EUR | 48,000 EUR | Recklinghausen HQ |
| Tooling and SaaS | 3,500 EUR | 42,000 EUR | Development tools, comms |
| Contingency (10%) | 15,000 EUR | 180,000 EUR | |
| **Total monthly (Year 3)** | **164,000 EUR** | **1,968,000 EUR** | |

### 2.3 Team composition

At steady state (Year 3), the team consists of approximately 14 FTE:

| Role | Count | Notes |
|:-----|:------|:------|
| Core development (Rust/Go) | 5 | GoNode, SimpleGo, wire protocol |
| Frontend/UX | 2 | Apps and marketplace |
| DevOps/Infrastructure | 2 | Service operations |
| Hardware engineering | 1 | GoKey/SimpleGo hardware |
| Security engineering | 1 | Audits, monitoring, incident response |
| Legal and compliance | 1 | Full-time or 0.5 FTE split with outside counsel |
| Community management | 1 | Moderation, events, partnerships |
| Business development | 1 | Enterprise and AI services |
| Leadership | Founder + 0.5 COO | Overall direction |

One FTE less than the prior design (no dedicated tokenomics specialist needed), reducing costs while maintaining capability.

---

## 3. 5-year financial projection

### 3.1 Revenue forecast

| Year | Pro Subs | Enterprise | AI Services | Grants | Total |
|:-----|:---------|:-----------|:------------|:-------|:------|
| 1 | 30,000 EUR | 120,000 EUR | 200,000 EUR | 500,000 EUR | 850,000 EUR |
| 2 | 210,000 EUR | 480,000 EUR | 500,000 EUR | 300,000 EUR | 1,490,000 EUR |
| 3 | 720,000 EUR | 1,200,000 EUR | 800,000 EUR | 200,000 EUR | 2,920,000 EUR |
| 4 | 2,400,000 EUR | 2,200,000 EUR | 1,100,000 EUR | 100,000 EUR | 5,800,000 EUR |
| 5 | 6,000,000 EUR | 3,500,000 EUR | 1,500,000 EUR | 100,000 EUR | 11,100,000 EUR |

### 3.2 Cost and profit

| Year | Revenue | Costs | Net | Pro Subscribers |
|:-----|:--------|:------|:----|:----------------|
| 1 | 850,000 EUR | 980,000 EUR | -130,000 EUR | 500 |
| 2 | 1,490,000 EUR | 1,560,000 EUR | -70,000 EUR | 3,500 |
| 3 | 2,920,000 EUR | 1,970,000 EUR | **+950,000 EUR** | 12,000 |
| 4 | 5,800,000 EUR | 2,600,000 EUR | **+3,200,000 EUR** | 40,000 |
| 5 | 11,100,000 EUR | 3,600,000 EUR | **+7,500,000 EUR** | 100,000 |

**Key milestones:**
- **Break-even:** Year 3 (earlier than previous Year 4 target due to lower costs)
- **Cash positive:** Year 3
- **Strong margin:** 68% gross margin by Year 5
- **Operating reserve replenished:** Year 4

### 3.3 Pro subscriber growth assumptions

| Year | New Subs | Churn | Net | Total |
|:-----|:---------|:------|:----|:------|
| 1 | 500 | 0 | 500 | 500 |
| 2 | 3,500 | 500 | 3,000 | 3,500 |
| 3 | 10,000 | 1,500 | 8,500 | 12,000 |
| 4 | 32,000 | 4,000 | 28,000 | 40,000 |
| 5 | 70,000 | 10,000 | 60,000 | 100,000 |

Churn assumptions based on industry standard for privacy-focused subscription services (lower than mass-market SaaS).

### 3.4 Enterprise customer growth

| Year | New | Total | Avg ARR |
|:-----|:----|:------|:--------|
| 1 | 2 | 2 | 60,000 EUR |
| 2 | 6 | 8 | 60,000 EUR |
| 3 | 12 | 20 | 60,000 EUR |
| 4 | 18 | 36 | 60,000 EUR |
| 5 | 22 | 55 | 63,000 EUR |

Enterprise contracts include both SLA and integration services.

---

## 4. Loyalty system economics

### 4.1 How the loyalty system supports the business

GoCoin loyalty rewards directly support the business model in three ways:

**Retention flywheel:** Users who accumulate GoCoin through subscriptions and community participation have ongoing incentive to stay engaged. Churn rates for loyalty program members are typically 30-50% lower than non-members.

**Upsell driver:** Users with GoCoin balances are more likely to purchase higher tiers, hardware, and special editions to redeem their points. This creates natural upsell opportunities without aggressive marketing.

**Community strengthening:** The peer-to-peer marketplace creates user-to-user interactions, building community bonds that strengthen product loyalty.

### 4.2 Loyalty program costs

The loyalty program has modest direct costs:

| Category | Annual (steady state) |
|:---------|:----------------------|
| Special edition production | 30,000 EUR |
| Community rewards | 20,000 EUR |
| Marketplace operations | 15,000 EUR |
| Customer support for coin issues | 12,000 EUR |
| **Total** | **77,000 EUR** |

This is dramatically lower than the old crypto-token model which required:
- 500,000 EUR DEX liquidity (now zero)
- 50,000 EUR CEX listings (now zero)
- 80,000 EUR market maker retainer (now zero)
- 60,000 EUR tokenomics specialist (now zero)
- 120,000 EUR smart contract audits (now zero)
- **Total saved: 810,000 EUR/year compared to old model**

### 4.3 Marketplace fee revenue

The peer-to-peer marketplace generates modest fee revenue:

| Year | Marketplace Transactions | Avg Value | Foundation Fee (3%) |
|:-----|:-------------------------|:----------|:---------------------|
| 3 | 5,000 | 50 EUR equiv | 7,500 EUR |
| 4 | 25,000 | 60 EUR equiv | 45,000 EUR |
| 5 | 75,000 | 75 EUR equiv | 169,000 EUR |

These fees are denominated in GoCoin and burned (removed from circulation), not converted to EUR. The burn supports the loyalty system's supply control.

---

## 5. Comparison: old crypto-token model vs. new loyalty model

### 5.1 Setup cost comparison

| Category | Old model | New model | Savings |
|:---------|:----------|:----------|:--------|
| Legal (dual entity) | 150,000 EUR | 25,000 EUR | 125,000 EUR |
| DEX liquidity | 500,000 EUR | 0 EUR | 500,000 EUR |
| CEX listings | 50,000 EUR | 0 EUR | 50,000 EUR |
| Market maker engagement | 80,000 EUR | 0 EUR | 80,000 EUR |
| Smart contract audits | 150,000 EUR | 30,000 EUR | 120,000 EUR |
| Tokenomics design | 40,000 EUR | 5,000 EUR | 35,000 EUR |
| MiCA whitepaper | 70,000 EUR | 0 EUR | 70,000 EUR |
| Other setup | 550,000 EUR | 495,000 EUR | 55,000 EUR |
| **Total setup** | **1,590,000 EUR** | **555,000 EUR** | **1,035,000 EUR** |

### 5.2 Annual operating cost comparison

| Category | Old model | New model | Savings |
|:---------|:----------|:----------|:--------|
| Team (15 vs 14 FTE) | 1,440,000 | 1,344,000 | 96,000 |
| MiCA compliance | 180,000 | 0 | 180,000 |
| Token-related legal | 120,000 | 0 | 120,000 |
| Market making retainer | 60,000 | 0 | 60,000 |
| DEX monitoring | 24,000 | 0 | 24,000 |
| Smart contract audits (annual) | 80,000 | 10,000 | 70,000 |
| Tokenomics operations | 60,000 | 0 | 60,000 |
| Other operations | 596,000 | 614,000 | -18,000 |
| **Total annual** | **2,560,000** | **1,968,000** | **592,000** |

### 5.3 Break-even comparison

| Milestone | Old model | New model | Improvement |
|:----------|:----------|:----------|:------------|
| Operating break-even | Year 4 | Year 3 | 1 year earlier |
| Cash flow positive | Year 4 | Year 3 | 1 year earlier |
| Foundation reserve replenished | Year 5 | Year 4 | 1 year earlier |
| Initial funding required | 1,590,000 EUR | 555,000 EUR | 65% less |

---

## 6. Unit economics

### 6.1 Pro subscriber unit economics

**Acquisition cost:**
- CAC assumption: 25 EUR per Pro subscriber
- Channels: organic (60%), content marketing (20%), community referral (15%), paid (5%)

**Lifetime value:**
- Average subscription length: 18 months
- Average monthly revenue: 5 EUR
- Average lifetime gross profit: 18 * 5 * 0.85 = 76.50 EUR
- **LTV/CAC ratio: 3.0x** (healthy for subscription business)

### 6.2 Enterprise customer unit economics

**Acquisition cost:**
- CAC for enterprise: 15,000 EUR (longer sales cycle, custom proposals)
- Channels: direct outreach, community-referred, conference

**Lifetime value:**
- Average contract length: 3 years
- Average ARR: 60,000 EUR
- Lifetime revenue: 180,000 EUR
- Gross margin: 65%
- Lifetime gross profit: 117,000 EUR
- **LTV/CAC ratio: 7.8x** (very healthy)

### 6.3 AI Services unit economics

**Acquisition cost:**
- CAC: 5,000 EUR per project
- Channels: inbound referral, existing customer expansion

**Revenue per engagement:**
- Average project: 75,000 EUR
- Gross margin: 65%
- Per-project gross profit: 48,750 EUR
- **LTV/CAC ratio: 9.8x** (excellent)

---

## 7. Risk analysis

### 7.1 Revenue risks

**Slow Pro adoption:**
- Risk: Pro subscribers grow slower than projected
- Mitigation: Free tier with compelling features maintains engagement; Pro features continually improved; Enterprise and AI services provide alternative revenue
- Scenario: If Pro growth hits only 50% of target, revenue drops by 30% but break-even delayed only 12 months

**Enterprise sales cycle:**
- Risk: Long enterprise sales cycles delay revenue
- Mitigation: AI Services provide faster revenue while enterprise pipeline develops; lower-tier Enterprise plans accessible to startups
- Scenario: If enterprise lags 6 months behind plan, Year 3 break-even pushed to Year 3.5

**Grant approval rates:**
- Risk: Lower than expected grant success rate
- Mitigation: Diversified grant portfolio (10-15 applications); ability to survive on revenue alone from Year 3
- Scenario: If grants deliver 50% of target, operating reserve required but long-term viability unaffected

### 7.2 Cost risks

**Team cost inflation:**
- Risk: Senior engineering talent costs rise faster than planned
- Mitigation: Location in Recklinghausen provides cost advantage vs. Berlin/Munich; remote-friendly hiring expands talent pool
- Scenario: 10% team cost inflation delays break-even by ~3 months

**Compliance cost escalation:**
- Risk: Regulatory changes increase compliance costs
- Mitigation: Conservative design staying within established loyalty precedent; minimal regulatory surface area
- Scenario: Significant compliance increase would affect all competitors equally

### 7.3 Market risks

**Privacy market evolution:**
- Risk: Privacy concerns decrease, reducing addressable market
- Mitigation: Multiple use cases beyond pure privacy (enterprise, IoT, developer services)
- Counter-evidence: Privacy concerns are increasing, not decreasing, in 2025-2026

**Competitor response:**
- Risk: Larger players (Apple, Google) improve privacy offerings
- Mitigation: Focus on hardware and infrastructure where large players don't compete; open-source moat; community building
- Counter-evidence: Big tech improvements drive awareness, benefiting smaller specialised players

---

## 8. Funding strategy

### 8.1 Initial funding: 555,000 EUR

Target composition for initial setup funding:

| Source | Target | Timing |
|:-------|:-------|:-------|
| Founder contribution | 100,000 EUR | Immediate |
| Strategic investors (non-control) | 200,000 EUR | Month 1-3 |
| Initial grants (smaller, quick-turn) | 150,000 EUR | Month 3-6 |
| Revenue (first customers) | 105,000 EUR | Month 1-6 |
| **Total** | **555,000 EUR** | **6 months** |

No initial DEX liquidity needed. No crypto treasury requirements. Much simpler funding story than the previous crypto-token model.

### 8.2 Strategic investor profile

If bringing in strategic investors beyond founder and grants:
- Aligned values: Privacy, open-source, European technology sovereignty
- Reasonable expectations: Understanding of patient capital for infrastructure
- Relevant expertise: Enterprise sales, security, regulatory
- Governance respect: Not seeking control over technical or regulatory decisions

**Ideal profiles:**
- Privacy-focused angel investors
- Enterprise tech operators
- FOSS ecosystem funders (NLnet, Sovereign Tech Fund)
- European digital sovereignty initiatives

### 8.3 Secondary funding: not required

Unlike typical startups, GoNode does not need a Series A. Break-even in Year 3 means external funding is only needed for initial 555k setup. From Year 4, internal cash flow funds expansion.

This is a major simplification from the previous design which targeted a Token Generation Event for additional capital.

---

## 9. Milestones and use of funds

### 9.1 Months 0-6: Foundation and setup

**Goals:**
- Legal entity setup complete
- Core team hired (8 FTE)
- Initial infrastructure deployed
- First 100 paying Pro users
- First enterprise prospect conversations

**Use of funds (approximate):**
- Legal and setup: 50,000 EUR
- Team: 200,000 EUR (partial year)
- Infrastructure: 30,000 EUR
- Marketing: 25,000 EUR
- Reserve: 250,000 EUR

### 9.2 Months 7-18: Early traction

**Goals:**
- 3,500 Pro subscribers
- 8 Enterprise customers
- AI Services delivering steady revenue
- First marketplace beta users
- Grant applications submitted

**Key metrics:** MRR, CAC, churn rate, NPS, grant conversion rate

### 9.3 Months 19-36: Break-even path

**Goals:**
- 12,000 Pro subscribers
- 20 Enterprise customers
- Marketplace live and growing
- Hardware product line established
- Operating cash positive

**Key metrics:** LTV/CAC ratios all above 3, gross margin above 65%, team productivity

### 9.4 Year 4-5: Scale

**Goals:**
- 40,000-100,000 Pro subscribers
- 36-55 Enterprise customers
- Strong AI Services practice
- Consider international expansion
- Consider permissioned blockchain evaluation

**Strategic decisions at Year 4:**
- International expansion outside Germany/EU
- Premium hardware product launch
- Partnerships with complementary projects

---

## 10. Exit strategy considerations

GoNode is designed as a sustainable business, not an exit vehicle. However, several future paths remain available:

### 10.1 Continued operation (primary path)

- Stay independent and grow
- Generate profit for reinvestment
- Fund ecosystem expansion (GoShop, GoTube, GoBook, GoOS)
- Maintain mission alignment long-term

### 10.2 Strategic acquisition (low priority)

Only considered if:
- Acquirer has genuine commitment to privacy mission
- Technical continuity preserved
- Team and community remain intact
- Open-source licensing maintained
- Governance structure respects community

### 10.3 Foundation model (possible future)

Convert commercial operations to non-profit Foundation structure:
- Protects long-term mission
- Attracts donations and grants
- Prevents hostile acquisition
- Common model for successful privacy projects (Signal Foundation precedent)

### 10.4 What we explicitly reject

- Sale to surveillance-aligned company
- Abandonment of privacy mission for revenue
- Token speculation or pump-and-dump behaviour (not possible with loyalty system anyway)
- Proprietary relicensing of open-source code
- Compromise of user privacy for commercial gain

---

## 11. Financial controls

### 11.1 Governance

- Standard GmbH governance under German law
- Monthly financial reviews by leadership
- Quarterly board review (when advisors engaged)
- Annual external audit once above thresholds

### 11.2 Treasury management

- Operating cash: EUR only, held at reputable German banks
- Reserve: Minimum 6 months operating costs
- **No crypto treasury:** Unlike previous design, Foundation holds no volatile crypto assets
- Short-term investments: Low-risk EUR money market for excess reserves

### 11.3 Transparency

- Monthly internal reporting
- Quarterly community updates
- Annual audited financial statements
- Public milestone reporting

---

## 12. Strategic alignment

### 12.1 Alignment with GoNode technical mission

The business model directly supports technical goals:
- **Revenue funds development:** No pressure to compromise for quick wins
- **Enterprise focus drives quality:** Business customers demand robust software
- **AI Services provide technical leverage:** Cross-pollination benefits open-source work
- **Grants fund non-commercial work:** Community and research remain funded
- **Loyalty rewards drive engagement:** Users have ongoing incentive to use platform

### 12.2 Alignment with SimpleGo ecosystem

GoNode's business model supports the broader SimpleGo ecosystem:
- Hardware revenue (GoKey, SimpleGo devices) feeds into ecosystem
- Enterprise relationships open doors for SimpleGo/GoBot/GoUNITY adoption
- Developer services promote ecosystem-wide technical excellence
- Grant funding benefits all ecosystem components
- User base growth creates demand for complementary products

### 12.3 Alignment with privacy values

Revenue choices reinforce values:
- No advertising model: Users are customers, not products
- No data monetisation: Zero-knowledge architecture prevents it even if desired
- No dark patterns: Consumer protection and community trust are paramount
- Transparent pricing: Simple subscription, no hidden fees
- No tracking revenue: Analytics are privacy-preserving

---

## 13. Comparison with competitor financials

For context, comparison with similar privacy projects:

| Project | Revenue (est.) | Users | Status |
|:--------|:---------------|:------|:-------|
| Signal Messenger | 50M USD (donations) | 100M+ | Non-profit |
| ProtonMail | 150M EUR | 70M | Growing profitably |
| Tutanota | 20M EUR | 10M | Growing |
| Session | N/A (token-funded) | 1.7M | Shutting down April 2026 |
| Threema | 25M CHF | 11M | Profitable |

GoNode targets 11M EUR revenue at Year 5 with 100,000 Pro users. This is realistic given the market size demonstrated by ProtonMail, Threema, and Tutanota's trajectories, and distinctive through enterprise focus and ecosystem breadth.

---

## 14. Related documents

| Document | Relevance |
|:---------|:----------|
| [README](../README.md) | Project overview |
| [Concept](CONCEPT.md) | Strategic rationale |
| [Tokenomics](TOKENOMICS.md) | Loyalty program details |
| [Architecture and Security](ARCHITECTURE_AND_SECURITY.md) | Technical foundation |
| [Legal Compliance](LEGAL_COMPLIANCE.md) | Regulatory framework |
| [Roadmap](ROADMAP.md) | Execution timeline |

---

*GoNode Business Model v2 - April 2026 (redesigned for loyalty system)*
*IT and More Systems, Recklinghausen, Germany*
