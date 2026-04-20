# GoNode Roadmap

**Document version:** Season 1 | April 2026
**Component:** Execution timeline from concept to operational network
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This roadmap describes the 5-phase execution plan for GoNode, from concept through operational network and ecosystem expansion. The timeline reflects the redesigned loyalty system model (no Token Generation Event, no DEX liquidity milestone, no CEX listings). Milestones focus on infrastructure readiness, user adoption, and marketplace maturity.

**Important:** This is a projection, not a commitment. Timelines depend on funding, team availability, regulatory developments, and market conditions. Milestones may shift as reality informs planning.

**Execution philosophy:**

- **Build values first.** Create real utility before worrying about loyalty points, marketing, or community scale.
- **Revenue before features.** Each phase must produce revenue or clear path to revenue before advancing.
- **Ship small, ship often.** Prefer small releases over big bang launches.
- **Decentralisation progressively.** Start with Foundation-operated infrastructure; transition to operator-run as network matures.

---

## Timeline at a glance

```
Phase 0: Foundation and concept
    Months 0-3
    Legal setup, initial team, grant applications

Phase 1: Core infrastructure
    Months 3-9
    Internal alpha, first paying users, AI services live

Phase 2: Operator rewards and testnet
    Months 9-15
    Operator onboarding, public testnet, loyalty ledger live

Phase 3: Marketplace launch
    Months 15-21
    Peer-to-peer marketplace, full DSA compliance, scale-up

Phase 4: Scale and ecosystem expansion
    Months 21-36+
    Multi-product, international expansion, maturity
```

---

## Phase 0: Foundation and concept

**Timing:** Months 0-3
**Objective:** Establish legal foundation, core team, and funding pipeline. Nothing ships publicly yet.

### Key activities

**Legal and entity:**
- IT and More Systems GmbH documentation updated for GoNode activity
- Legal opinion commissioned on loyalty program classification (PSD2 Art. 3(k), ZAG § 2)
- Terms of Service drafted for users and operators
- Privacy policy aligned with GDPR
- Trademark applications filed (GoCoin, GoNode, SimpleGo)

**Team building:**
- Core technical team identified
- Legal counsel retained
- Accounting and tax advisor retained
- Advisory board approached

**Funding pipeline:**
- Grant applications drafted and submitted to EU Digital Europe, NLnet, Sovereign Tech Fund, BMBF
- Strategic investor conversations where appropriate
- Bootstrapping plan finalised

**Documentation and community:**
- Repository maintained and refined based on community feedback
- Initial community channel established separately from SimpleGo main channel
- First community announcements
- FAQ developed based on early reactions

### Success criteria

- Legal opinion received confirming loyalty classification
- Terms of Service drafted and reviewed
- Core team committed
- At least 2 grant applications submitted
- Initial community space active
- Path to initial funding identified

### Risks at this phase

- Legal opinion raises issues requiring design changes (mitigation: conservative design staying within established precedent)
- Team recruitment slower than expected (mitigation: remote-friendly, community-driven)
- Grant process slow (mitigation: multiple applications in parallel, bootstrapping cushion)

---

## Phase 1: Core infrastructure

**Timing:** Months 3-9
**Objective:** Build core GoNode infrastructure. First internal testing. First paying customers. AI Developer Support service live to generate early revenue.

### Key activities

**Technical development:**
- GoNode service node runtime (Rust implementation of SMP)
- Loyalty ledger (PostgreSQL implementation, see SMART_CONTRACTS.md)
- Initial wire protocol implementation
- Authentication via GoUNITY certificates
- Core API endpoints for clients
- Basic admin tools

**Loyalty system:**
- Account creation flows
- Earning mechanics for purchases (bonus calculation)
- Basic redemption catalog (initial special editions)
- Foundation reserve allocation
- Transaction logging and audit trail

**Client integration:**
- SimpleGo client updated to use GoNode infrastructure (where available)
- Pro subscription flow
- Basic user dashboard
- Balance and transaction history views

**Revenue activation:**
- AI Developer Support service launched (first revenue)
- Pro subscription billing via SEPA / card / PayPal
- First enterprise prospects engaged
- Marketing content published

**Operations:**
- Monitoring infrastructure deployed
- Backup and disaster recovery tested
- First external security audit commissioned
- Support ticket system live

### Success criteria

- 3 bootstrap nodes operational (Foundation-run)
- Loyalty ledger processing test transactions
- 100+ active users on Pro (paid)
- First AI Services revenue booked
- First enterprise pilot discussion
- Security audit completed

### What users see

- Basic Pro features work reliably
- They can earn and view GoCoin balance
- They can redeem coins for a small selection of special items
- Customer support responds within 72 hours

### What operators see

- Not yet - operators join in Phase 2

### Risks at this phase

- Technical complexity higher than estimated (mitigation: smaller scope, more iteration)
- User acquisition slower than planned (mitigation: tight focus on early adopters, word-of-mouth)
- AI Services slow to close first deals (mitigation: leverage existing network, price for learning)

---

## Phase 2: Operator rewards and testnet

**Timing:** Months 9-15
**Objective:** Onboard external operators, launch public testnet, start monthly operator rewards. Prepare for marketplace launch.

### Key activities

**Operator program:**
- Operator application process opened
- 20-50 operators onboarded across Phase 2
- Operator dashboard for performance metrics and earnings
- Monthly reward calculation and distribution (automated)
- 30-day holding period mechanics live
- Operator community channel active

**Technical expansion:**
- Swarm coordination fully operational
- 3-hop Sphinx onion routing tested in production
- Reed-Solomon erasure coding for file storage
- Audit challenge protocol running hourly
- Automatic fragment redistribution

**Loyalty system expansion:**
- Community reward mechanism
- Expanded redemption catalog
- Operator earnings statements (for tax reporting)
- BaFin notification submitted (if volume above 1M EUR)
- Transparency reports started (monthly)

**User experience:**
- Pro+ tier introduced
- Hardware bundle options (with GoKey integration)
- Multi-device sync
- Improved onboarding flow

**Business development:**
- 3-5 enterprise pilot customers signed
- AI Services at 500k EUR annualised run-rate
- First hardware partnerships explored

### Success criteria

- 20+ external operators earning rewards
- 3,000+ Pro subscribers
- Monthly transparency reports published
- All Phase 2 technical milestones operational
- Monthly revenue exceeding 100k EUR
- DSA notice-and-action mechanism live

### What users see

- Faster, more reliable service as operator network grows
- Expanded features with Pro+
- Larger redemption catalog
- First community-generated content

### What operators see

- Clear earnings dashboard
- Monthly GoCoin receipts with EUR equivalents
- Performance metrics
- Community recognition for good operators

### Risks at this phase

- Operator uptake slower than expected (mitigation: reduce technical barrier, improve documentation, early operator bonuses)
- DSA compliance complexity higher than planned (mitigation: focus on minimum viable compliance, expand incrementally)
- Technical issues in production (mitigation: gradual rollout, feature flags, rollback capability)

---

## Phase 3: Marketplace launch

**Timing:** Months 15-21
**Objective:** Launch the peer-to-peer marketplace. Enable trading between users. Full DSA compliance. Scale the network.

### Key activities

**Marketplace development:**
- Listing creation and management
- Auction mechanics (timed bidding)
- Barter mechanics (coin-for-item trades)
- Escrow service for trades
- Dispute resolution workflow
- Marketplace moderation tools

**DSA full compliance:**
- Notice-and-action mechanism fully operational
- Statement of reasons for moderation actions
- Internal complaint handling
- Trader traceability (for commercial users)
- Annual transparency report prepared
- External dispute resolution body identified

**Scale infrastructure:**
- 500+ operators network
- Geographic diversity achieved
- 10,000+ active users
- Enterprise SLA tier formalised (99.9% availability)
- 24/7 monitoring operational

**DAC7 reporting:**
- Platform operator registration
- User TIN collection above thresholds
- Annual report to BZSt prepared
- User notification workflow

**Decision point: permissioned blockchain**
- Evaluate community demand for on-chain transparency
- Assess technical maturity of options (Hyperledger Fabric)
- Cost-benefit analysis
- Decision: proceed to Phase 4 with database only, or plan migration

### Success criteria

- Marketplace live with 1000+ listings
- 10,000+ Pro subscribers
- 15+ enterprise customers
- All DSA obligations met and documented
- First annual transparency report published
- Operating break-even achieved or imminent

### What users see

- Full ecosystem experience: earn, redeem, trade
- Active marketplace with diverse items
- Clear dispute resolution when issues arise
- Transparent moderation

### What operators see

- Mature ecosystem driving demand
- Stable earnings
- Community status and recognition
- Access to operator-only benefits

### Risks at this phase

- Marketplace abuse (mitigation: strong moderation, volume thresholds, audit logs)
- Disputes overwhelm resolution capacity (mitigation: automation where possible, clear rules, escalation paths)
- Scaling bottlenecks (mitigation: load testing, capacity planning, autoscaling)

---

## Phase 4: Scale and ecosystem expansion

**Timing:** Months 21-36+
**Objective:** Scale the network. Expand the ecosystem. Evaluate international expansion and multi-product strategy.

### Key activities

**Ecosystem expansion:**
- GoShop (ecommerce using SimpleGo infrastructure) launched
- GoTube (video sharing) beta
- GoBook (social networking) beta
- Integration between ecosystem products
- Cross-product loyalty program

**International expansion:**
- Evaluation of other EU markets (France, Netherlands, Spain, Italy)
- Localised Terms of Service and legal framework
- Regional community managers
- Multi-language support

**Advanced features:**
- Permissioned blockchain migration (if decided in Phase 3)
- Advanced cryptographic features (threshold signatures, MPC)
- Hardware roadmap: next-gen SimpleGo devices
- Enterprise premium tier with custom integration

**Business maturity:**
- 100,000+ Pro subscribers target
- 50+ enterprise customers
- 1,500+ operators
- Strong cash flow supporting reinvestment
- Independent board of advisors

**Community governance:**
- Community input on major decisions
- Operator representation in governance
- Transparent change management
- Annual in-person event

### Success criteria

- Multi-product ecosystem live and growing
- 100,000+ Pro subscribers
- International presence in 3+ EU countries
- Profitability sustained
- Community health strong (NPS, participation metrics)

### What users see

- Rich ecosystem with multiple products
- Seamless integration between apps
- International language and features
- Strong community and governance

### What operators see

- Stable, growing network
- Clear advancement paths (entry → standard → enterprise tier)
- Recognition and rewards
- Voice in governance

### Risks at this phase

- Ecosystem fragmentation (mitigation: unified architecture, shared loyalty, common brand)
- International complexity (mitigation: focus on one country at a time, legal review per market)
- Competition from larger players (mitigation: differentiation through hardware, privacy, community)

---

## Revenue milestones

Each phase has revenue targets aligned with business sustainability:

| Phase | Timing | Monthly Revenue Target | Annual Run-rate |
|:------|:-------|:----------------------|:----------------|
| 0 | Months 0-3 | 0 - 5k EUR | 0 - 60k EUR (grants only) |
| 1 | Months 3-9 | 5k - 50k EUR | 60k - 600k EUR |
| 2 | Months 9-15 | 50k - 200k EUR | 600k - 2.4M EUR |
| 3 | Months 15-21 | 200k - 400k EUR | 2.4M - 4.8M EUR |
| 4 | Months 21-36+ | 400k - 1M+ EUR | 4.8M - 12M+ EUR |

Revenue streams active at each phase:

- **Phase 1:** AI Services, first Pro subscriptions
- **Phase 2:** + Enterprise SLAs, hardware bundles
- **Phase 3:** + Marketplace fees (modest)
- **Phase 4:** + Multi-product revenue

---

## Team growth

Target team size at each phase:

| Phase | Team Size | Key Additions |
|:------|:----------|:--------------|
| 0 | 2-3 FTE | Founder + core engineers |
| 1 | 6-8 FTE | Full engineering, first ops |
| 2 | 10-12 FTE | Community, compliance, business |
| 3 | 13-14 FTE | DSA/compliance, marketplace ops |
| 4 | 14-18 FTE | International, ecosystem |

Hiring priorities at each phase:

- **Phase 0:** Legal counsel, senior Rust engineer
- **Phase 1:** Additional engineers, first customer support
- **Phase 2:** Compliance, community manager
- **Phase 3:** Marketplace operations, moderation
- **Phase 4:** International, product managers

---

## Technical milestones

Critical technical milestones by phase:

### Phase 0 (Months 0-3)
- Repository structure finalised
- Development environment documented
- Initial technical specifications published

### Phase 1 (Months 3-9)
- SMP Rust implementation (SimpleGoX) functional
- GoNode node runtime operational
- PostgreSQL loyalty ledger live
- First internal deployment

### Phase 2 (Months 9-15)
- Swarm coordination in production
- Sphinx onion routing tested at scale
- Reed-Solomon erasure coding operational
- GoKey hardware integration complete
- 50+ operators onboarded

### Phase 3 (Months 15-21)
- Marketplace operational
- DSA full compliance
- DAC7 reporting infrastructure
- 500+ operators
- Post-quantum hybrid handshakes default

### Phase 4 (Months 21-36+)
- Multi-product ecosystem integration
- Permissioned blockchain migration (if elected)
- International deployments
- 1,500+ operators
- Advanced cryptographic features

---

## Regulatory milestones

Compliance milestones aligned with operational growth:

### Phase 0-1
- Terms of Service drafted and published
- Privacy policy live
- GDPR compliance baseline

### Phase 2
- BaFin notification submitted if transaction volume exceeds 1M EUR
- First annual transparency report
- Operator earnings statements for tax reporting

### Phase 3
- Full DSA Art. 16 notice-and-action mechanism
- Full DSA Art. 30 traceability (for commercial users)
- DAC7 first annual report to BZSt
- External compliance audit

### Phase 4
- Multi-country compliance alignment
- Enhanced compliance for larger scale
- Review of permissioned blockchain regulatory status (if elected)
- Advisory board with regulatory expertise

---

## Community milestones

Community development aligned with product phases:

### Phase 0 (Months 0-3)
- Dedicated GoNode community space active
- First 100 engaged community members
- Clear community guidelines
- Moderator team identified

### Phase 1 (Months 3-9)
- Monthly community updates
- First community contributions accepted
- Regular Q&A sessions
- Community-driven feature requests process

### Phase 2 (Months 9-15)
- Operator community subdivision
- Community documentation contributions
- Bug bounty program live
- First community-organised events

### Phase 3 (Months 15-21)
- Marketplace community active
- Content creator program
- Community-designed special editions
- International community chapters

### Phase 4 (Months 21-36+)
- Community governance mechanisms
- Annual in-person conference
- Community-led initiatives
- Developer ecosystem around SDKs

---

## Risk-adjusted scenarios

Three scenarios for how the roadmap might actually unfold:

### Optimistic scenario
- Grants successfully secured in Phase 0
- Strong word-of-mouth drives user growth
- Enterprise sales close faster than expected
- Community grows organically
- Phase 3 marketplace launches 3 months early
- Break-even in Year 2.5

### Base scenario (as described above)
- Moderate grant success
- Steady user growth matching projections
- Normal enterprise sales cycle
- Community development as planned
- Phase 3 marketplace launches on time
- Break-even in Year 3

### Conservative scenario
- Grants slower than expected
- User growth 50% of projection
- Enterprise sales 6-12 months behind
- Community more niche than mass market
- Phase 3 marketplace delayed by 6 months
- Break-even in Year 4
- Additional bootstrapping required

All three scenarios remain economically viable because the model does not depend on token markets or speculative assets. Slower growth just means slower expansion, not existential risk.

---

## What we explicitly will not do

Things that are tempting but would compromise the model:

- **No Token Generation Event.** The loyalty system replaces the need for this entirely.
- **No DEX liquidity provision.** Foundation never provides liquidity.
- **No CEX listings.** GoCoin does not trade on any exchange.
- **No external trading markets.** Coins stay in the closed loop.
- **No conversion to EUR by Foundation.** Users cannot cash out coins through us.
- **No aggressive user acquisition.** Organic growth aligned with infrastructure capacity.
- **No premature internationalisation.** Master Germany/EU first.
- **No feature creep.** Focus on core privacy infrastructure.
- **No compromise on open source.** All code remains AGPL-3.0.
- **No surveillance partnerships.** Zero-knowledge architecture is a design invariant.

---

## Decision points

Key decisions that need to be made at specific milestones:

### End of Phase 0 (Month 3)
- Confirm legal classification approach
- Commit funding sources
- Lock initial team composition
- Ratify technical architecture

### End of Phase 1 (Month 9)
- Assess product-market fit early signals
- Decide on Phase 2 operator program design
- Evaluate technical debt and refactoring needs
- Ratify compliance framework

### End of Phase 2 (Month 15)
- Marketplace go/no-go decision
- DSA compliance readiness assessment
- International expansion timing
- Hardware roadmap confirmation

### End of Phase 3 (Month 21)
- Permissioned blockchain decision
- Phase 4 scope definition
- Ecosystem expansion priorities
- Capital strategy (profit reinvestment vs. additional raise)

### During Phase 4 (Months 21-36+)
- International expansion targets
- Multi-product launch sequence
- Governance evolution
- Exit strategy considerations

---

## Status reporting cadence

To maintain transparency and accountability:

- **Monthly:** Community update on progress (blog post + community channel)
- **Quarterly:** Detailed progress report with metrics
- **Semi-annually:** Season retrospective (see SEASON-INDEX.md)
- **Annually:** Full year-in-review with strategic assessment

Each report covers:

- Progress against roadmap milestones
- Metrics against targets
- Lessons learned
- Adjusted projections
- Open questions for community input

---

## Related documents

| Document | Relevance |
|:---------|:----------|
| [README](../README.md) | Project overview |
| [Concept](CONCEPT.md) | Strategic rationale |
| [Architecture and Security](ARCHITECTURE_AND_SECURITY.md) | Technical foundation |
| [Tokenomics](TOKENOMICS.md) | Loyalty system details |
| [Business Model](BUSINESS_MODEL.md) | Revenue and costs |
| [Legal Compliance](LEGAL_COMPLIANCE.md) | Regulatory framework |
| [Smart Contracts](SMART_CONTRACTS.md) | Ledger implementation |
| [Seasons Index](seasons/SEASON-INDEX.md) | Retrospectives per season |

---

*GoNode Roadmap v2 - April 2026 (redesigned for loyalty system)*
*IT and More Systems, Recklinghausen, Germany*
