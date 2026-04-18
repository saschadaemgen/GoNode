# GoNode Business Model

**Document version:** Season 1 | April 2026
**Component:** GoNode revenue streams and financial projections
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the complete business model for the GoNode network: four independent revenue streams, pricing strategy, customer acquisition plan, unit economics, five-year financial projections and funding requirements. Every figure is based on benchmarked data from comparable projects (Session, Storj, Matrix/Element, Threema, Helium) adjusted for GoNode's specific market position.

The core financial principle of GoNode is **revenue before token**. Real fiat revenue from Pro subscriptions, enterprise SLAs, AI developer support and grants flows before the Token Generation Event. By the time GoCoin launches, the Foundation has 18+ months of EUR-denominated runway secured. The token enhances an existing business; it does not create one.

| Metric | Target Year 5 |
|:-------|:--------------|
| Annual revenue | 11,000,000 EUR |
| Operating profit | 7,600,000 EUR |
| Profit margin | 69% |
| Pro subscribers | 100,000 |
| Enterprise customers | 100 |
| AI service seats | 5,000 |
| Funded runway at launch | 18 months |

---

## 1. The four revenue streams

GoNode intentionally avoids dependency on any single revenue source. Four parallel streams ensure resilience:

| Stream | Contribution (Year 5) | Risk Profile | Time-to-Revenue |
|:-------|:---------------------|:-------------|:----------------|
| GoNode Pro subscriptions | 6,000,000 EUR (55%) | Market risk (consumer demand) | Phase 2 (month 9) |
| Enterprise SLA contracts | 3,600,000 EUR (33%) | Sales cycle risk | Phase 1 (month 3) |
| AI Developer Support | 1,200,000 EUR (11%) | Technology risk (AI quality) | Phase 1 (month 3) |
| Non-dilutive grants | 200,000 EUR (1%) | Application risk | Phase 0 (month 0) |

**Why diversification matters:** Every token-funded decentralised messenger failed because they had only one revenue source - token appreciation. When the bear market hit, so did the funding crisis. GoNode's four-stream design means any single stream can collapse to zero while the others carry operations.

---

## 2. Stream 1: GoNode Pro subscriptions

### 2.1 Product description

GoNode Pro is a consumer subscription that unlocks enhanced features on top of the free SimpleGo messaging experience. Free users get full messaging functionality. Pro users get additional capacity, priority, and advanced features.

### 2.2 Features by tier

| Feature | Free | GoNode Pro |
|:--------|:----:|:----------:|
| Encrypted messaging | Yes | Yes |
| File transfers | Up to 1 GB/file | Up to 10 GB/file |
| File storage quota | 1 GB | 100 GB |
| Message history retention | 30 days | Unlimited |
| Priority message routing | No | Yes |
| Hardware identity (GoKey) | No | Yes |
| Advanced group moderation | No | Yes |
| Custom relay pinning | No | Yes |
| Early access to new features | No | Yes |
| Community support | Yes | Yes |
| Direct support (email) | No | Yes |

### 2.3 Pricing

| Plan | Price | Discount vs Monthly |
|:-----|:------|:-------------------|
| Monthly | 5 EURC/month | - |
| Annual | 50 EURC/year | 16% (2 months free) |
| Lifetime (limited launch offer) | 150 EURC | Year 2 breakeven |

**Why 5 EURC:** Benchmarked against comparable privacy services:
- Threema: 5 EUR one-time (12M users, profitable)
- ProtonMail Plus: 4 EUR/month (100M+ users)
- Tutanota Premium: 3-5 EUR/month
- Signal: voluntary donations (not a pricing comparable, but 40M+ USD annual costs)
- Matrix Element X Pro: 5 EUR/month

5 EURC is the sweet spot: low enough for mass-market adoption, high enough to support development.

### 2.4 Customer acquisition

**Target customers:** privacy-conscious individuals, journalists, activists, security researchers, small businesses handling sensitive data.

**Acquisition channels (prioritised by CAC):**

| Channel | Estimated CAC | Priority | Notes |
|:--------|:--------------|:---------|:------|
| SimpleGo community upgrade | 5 EUR | P0 | Existing users, easiest conversion |
| Privacy-focused communities (Reddit, HN) | 15 EUR | P1 | Content marketing, AMAs |
| Partnership with privacy NGOs | 10 EUR | P1 | EFF, Privacy International, Digitalcourage |
| Search (Google, DuckDuckGo) | 30 EUR | P2 | "private messenger" keywords |
| Conference presence (36C3, BSidesEU, etc.) | 50 EUR | P2 | Technical credibility building |
| Paid ads (Twitter, Reddit) | 40 EUR | P3 | Only after product-market fit |

### 2.5 Pro subscription growth model

Conservative assumptions based on comparable privacy service adoption curves:

| Year | Start of Year | Monthly Adds (avg) | Churn (annual) | End of Year | Revenue |
|:-----|:--------------|:-------------------|:--------------|:------------|:--------|
| 1 | 0 | 80 | 15% | 500 | 30,000 EUR |
| 2 | 500 | 300 | 15% | 3,500 | 210,000 EUR |
| 3 | 3,500 | 800 | 15% | 12,000 | 720,000 EUR |
| 4 | 12,000 | 2,500 | 15% | 40,000 | 2,400,000 EUR |
| 5 | 40,000 | 5,500 | 15% | 100,000 | 6,000,000 EUR |

**Growth rationale:**
- Year 1: very conservative, still-new product, word-of-mouth only
- Year 2: first public testnet exposes project to broader privacy community
- Year 3: TGE brings media attention, airdrop creates 10k loyalty base
- Year 4: post-TGE maturity, enterprise contracts validate product
- Year 5: organic growth, network effects, international expansion

### 2.6 Lifetime value (LTV)

```
Average customer lifetime: 15% annual churn -> ~6.7 years expected
Monthly revenue: 5 EURC
Annual revenue: 60 EURC (or 50 EURC if annual plan)

LTV at monthly plan: 5 × 80 = 400 EURC
LTV at annual plan: 50 × 6.7 = 335 EURC

Weighted LTV (70% monthly, 30% annual): 380 EURC

LTV/CAC ratios:
  Community upgrade: 380/5 = 76x (excellent)
  Privacy communities: 380/15 = 25x (very good)
  Paid search: 380/30 = 12x (good)
  Paid ads: 380/40 = 9.5x (acceptable)
```

These LTV/CAC ratios compare favorably to SaaS benchmarks (3-5x is considered healthy).

---

## 3. Stream 2: Enterprise SLA contracts

### 3.1 Product description

Enterprise SLA contracts provide organisations with dedicated GoNode capacity, custom deployment options, compliance support, and service level agreements. The primary reference architecture is Matrix/Element's enterprise offering, which has signed contracts with the German BundesMessenger, French Tchap (360k MAU), NATO ACT, Swedish SAFOS, UNICC, Luxembourg government, and US Space Force.

### 3.2 Target customers

| Segment | Typical Organization | Representative Deal Size |
|:--------|:--------------------|:------------------------|
| Government (federal) | BMI, BSI, agencies | 5,000 - 50,000 EUR/month |
| Government (state/local) | Länder, municipalities | 1,500 - 5,000 EUR/month |
| Healthcare | Hospitals, practices | 1,500 - 5,000 EUR/month |
| Financial services | Banks, insurance | 2,500 - 10,000 EUR/month |
| Legal | Law firms, compliance | 500 - 2,500 EUR/month |
| NGO | Human rights, journalism | 500 - 1,500 EUR/month (discounted) |
| Research | Universities, institutes | 500 - 2,500 EUR/month |
| Critical infrastructure | Energy, water, transport | 2,500 - 10,000 EUR/month |

### 3.3 Pricing tiers

| Tier | Price | Users | Storage | Features |
|:-----|:------|:------|:--------|:---------|
| **Starter** | 500 EUR/month | up to 50 | 100 GB | SLA 99.5%, email support |
| **Business** | 1,500 EUR/month | up to 250 | 1 TB | + GoKey integration, phone support |
| **Enterprise** | 5,000 EUR/month | up to 1,000 | 10 TB | + dedicated private swarm, 24/7 support |
| **Government** | Custom | Unlimited | Custom | + on-premise option, custom SLA, compliance docs |

### 3.4 Competitive positioning

| Criterion | Matrix/Element | GoNode |
|:----------|:--------------|:-------|
| Decentralisation | Federated (homeservers) | Fully decentralised (swarms) |
| Protocol | Matrix protocol | SimpleX (better metadata resistance) |
| Hardware identity | None | GoKey integration |
| Cryptography | Olm/Megolm | SimpleX five-layer + post-quantum |
| German brand | Foreign (UK) | German/Swiss |
| Reference customers | Many (first-mover) | Starting (post-TGE) |
| Price positioning | 3-8 EUR/user/month | 500-5000 EUR/tier |

**Win conditions:** GoNode wins against Matrix when:
- Customer needs hardware-rooted security (Matrix cannot match GoKey)
- Customer values metadata resistance (SimpleX vs Matrix protocol advantage)
- Customer prefers German/Swiss jurisdiction
- Customer wants tiered pricing rather than per-user (lower TCO at scale)

### 3.5 Sales process

**Enterprise sales cycle: 3-9 months typical**

```
Month 1: Initial contact, technical briefing
Month 2: Security review, compliance documentation
Month 3: Pilot deployment (free, 30 days)
Month 4-5: Expansion planning, contract negotiation
Month 6: Contract signed, production deployment
Month 7+: Support, expansion revenue, case study
```

**Required sales assets:**

| Asset | Status |
|:------|:-------|
| White paper (technical) | Complete (this document set) |
| Security audit reports | Planned Phase 1-2 |
| Compliance documentation (ISO 27001, GDPR) | Phase 2 |
| Customer references | Phase 1+ (pilots) |
| Demo environment | Phase 1 |
| Sales collateral (slides, videos) | Phase 2 |
| Proposal templates | Phase 1 |

### 3.6 Enterprise growth model

| Year | New Customers | Churn | Total Customers | Average Deal | Annual Revenue |
|:-----|:--------------|:------|:----------------|:-------------|:---------------|
| 1 | 3 | 0% | 3 | 6,000 EUR | 18,000 EUR |
| 2 | 12 | 10% | 14 | 8,500 EUR | 120,000 EUR |
| 3 | 35 | 10% | 47 | 10,000 EUR | 480,000 EUR |
| 4 | 65 | 10% | 107 | 13,500 EUR | 1,440,000 EUR |
| 5 | 85 | 5% | 186 | 19,400 EUR | 3,600,000 EUR |

Note: "Average Deal" grows because later customers include more Enterprise and Government tier (higher price points). Reduced churn in Year 5 reflects product maturity.

---

## 4. Stream 3: AI Developer Support service

### 4.1 Product description

An AI assistant trained on the complete SimpleGo ecosystem codebase (SimpleGo, GoBot, GoKey, GoUNITY, GoLab, GoNode and related repositories) that provides accurate, context-aware answers to integration and development questions.

This service is uniquely enabled by the ecosystem's comprehensive documentation and source code. Generic AI assistants (ChatGPT, Claude, GitHub Copilot) produce hallucinated or outdated answers about SimpleGo APIs because they lack specific training data. A specialised AI trained on the full codebase provides dramatically better answers for developers integrating the ecosystem.

**Real-world validation:** The user (Sascha Daemgen) has personally trained a Claude instance on the full codebase over 6 months and saved an estimated 6 months of development time implementing the SMP protocol in Rust. This is the value proposition: experienced developers save months of learning time.

### 4.2 Pricing tiers

| Plan | Price | Queries/Month | Features |
|:-----|:------|:--------------|:---------|
| **Free Trial** | 0 EUR | 10 | Basic Q&A |
| **Developer** | 20 EUR/seat/month | 500 | Full codebase access |
| **Professional** | 50 EUR/seat/month | 2,500 | + Architecture advice, code review |
| **Team** | 150 EUR/month (5 seats) | Pooled 10,000 | + Team collaboration features |
| **Enterprise** | Custom | Custom | + Private instance, SLA |

### 4.3 Technology stack

**AI backend options:**

| Option | Pros | Cons | Estimated Cost per Query |
|:-------|:-----|:-----|:-------------------------|
| OpenAI GPT-4 API | Mature, well-known | Data sent to OpenAI | 0.03 - 0.10 USD |
| Anthropic Claude API | Best code understanding | Data sent to Anthropic | 0.03 - 0.10 USD |
| Self-hosted Llama 3.3 70B | Privacy, control | Infrastructure cost, quality | 0.01 - 0.05 USD (at scale) |
| Mistral Large API | European provider | Smaller ecosystem | 0.02 - 0.06 USD |

**Recommended:** Start with Anthropic Claude API (best quality), transition to self-hosted Llama when volume justifies infrastructure cost (~10,000 queries/month).

### 4.4 Unit economics

```
Developer plan (20 EUR/month, 500 queries):
  Revenue: 20 EUR
  Query cost (at 0.05 EUR avg): 25 EUR maximum
  BUT: average user uses 150 queries, not 500
  Actual cost: 150 × 0.05 = 7.50 EUR
  Gross margin: (20 - 7.50) / 20 = 62.5%

Professional plan (50 EUR/month, 2,500 queries):
  Revenue: 50 EUR
  Actual usage: 600 queries avg
  Actual cost: 600 × 0.05 = 30 EUR
  Gross margin: (50 - 30) / 50 = 40%

Team plan (150 EUR/month, 10,000 queries pooled):
  Revenue: 150 EUR
  Actual usage: 3,500 queries avg across 5 seats
  Actual cost: 3,500 × 0.05 = 175 EUR
  Gross margin: negative without optimization

Optimization: self-hosted Llama at scale reduces cost to 0.01 EUR/query:
  Developer: 20 - (150 × 0.01) = 18.50 EUR margin (92.5%)
  Professional: 50 - (600 × 0.01) = 44 EUR margin (88%)
  Team: 150 - (3,500 × 0.01) = 115 EUR margin (77%)
```

### 4.5 Customer acquisition

**Built-in acquisition:** SimpleGo is actively used by developers integrating the ecosystem. Every developer hitting a documentation question is a potential customer.

**Channels:**
- Documentation site (every doc page has "Ask AI" widget)
- GitHub integration (AI answers issues in GoNode repos)
- Developer conferences (give away 3-month Developer plan)
- Referrals from integration partners

### 4.6 AI service growth model

| Year | Subscribers | Avg Price | Monthly Revenue | Annual Revenue |
|:-----|:------------|:----------|:----------------|:---------------|
| 1 | 50 | 20 EUR | 1,000 EUR | 12,000 EUR |
| 2 | 200 | 25 EUR | 5,000 EUR | 60,000 EUR |
| 3 | 500 | 33 EUR | 16,666 EUR | 200,000 EUR |
| 4 | 1,000 | 42 EUR | 41,666 EUR | 500,000 EUR |
| 5 | 2,000 | 50 EUR | 100,000 EUR | 1,200,000 EUR |

Average price rises as enterprise/team plans dominate in later years.

---

## 5. Stream 4: Non-dilutive grants

### 5.1 Overview

Grants from foundations and ecosystems provide capital without diluting token supply or equity. This stream is critical in Phase 0-1 when other revenue is minimal.

### 5.2 Active grant pipeline

| Source | Grant Size | Fit | Application Status | Target Decision |
|:-------|:-----------|:----|:-------------------|:----------------|
| Arbitrum Foundation | 500k - 2M USD | Very high (Arbitrum deployment) | Draft in Phase 0 | Month 3 |
| Ethereum Foundation ESP | 10k - 250k USD | High (privacy infrastructure) | Draft in Phase 0 | Month 4 |
| NLnet Foundation (NGI Zero) | 5k - 50k EUR (2 tracks) | Very high (public interest, privacy) | Phase 0 | Month 3 |
| Web3 Foundation | 10k / 30k / 100k USD | Moderate (Polkadot-adjacent) | Phase 1 | Month 6 |
| Octant (Golem) | 20k - 150k USD/epoch | High (public goods) | Phase 1 | Quarterly |
| Filecoin Foundation | 25k - 300k USD | Moderate (storage-adjacent) | Phase 1 | Month 8 |
| EU Digital Europe Programme | 100k - 5M EUR | Very high (privacy + sovereignty) | Phase 1 | Month 9 |
| Privacy-focused VCs | 100k - 2M EUR | Optional | Phase 2 if needed | - |

### 5.3 Grant strategy

**Phase 0 (months 0-3): foundation-level grants for setup**
- NLnet NGI Zero: 50k EUR for initial protocol design work
- Ethereum Foundation ESP: 100k USD for smart contract development

**Phase 1 (months 3-9): major technical grants**
- Arbitrum Foundation: 1M USD for full network deployment
- EU Digital Europe: 500k EUR for European deployment

**Phase 2+ (months 9+): strategic grants**
- Octant: quarterly $50k-$150k for continued development
- Filecoin Foundation: specific integrations

### 5.4 Expected grant revenue

| Year | Expected Grants | Cumulative |
|:-----|:----------------|:-----------|
| 1 | 400,000 EUR | 400,000 |
| 2 | 600,000 EUR | 1,000,000 |
| 3 | 500,000 EUR | 1,500,000 |
| 4 | 300,000 EUR | 1,800,000 |
| 5 | 200,000 EUR | 2,000,000 |

Grant revenue declines over time as the project becomes self-sustaining through commercial revenue. This is the desired trajectory.

---

## 6. Cost structure

### 6.1 Cost categories

| Category | Year 1 | Year 5 | Notes |
|:---------|:-------|:-------|:------|
| Development (salaries) | 300,000 EUR | 1,800,000 EUR | 3 FTE -> 15 FTE |
| Legal and compliance | 120,000 EUR | 200,000 EUR | MiCA, GDPR, audits, ongoing |
| Infrastructure (bootstrap nodes) | 60,000 EUR | 240,000 EUR | Initial nodes, monitoring |
| Security audits | 80,000 EUR | 300,000 EUR | Annual audits + bug bounty |
| Marketing and community | 40,000 EUR | 500,000 EUR | Conferences, content, ads |
| Operations (Foundation admin) | 80,000 EUR | 150,000 EUR | Swiss entity, accounting |
| AI inference costs | 10,000 EUR | 200,000 EUR | Claude/GPT API or self-hosted Llama |
| Sales and BD | 0 EUR | 400,000 EUR | Full-time enterprise sales team |
| **Total** | **690,000 EUR** | **3,790,000 EUR** | |

### 6.2 Team growth

| Year | FTE | Structure |
|:-----|:----|:----------|
| 1 | 3 | 1 tech lead, 1 protocol engineer, 1 legal/ops |
| 2 | 6 | + 1 smart contract, 1 DevRel, 1 sales |
| 3 | 10 | + 2 engineers, 1 cryptographer, 1 DevOps |
| 4 | 12 | + 1 designer, 1 community manager |
| 5 | 15 | + 2 enterprise sales, 1 compliance officer |

### 6.3 Compensation philosophy

| Role | Compensation Structure |
|:-----|:-----------------------|
| Technical lead | 80-100k EUR base + significant token allocation |
| Senior engineer | 70-90k EUR base + moderate token allocation |
| Junior engineer | 50-65k EUR base + small token allocation |
| Sales | 60-90k EUR base + commission on deals + moderate token |
| Operations | 55-75k EUR base + small token allocation |
| Part-time advisors | Token-only compensation |

Swiss-competitive but not Silicon Valley levels. Token upside provides the long-term incentive alignment.

---

## 7. Five-year financial projection

### 7.1 Revenue projection

| Year | Pro Subs | Enterprise | AI Service | Grants | **Total Revenue** |
|:-----|:---------|:-----------|:-----------|:-------|:------------------|
| 1 | 30,000 | 18,000 | 12,000 | 400,000 | **460,000** |
| 2 | 210,000 | 120,000 | 60,000 | 600,000 | **990,000** |
| 3 | 720,000 | 480,000 | 200,000 | 500,000 | **1,900,000** |
| 4 | 2,400,000 | 1,440,000 | 500,000 | 300,000 | **4,640,000** |
| 5 | 6,000,000 | 3,600,000 | 1,200,000 | 200,000 | **11,000,000** |

All figures in EUR, conservatively rounded.

### 7.2 Cost projection

| Year | Dev | Legal | Infra | Audits | Mkt | Ops | AI | Sales | **Total Costs** |
|:-----|:----|:------|:------|:-------|:----|:----|:----|:------|:----------------|
| 1 | 300k | 120k | 60k | 80k | 40k | 80k | 10k | 0 | **690,000** |
| 2 | 500k | 150k | 100k | 100k | 80k | 100k | 20k | 150k | **1,200,000** |
| 3 | 900k | 170k | 150k | 150k | 150k | 120k | 60k | 300k | **2,000,000** |
| 4 | 1,300k | 180k | 200k | 200k | 300k | 130k | 130k | 360k | **2,800,000** |
| 5 | 1,800k | 200k | 240k | 300k | 500k | 150k | 200k | 400k | **3,790,000** |

### 7.3 Profitability projection

| Year | Revenue | Costs | Net | Margin |
|:-----|:--------|:------|:----|:-------|
| 1 | 460,000 | 690,000 | **-230,000** | -50% |
| 2 | 990,000 | 1,200,000 | **-210,000** | -21% |
| 3 | 1,900,000 | 2,000,000 | **-100,000** | -5% |
| 4 | 4,640,000 | 2,800,000 | **+1,840,000** | 40% |
| 5 | 11,000,000 | 3,790,000 | **+7,210,000** | 66% |

**Cumulative operating results:**
- Years 1-3 total loss: -540,000 EUR
- Year 4 alone turns profitable and covers previous losses within 2 months
- Year 5 generates >10x the cumulative loss in a single year

### 7.4 Sensitivity analysis

What if Pro subscriber growth is 50% slower than projected?

| Year | Pro Subs (slow) | Pro Revenue (slow) | Total Revenue | Net |
|:-----|:----------------|:-------------------|:--------------|:----|
| 5 | 50,000 | 3,000,000 | 8,000,000 | +4,210,000 |

Still profitable, just smaller. The four-stream diversification provides resilience.

What if enterprise sales are 30% slower?

| Year | Enterprise (slow) | Total Revenue | Net |
|:-----|:------------------|:--------------|:----|
| 5 | 2,500,000 | 9,900,000 | +6,110,000 |

Still profitable. Enterprise is the highest-risk stream but not critical.

What if both Pro and Enterprise underperform by 30%?

| Year | Total Revenue | Net |
|:-----|:--------------|:----|
| 5 | 7,700,000 | +3,910,000 |

Still profitable.

---

## 8. Initial funding requirements

### 8.1 Capital needs

To reach break-even in Year 4, GoNode must fund the cumulative operating deficit of Years 1-3 plus one-time establishment costs.

| Item | Amount (EUR) | Source |
|:-----|:-------------|:-------|
| Years 1-3 operating deficit | 540,000 | Grants + strategic round |
| Legal setup (Foundation, MiCA WP, advisory) | 100,000 | Foundation treasury / grants |
| Initial DEX liquidity (EURC side) | 500,000 | Foundation treasury |
| Security audits (pre-launch) | 150,000 | Grants |
| Buffer (6 months additional runway) | 300,000 | Reserve |
| **Total initial funding requirement** | **1,590,000** | |

### 8.2 Funding plan

**Phase 0-1 (months 0-9): grant-heavy**

```
Arbitrum Foundation:   1,000,000 USD ≈ 920,000 EUR
Ethereum Foundation:     150,000 USD ≈ 140,000 EUR
NLnet (2 tracks):        100,000 EUR
EU Digital Europe:       300,000 EUR

Total grants targeted:   1,460,000 EUR
```

**Phase 2 (months 9-15): optional strategic round**

If grants fall short, a 5M GoCoin strategic round at 0.20 EURC (pre-TGE valuation):

```
5,000,000 GoCoin × 0.20 EURC = 1,000,000 EURC raised
Investors: privacy-focused funds, mission-aligned VCs
Terms: 2-year lockup, no board seats, utility token only
Dilution: 5% of total supply to strategic investors
```

**Phase 3+ (months 15+): self-sustaining**

Post-TGE revenue covers operations. No additional dilution needed.

### 8.3 Grant application strategy

**Arbitrum Foundation ($1M target):**
- Angle: bringing SimpleX protocol to Arbitrum, decentralised messaging infrastructure
- Timeline: Phase 0 draft, submit month 2, decision month 3-4
- Deliverables: testnet deployment, mainnet contracts, user acquisition targets

**Ethereum Foundation ESP ($150k target):**
- Angle: privacy-preserving infrastructure on Ethereum ecosystem
- Timeline: Phase 0 draft, submit month 2, decision month 4
- Deliverables: protocol research, smart contract development, security audits

**NLnet NGI Zero (2x 50k EUR target):**
- Angle: public interest privacy infrastructure, European sovereignty
- Track 1: NGI Zero Core (protocol implementation)
- Track 2: NGI Zero Entrust (security and trust aspects)
- Timeline: rolling applications, decisions within 6-8 weeks

**EU Digital Europe Programme (300-800k EUR target):**
- Angle: European digital sovereignty, privacy-by-design infrastructure
- Timeline: EU grants have longer cycles (12-18 months)
- Consortium: potentially with academic partners (TU Berlin, TU Munich, ETH Zurich)

### 8.4 Risk: what if grants fail?

**Scenario: Arbitrum Foundation grant is declined**

Impact: 920k EUR shortfall. Mitigations:
- Accelerate strategic round (close in month 6 instead of month 12)
- Apply to additional sources (a16z crypto, Variant, Placeholder)
- Delay Phase 2 deliverables by 3 months to extend runway
- Consider reducing team by 1 FTE for 6 months

**Scenario: All grants are declined**

Very unlikely (at least 2-3 of the 6 applications should succeed based on statistics), but mitigations:
- Execute full strategic round (1M EUR)
- Accept equity investment from aligned VCs (2-3M EUR, last resort)
- Delay TGE by 6 months, extend Phase 1 runway

---

## 9. Unit economics summary

### 9.1 Revenue per customer

| Stream | Year 5 Customers | Revenue per Customer (annual) |
|:-------|:-----------------|:-----------------------------|
| Pro subscriptions | 100,000 | 60 EUR |
| Enterprise SLA | 186 | 19,350 EUR |
| AI service | 2,000 | 600 EUR |

### 9.2 Gross margins

| Stream | Gross Margin | Notes |
|:-------|:-------------|:------|
| Pro subscriptions | ~90% | Infrastructure cost is marginal (shared) |
| Enterprise SLA | ~75% | Higher support burden, SLA obligations |
| AI service | ~60-85% | Depends on self-hosted vs API inference |

### 9.3 Break-even analysis

```
Fixed annual costs (Year 3): ~2,000,000 EUR

At 100% Pro margin: 2M/60 = 33,333 Pro subs needed to break even on Pro alone
At 100% Enterprise margin: 2M/19,350 = 103 enterprise customers needed alone
At 100% AI margin: 2M/600 = 3,333 AI customers needed alone

With actual margins and diversified revenue, break-even reached in Year 4 with:
- 40,000 Pro subs × 60 EUR × 90% = 2,160,000 EUR gross profit
- 107 Enterprise × 13,500 EUR × 75% = 1,083,000 EUR gross profit
- 1,000 AI × 42 EUR × 12 × 70% = 352,800 EUR gross profit
- Grants: 300,000 EUR

Total: 3,895,800 EUR gross > 2,800,000 EUR costs -> profitable
```

---

## 10. Long-term vision

### 10.1 Five-year outlook (years 6-10)

After Year 5, GoNode has:
- 100,000+ Pro subscribers (international base)
- 200+ enterprise customers
- 2,000+ AI service subscribers
- 2,000-5,000 active node operators
- Self-sustaining revenue without grants
- Token economy in net deflation (burn > emission)

**Next growth frontiers:**

| Frontier | Opportunity | Timeline |
|:---------|:------------|:---------|
| International expansion | 10x addressable market | Years 6-7 |
| Additional product lines (GoShop, GoTube, GoBook) | Cross-ecosystem revenue | Years 6-8 |
| Developer platform (third-party integrations) | Platform economy | Years 7-10 |
| Regulated enterprise (banking, healthcare) | Premium tier | Years 8-10 |
| Hardware expansion (GoKey evolution) | Physical products | Years 6-8 |

### 10.2 Exit scenarios (none required)

Unlike VC-backed startups, GoNode does not require an exit. The Swiss Stiftung structure is designed for long-term operation, not liquidation. Possible long-term outcomes:

- **Self-sustaining operation indefinitely:** target outcome
- **Foundation transitions to pure DAO:** post-Phase 4, Foundation becomes optional
- **Acquisition by privacy-focused organisation:** possible but not sought
- **Merger with aligned project:** possible if strategic rationale exists

Developers retain their vested GoCoin allocations regardless of outcome. Node operators retain their stakes and rewards. Users retain their Pro subscriptions until expiry.

---

## 11. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [GoNode Tokenomics](TOKENOMICS.md) | Token economic mechanics | This repo |
| [GoNode Architecture](ARCHITECTURE_AND_SECURITY.md) | Technical basis for services | This repo |
| [GoNode Legal Compliance](LEGAL_COMPLIANCE.md) | Regulatory framework | This repo |
| [GoNode Roadmap](ROADMAP.md) | Execution phases and milestones | This repo |
| [SimpleGo ecosystem](https://github.com/saschadaemgen/SimpleGo) | Broader context | SimpleGo repo |

---

*GoNode Business Model v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
