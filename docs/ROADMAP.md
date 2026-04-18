# GoNode Roadmap

**Document version:** Season 1 | April 2026
**Component:** GoNode phase planning and milestones
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the execution roadmap for GoNode from concept (April 2026) through full DAO governance (estimated April 2029). The roadmap follows a deliberate 5-phase structure with revenue-first milestones, ensuring the Foundation has paying customers and proven product-market fit before the Token Generation Event.

Each phase has explicit deliverables, success criteria, and funding milestones. Every phase ends with a go/no-go review based on objective metrics. If a phase's success criteria are not met, the roadmap is adjusted before proceeding.

| Phase | Timeline | Focus | Status |
|:------|:---------|:------|:-------|
| Phase 0 | Months 0-3 (Apr 2026 - Jul 2026) | Foundation setup, grants, team | Current |
| Phase 1 | Months 3-9 (Jul 2026 - Jan 2027) | Permissioned testnet, first revenue | Planned |
| Phase 2 | Months 9-15 (Jan 2027 - Jul 2027) | Public testnet, MiCA filing | Planned |
| Phase 3 | Months 15-24 (Jul 2027 - Apr 2028) | TGE, mainnet launch | Planned |
| Phase 4 | Months 24+ (Apr 2028+) | DAO transition, ecosystem expansion | Planned |

---

## 1. Phase 0: Foundation (Months 0-3)

**Goal:** Establish legal and operational foundation. Secure initial non-dilutive funding. Build core team. Publish concept documentation.

**Timeline:** April 2026 - July 2026

### 1.1 Legal setup

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Foundation incorporation begun | Month 1 | Mandate to Swiss law firm, Stiftungsurkunde drafted |
| IT and More Systems GmbH scope update | Month 1 | Handelsregister filing for GoNode activities |
| Rechtsgutachten commissioned | Month 1 | Engagement letter with qualified crypto law firm |
| Initial trademark search | Month 2 | Availability report for "GoCoin", "GoNode" |
| Foundation incorporated | Month 3 | Stiftung registered with Canton of Zug |
| Bank account opened | Month 3 | Swiss banking relationship established |

### 1.2 Grant applications

| Grant | Target Month | Amount | Status |
|:------|:------------|:-------|:-------|
| NLnet NGI Zero Core | Month 1 submitted | 50,000 EUR | Draft ready |
| NLnet NGI Zero Entrust | Month 1 submitted | 50,000 EUR | Draft ready |
| Ethereum Foundation ESP | Month 2 submitted | 150,000 USD | Outline ready |
| Arbitrum Foundation | Month 2 submitted | 500,000-1,000,000 USD | Drafting |
| Octant (quarterly) | Month 3 | 50,000-150,000 USD | Queued |
| EU Digital Europe Programme | Month 3 | 300,000-800,000 EUR | Preparing |

**Target by end of Phase 0:** At least 300,000 EUR secured or committed.

### 1.3 Team building

| Role | Target Month | Status |
|:-----|:------------|:-------|
| Technical lead (existing) | Month 0 | Sascha Daemgen |
| Protocol engineer (Go) | Month 2 | Recruiting |
| Legal/operations coordinator | Month 2 | Recruiting |
| Community manager (part-time) | Month 3 | Recruiting |
| Strategic advisors (2-3) | Month 3 | Identifying |

### 1.4 Documentation and communication

| Deliverable | Target Month | Status |
|:------------|:------------|:-------|
| Concept documentation | Month 0 | **This document set** |
| Landing page (simplego.dev/gonode) | Month 1 | Planning |
| Blog announcement | Month 1 | Drafting |
| Developer mailing list | Month 2 | Planning |
| First community AMA | Month 3 | Planning |

### 1.5 Success criteria (Phase 0)

Phase 0 is successful if all of these are true by month 3:

- [ ] Swiss Foundation incorporated
- [ ] Minimum 300,000 EUR grants secured or committed
- [ ] Minimum 3 team members including technical lead
- [ ] Complete concept documentation published
- [ ] Community AMA held with at least 100 attendees
- [ ] Legal opinion confirming structure

**If criteria not met:** Extend Phase 0 by up to 3 months. Re-evaluate funding strategy. Consider strategic round acceleration.

---

## 2. Phase 1: Permissioned testnet (Months 3-9)

**Goal:** Build permissioned testnet with selected operators. Ship first revenue-generating services. Validate technical architecture.

**Timeline:** July 2026 - January 2027

### 2.1 Technical milestones

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Core runtime alpha | Month 4 | Go binary: connects peers, stores messages |
| Swarm protocol implementation | Month 5 | Swarms form, replicate, maintain state |
| Reed-Solomon file sharding | Month 6 | Files split, distributed, reconstructed |
| Audit system prototype | Month 6 | HMAC challenges distributed and verified |
| Onion routing layer | Month 7 | 3-hop Sphinx routing operational |
| BFT appchain integration | Month 8 | Test appchain deployed with 5 validators |
| Permissioned testnet launch | Month 8 | 20 Foundation-selected operators |
| Testnet scale-up | Month 9 | 50 operators, 500 test users |

### 2.2 Smart contract development

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Contract specifications | Month 4 | Full Solidity interface drafts |
| Initial implementation | Month 5 | All 5 contracts coded and unit-tested |
| Internal security review | Month 6 | Internal code review complete |
| First external audit | Month 7 | One audit firm engaged, report delivered |
| Testnet deployment | Month 8 | Contracts on Arbitrum Sepolia |
| Bug fix iteration | Month 9 | Issues from testnet addressed |

### 2.3 Revenue milestones

**GoNode AI Developer Support launches (month 3):**

```
Month 3: Beta launch with 20 invited users
Month 4: Public launch, 50 users
Month 5: 75 users
Month 6: 100 users
Month 7: 150 users
Month 8: 200 users
Month 9: 300 users (conservative path to Year 1 target of 500)

Revenue trajectory:
Month 9 monthly revenue: ~6,000 EUR
Phase 1 total AI revenue: ~25,000 EUR
```

**First enterprise pilots (month 5-6):**

| Customer Type | Target | Month Signed |
|:--------------|:-------|:-------------|
| German government agency (pilot) | 1 | Month 5 |
| Privacy NGO | 1 | Month 6 |
| Healthcare provider (pilot) | 1 | Month 7 |
| Legal firm | 1 | Month 8 |

All pilots are free for 60-90 days, converting to paid SLA at end of Phase 1.

### 2.4 Community milestones

| Milestone | Target Month | Metric |
|:----------|:------------|:-------|
| Developer community (GoLab channel) | Month 4 | 500+ members |
| Weekly developer call established | Month 4 | Consistent attendance 20+ |
| Blog post cadence | Month 4 | 1 post/week |
| Conference presence | Month 6 | Talk at 36C3 or equivalent |
| Community bug bounty (testnet) | Month 7 | 10+ participants |

### 2.5 Funding milestones

| Milestone | Target Month | Amount |
|:----------|:------------|:-------|
| Arbitrum Foundation decision | Month 3-4 | 500k-1M USD |
| NLnet grants received | Month 4-5 | 50-100k EUR |
| Additional grants | Month 6-9 | 200k EUR |
| Total Phase 1 funding secured | Month 9 | 900k+ EUR |

### 2.6 Success criteria (Phase 1)

Phase 1 is successful if all of these are true by month 9:

- [ ] Permissioned testnet operational with 50+ operators
- [ ] All five smart contracts passed first security audit
- [ ] At least 3 paying enterprise pilots signed
- [ ] AI service reached 300+ paying users
- [ ] Cumulative Phase 1 revenue: 50,000+ EUR
- [ ] Arbitrum Foundation grant confirmed
- [ ] Team expanded to 6 FTE
- [ ] Zero critical security issues outstanding

**If criteria not met:** Extend Phase 1 by 3 months. Re-evaluate technical approach if fundamentals flawed. Consider scope reduction.

---

## 3. Phase 2: Public testnet (Months 9-15)

**Goal:** Open public testnet with incentive points. Complete MiCA whitepaper filing. Begin Pro subscription beta. Second security audit.

**Timeline:** January 2027 - July 2027

### 3.1 Technical milestones

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Client library API stable | Month 10 | SemVer 1.0 for Go client |
| Rust client implementation | Month 11 | Alternative client, 80%+ feature parity |
| Mobile client alpha | Month 12 | Android prototype integration |
| Public testnet launch | Month 11 | Permissionless participation |
| Incentive points system | Month 11 | Testnet participants earn points |
| Scaling tests | Month 13 | 500+ operators, 10,000+ test users |
| Performance optimization | Month 14 | Latency benchmarks published |
| Mainnet deployment rehearsal | Month 15 | End-to-end testnet migration drill |

### 3.2 MiCA compliance

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Whitepaper first draft | Month 10 | Internal review |
| Legal counsel review | Month 11 | External legal review complete |
| Community feedback period | Month 12 | Public review 30 days |
| Final whitepaper | Month 13 | Ready for submission |
| BaFin notification filed | Month 13 | 20+ business days before offer |
| Whitepaper published | Month 14 | simplego.dev/whitepaper |

### 3.3 Revenue milestones

**Pro subscription beta (month 12):**

```
Month 12: Beta launch, invited users only (free first month)
Month 13: Public launch, 5 EURC/month
Month 14: 300 paying subscribers
Month 15: 500 paying subscribers
```

**Enterprise SLA conversion (month 9-12):**

Pilots from Phase 1 convert to paid SLA contracts:

```
Month 9-10: 3 pilots convert to Starter tier (500 EUR/mo)
Month 11-12: 5 new pilots begin
Month 12-15: 2 new Business tier customers (1500 EUR/mo)
```

**Phase 2 total revenue target:** 250,000 EUR

### 3.4 Security and audits

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Second audit firm engaged | Month 10 | Trail of Bits / Consensys Diligence / similar |
| Second audit report | Month 13 | All findings addressed |
| Formal verification (optional) | Month 14 | Critical contract paths verified |
| Public bug bounty launched | Month 14 | Immunefi or equivalent platform |
| Penetration test | Month 15 | External pentest report |

### 3.5 Community and partnerships

| Milestone | Target Month | Metric |
|:----------|:------------|:-------|
| Developer community growth | Month 12 | 2,500+ members |
| Conference presence expanded | Month 9-15 | 3+ major conference talks |
| Ecosystem partnerships | Month 12 | 2+ integrations (wallet, exchange) |
| Media coverage | Month 13 | Major tech publication features |
| Operator community | Month 13 | Dedicated operator documentation, support |

### 3.6 Success criteria (Phase 2)

Phase 2 is successful if all of these are true by month 15:

- [ ] Public testnet with 500+ operators and 10,000+ users
- [ ] MiCA whitepaper filed with BaFin
- [ ] 500+ Pro subscribers paying 5 EURC/month
- [ ] 10+ enterprise customers signed
- [ ] Cumulative Phase 2 revenue: 250,000+ EUR
- [ ] Two independent security audits completed
- [ ] Rust client implementation operational
- [ ] Team expanded to 10 FTE

**If criteria not met:** Delay TGE by 3-6 months. Re-evaluate product-market fit. Consider pivoting specific services.

---

## 4. Phase 3: Mainnet and TGE (Months 15-24)

**Goal:** Launch mainnet. Execute Token Generation Event. Community airdrop. Transition to full economic model with Pro subscriptions in EURC on Arbitrum.

**Timeline:** July 2027 - April 2028

### 4.1 Pre-TGE preparation

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| TGE date announced | Month 15 | Community communication |
| Airdrop eligibility criteria | Month 16 | Published rules |
| Airdrop snapshot taken | Month 17 | SimpleGo/GoBot/GoLab users counted |
| Initial DEX liquidity secured | Month 18 | 500k EURC reserved |
| Market maker engagement | Month 18 | Term sheet signed |
| CEX listing applications | Month 19 | MEXC, Gate.io, BitMart, LBank submitted |
| Final smart contract deployment | Month 20 | Contracts deployed to Arbitrum mainnet |

### 4.2 TGE execution

**Launch sequence (Month 21):**

| Day | Activity |
|:----|:---------|
| Day -14 | Whitepaper final publication |
| Day -7 | Token contract verified on Arbiscan |
| Day 0 | 30M GC distributed per allocation |
| Day 0 | Uniswap V3 pool created (5M GC + 500k EURC) |
| Day 0 | Trading begins at 0.10 EURC per GC |
| Day 1 | Community airdrop claim period opens |
| Day 7 | Service Node Bonus Program begins |
| Day 14 | First CEX listing (MEXC) |
| Day 30 | Second CEX listing (Gate.io) |
| Day 30 | Reward distribution begins (first monthly payout) |

### 4.3 Network transition

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Testnet operators migrate to mainnet | Month 21 | 200+ operators staked |
| Bootstrap node deprecation | Month 22 | Foundation nodes removed from default list |
| Network fully community-operated | Month 22 | No Foundation dependency for messaging |
| First slashing event (if any) | Month 23 | System validated against real adversary |
| Performance parity with testnet | Month 24 | Latency, throughput meeting targets |

### 4.4 Revenue milestones (Phase 3)

**Pro subscription scaling:**

```
Month 15: 500 subscribers
Month 18: 1,500 subscribers
Month 21: 3,000 subscribers
Month 24: 5,000 subscribers

Revenue trajectory:
Month 18 monthly: 7,500 EUR
Month 21 monthly: 15,000 EUR
Month 24 monthly: 25,000 EUR
Phase 3 total Pro revenue: ~180,000 EUR
```

**Enterprise SLA scaling:**

```
Month 15: 10 customers
Month 21: 25 customers
Month 24: 45 customers

Revenue trajectory:
Phase 3 total enterprise revenue: ~550,000 EUR
```

**Phase 3 total revenue target:** 900,000 EUR

### 4.5 Ecosystem integration

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| GoBot migrates to GoNode infrastructure | Month 18 | All GoBot traffic via GoNode swarms |
| GoLab uses GoNode for fan-out | Month 19 | GoLab channels on GoNode swarms |
| GoKey hardware identity integration | Month 20 | Operators can bind to GoKey |
| GoUNITY certificates via GoNode | Month 22 | Certificates delivered via swarms |
| GoShop/GoTube/GoBook exploration | Month 24 | Integration feasibility studies |

### 4.6 Success criteria (Phase 3)

Phase 3 is successful if all of these are true by month 24:

- [ ] TGE executed successfully
- [ ] GoCoin trading on Uniswap and 2+ CEXs
- [ ] 200+ active mainnet operators
- [ ] 5,000+ Pro subscribers in EURC
- [ ] 45+ enterprise customers
- [ ] Total Phase 3 revenue: 900,000+ EUR
- [ ] Zero critical smart contract exploits
- [ ] Foundation treasury: 500,000+ EURC reserve

**If criteria not met:** Evaluate cause. If technical, iterate. If market, adjust positioning. TGE can be delayed but not repeated if executed poorly.

---

## 5. Phase 4: DAO transition (Months 24+)

**Goal:** Transition from Foundation-controlled to DAO-governed network. Burn deployer keys. Expand ecosystem integration.

**Timeline:** April 2028 onwards

### 5.1 Governance transition

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| DAO voting framework deployed | Month 25 | Smart contract for governance votes |
| First DAO vote (non-binding) | Month 26 | Community signals on fee parameter |
| Hybrid governance begins | Month 28 | DAO votes on fees, grants |
| Foundation retains protocol control | Months 24-36 | Veto on security-critical changes |
| Deployer keys burned | Month 36 | Phase 4 formally complete |
| Full DAO governance | Month 36 | All parameters via on-chain vote |

### 5.2 Protocol maturity

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| Protocol v1.0 finalised | Month 28 | Feature-complete, stable API |
| Third major audit | Month 30 | Comprehensive security review |
| Formal specification | Month 32 | Paper-quality protocol spec |
| Reference client in 3 languages | Month 34 | Go, Rust, TypeScript |
| Mobile clients (iOS + Android) | Month 36 | Native integrations |

### 5.3 Ecosystem expansion

| Milestone | Target Month | Deliverable |
|:----------|:------------|:------------|
| GoShop integration | Month 26-30 | E-commerce on GoNode |
| GoTube integration | Month 30-36 | Video platform on GoNode |
| GoBook integration | Month 36-42 | Publishing on GoNode |
| Third-party wallets | Ongoing | MetaMask, Rabby, Frame support |
| Exchange integrations | Ongoing | Coinbase, Binance, Kraken |
| Privacy-focused browser integration | Month 30 | Brave, Tor Browser |

### 5.4 Long-term financial targets (Years 3-5)

| Year | Revenue Target | Pro Subs | Enterprise | Notes |
|:-----|:--------------|:---------|:-----------|:------|
| Year 3 | 1,900,000 EUR | 12,000 | 47 | Approaching break-even |
| Year 4 | 4,640,000 EUR | 40,000 | 107 | **Operational profitability** |
| Year 5 | 11,000,000 EUR | 100,000 | 186 | Self-sustaining, no grants needed |

### 5.5 Success criteria (Phase 4, 12-month review)

Success by month 36:

- [ ] Deployer keys burned
- [ ] Full DAO governance operational
- [ ] 40,000+ Pro subscribers
- [ ] 100+ enterprise customers
- [ ] Annual revenue: 4,500,000+ EUR
- [ ] Foundation financially self-sustaining
- [ ] Zero critical incidents in past 12 months

---

## 6. Cross-phase commitments

### 6.1 Security commitments

Across all phases, GoNode commits to:

- Minimum 2 independent smart contract audits before mainnet
- Bug bounty program from Phase 2 onwards
- 90-day responsible disclosure timeline
- Security incidents publicly documented post-resolution
- No silent patches of security issues

### 6.2 Transparency commitments

- Monthly Foundation reports (financial status, metric updates)
- Quarterly community calls (open Q&A)
- Annual transparency report (operations, security, financial)
- All technical decisions documented publicly
- All grant usage reported to grantors

### 6.3 Decentralisation commitments

- Bootstrap nodes deprecated at Phase 3
- Deployer keys burned at Phase 4
- No single point of control post-Phase 4
- Foundation continues operations but without special privileges
- Geographic diversity encouraged via reward weighting

---

## 7. Risk-adjusted scenarios

### 7.1 Optimistic scenario

If all major grants succeed and market conditions are favorable:

| Metric | Acceleration |
|:-------|:-------------|
| TGE date | Month 18 (instead of 21) |
| Pro subscribers Year 3 | 25,000 (instead of 12,000) |
| Enterprise customers Year 3 | 80 (instead of 47) |
| Break-even | Year 3 (instead of Year 4) |
| DAO transition | Month 30 (instead of 36) |

### 7.2 Conservative scenario

If grants underperform and market conditions are harsh:

| Metric | Deceleration |
|:-------|:-------------|
| TGE date | Month 27 (instead of 21) |
| Pro subscribers Year 3 | 6,000 (instead of 12,000) |
| Enterprise customers Year 3 | 25 (instead of 47) |
| Break-even | Year 5 (instead of Year 4) |
| Additional funding needed | 500,000 EUR strategic round |

### 7.3 Pessimistic scenario

If major setbacks occur (legal challenge, security breach, team loss):

- Extend each phase by 3-6 months
- Reduce team temporarily (3 FTE core)
- Focus on revenue streams unaffected by setback
- Emergency foundation treasury supports 18-month runway extension
- DAO transition possibly simplified or delayed

**Key resilience factor:** Four diversified revenue streams mean any single setback does not threaten Foundation solvency.

---

## 8. Key dependencies

### 8.1 External dependencies

| Dependency | Risk | Mitigation |
|:-----------|:-----|:-----------|
| Arbitrum One operational | Low | Multi-chain deployment option if needed |
| Circle EURC availability | Low | USDC alternative, multiple stablecoins |
| BaFin responsive | Medium | Early engagement, professional counsel |
| Security audit firm availability | Low | Multiple qualified firms identified |
| Grant decisions | Medium | 6+ grants in parallel, 2-3 should succeed |

### 8.2 Internal dependencies

| Dependency | Risk | Mitigation |
|:-----------|:-----|:-----------|
| Founding team retention | Medium | Vesting schedules, token allocation |
| Hiring senior engineers | Medium | Competitive compensation + equity/token |
| Legal counsel availability | Low | Relationships established Phase 0 |
| Community building | Medium | Dedicated community manager from Phase 1 |

### 8.3 Technical dependencies

| Dependency | Risk | Mitigation |
|:-----------|:-----|:-----------|
| SimpleX protocol stability | Low | SimpleX is battle-tested, upstream stable |
| Go ecosystem maturity | Low | Proven at scale (K8s, Docker, etc.) |
| Reed-Solomon libraries | Low | klauspost/reedsolomon production-tested |
| Post-quantum crypto | Medium | ML-KEM stable, fallback to classical if issues |

---

## 9. Milestone tracking

### 9.1 Monthly cadence

Every month, the Foundation publishes:

- Progress against roadmap milestones (green/yellow/red)
- Financial summary (revenue, costs, runway)
- User metrics (operators, subscribers, usage)
- Security status (incidents, audits, bug bounty)
- Upcoming milestones next 30 days

### 9.2 Quarterly reviews

Every quarter, the Foundation:

- Reviews phase progress against success criteria
- Adjusts roadmap if material deviation
- Conducts strategic review with Board and advisors
- Publishes quarterly report to community
- Holds community call for Q&A

### 9.3 Annual retrospectives

Every year, the Foundation:

- Commissions independent audit of progress
- Reviews ecosystem health (competitive, regulatory, technical)
- Publishes comprehensive annual report
- Plans next year's execution in detail
- Refreshes long-term vision if needed

---

## 10. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [GoNode Concept](CONCEPT.md) | Strategic rationale for roadmap | This repo |
| [GoNode Business Model](BUSINESS_MODEL.md) | Revenue targets underlying roadmap | This repo |
| [GoNode Tokenomics](TOKENOMICS.md) | TGE details and token economics | This repo |
| [GoNode Legal Compliance](LEGAL_COMPLIANCE.md) | Regulatory milestones | This repo |
| [Season Index](seasons/SEASON-INDEX.md) | Detailed season documentation | This repo |

---

*GoNode Roadmap v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
