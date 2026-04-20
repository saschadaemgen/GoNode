# GoNode Ledger Architecture

**Document version:** Season 1 | April 2026
**Component:** GoCoin ledger technical specification (database and optional permissioned blockchain)
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

> **Note on naming:** This document was previously titled "Smart Contracts" when GoCoin was designed as an ERC-20 token on Arbitrum. Following the redesign to a closed-loop loyalty system, the file name is retained for cross-reference stability, but the contents now describe the loyalty ledger architecture - either a relational database (Phase 1) or an optional permissioned blockchain (Phase 3+). No Solidity smart contracts are deployed in the new design.

---

## Overview

The GoCoin ledger tracks loyalty point balances, issuances, redemptions, and peer-to-peer transfers for all users and operators in the SimpleGo ecosystem. The design prioritises simplicity, legal clarity, operational reliability, and user experience over blockchain ideology.

Two implementation paths are defined:

- **Phase 1 (initial):** Relational database (PostgreSQL) - simple, fast, well-understood, aligned with how all major loyalty programs operate (Payback, Miles & More, Steam Wallet)
- **Phase 3+ (optional):** Permissioned blockchain (Hyperledger Fabric or similar) - for additional transparency and tamper-evidence if community demand warrants

Both paths produce the same legal classification (closed-loop loyalty under PSD2 Art. 3(k) / ZAG § 2), the same user experience, and the same business behaviour. The choice is operational, not regulatory.

---

## 1. Core design principles

### 1.1 Simplicity over complexity

The loyalty ledger is the opposite of the previous smart contract design:

| Old design | New design |
|:-----------|:-----------|
| 5 Solidity contracts on Arbitrum | 1 database or 1 permissioned chain |
| 1,088 lines of Solidity | ~500 lines of application code |
| Gas fees on every operation | Free operations |
| Immutable after deployment | Update normally with software releases |
| Required audits at 50-200k EUR each | Standard software testing |
| MEV concerns, flash loan risks | Not applicable |
| Private key management | Standard authentication |

### 1.2 Legal clarity

The design deliberately avoids any features that could trigger crypto-asset classification:

- No public blockchain
- No cryptographic proof of balance "ownership" (database record, not token)
- No transferability outside the system
- No external interoperability with crypto wallets
- No backing by other assets
- No bearer-instrument properties

### 1.3 User experience

Users interact with GoCoin like Payback points or Steam Wallet credits:

- View balance in account dashboard
- See transaction history
- Click to redeem for items
- Post offers on marketplace
- No wallet software, no seed phrases, no gas fees

### 1.4 Operational reliability

Standard enterprise software practices:

- Daily backups with point-in-time recovery
- High availability with failover
- Monitoring and alerting
- Standard disaster recovery procedures
- Audit logs for all operations

---

## 2. Phase 1: Database architecture

### 2.1 Technology stack

| Layer | Choice | Rationale |
|:------|:-------|:----------|
| Database | PostgreSQL 16+ | ACID compliance, mature, free, widely known |
| Application | Go (Golang) | Consistent with GoNode stack, performant |
| API | REST + GraphQL | Standard integration patterns |
| Authentication | GoUNITY certificates | Consistent with ecosystem identity |
| Deployment | Kubernetes | Standard container orchestration |
| Backups | pgBackRest + offsite | Hourly incremental, daily full |

### 2.2 Schema overview

The core schema consists of seven tables:

**accounts** - User and operator accounts
```sql
CREATE TABLE accounts (
    account_id UUID PRIMARY KEY,
    account_type VARCHAR(20) NOT NULL CHECK (account_type IN ('user', 'operator', 'foundation')),
    identifier_hash BYTEA NOT NULL,              -- hashed link to GoUNITY identity
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    status VARCHAR(20) NOT NULL DEFAULT 'active' CHECK (status IN ('active', 'suspended', 'closed')),
    metadata JSONB,                              -- flexible additional info
    UNIQUE (identifier_hash)
);
```

**balances** - Current GoCoin balance per account
```sql
CREATE TABLE balances (
    account_id UUID PRIMARY KEY REFERENCES accounts(account_id),
    amount BIGINT NOT NULL DEFAULT 0 CHECK (amount >= 0),
    locked_amount BIGINT NOT NULL DEFAULT 0 CHECK (locked_amount >= 0),  -- coins on marketplace holds
    holding_period_release_at TIMESTAMPTZ,        -- for operator earnings
    last_updated TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

**transactions** - Immutable audit log of all coin movements
```sql
CREATE TABLE transactions (
    tx_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tx_type VARCHAR(30) NOT NULL,    -- earn_purchase, earn_operator, earn_community, redeem, transfer, burn
    from_account_id UUID REFERENCES accounts(account_id),
    to_account_id UUID REFERENCES accounts(account_id),
    amount BIGINT NOT NULL CHECK (amount > 0),
    reference_id VARCHAR(100),         -- link to purchase, redemption, etc.
    timestamp TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    metadata JSONB,
    CONSTRAINT from_or_system CHECK (from_account_id IS NOT NULL OR tx_type LIKE 'earn_%')
);

CREATE INDEX idx_tx_from ON transactions(from_account_id);
CREATE INDEX idx_tx_to ON transactions(to_account_id);
CREATE INDEX idx_tx_type_time ON transactions(tx_type, timestamp);
```

**issuance_log** - Tracks total supply against cap
```sql
CREATE TABLE issuance_log (
    log_id SERIAL PRIMARY KEY,
    category VARCHAR(30) NOT NULL,   -- purchase_reward, operator_reward, community, reserve
    amount BIGINT NOT NULL,
    timestamp TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    cumulative_issued BIGINT NOT NULL,
    notes TEXT
);
```

**redemptions** - Items redeemed by users
```sql
CREATE TABLE redemptions (
    redemption_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    account_id UUID NOT NULL REFERENCES accounts(account_id),
    item_sku VARCHAR(100) NOT NULL,
    coin_cost BIGINT NOT NULL,
    status VARCHAR(20) NOT NULL DEFAULT 'pending',
    redeemed_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    fulfilled_at TIMESTAMPTZ,
    tx_id UUID REFERENCES transactions(tx_id)
);
```

**marketplace_listings** - Active P2P offers
```sql
CREATE TABLE marketplace_listings (
    listing_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    seller_account_id UUID NOT NULL REFERENCES accounts(account_id),
    listing_type VARCHAR(30) NOT NULL,   -- auction, fixed, barter
    offered_item JSONB NOT NULL,          -- description of what's offered
    asking_price JSONB NOT NULL,          -- what the seller wants in return
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    expires_at TIMESTAMPTZ,
    status VARCHAR(20) NOT NULL DEFAULT 'active',
    completed_at TIMESTAMPTZ
);

CREATE INDEX idx_listings_active ON marketplace_listings(status, created_at) WHERE status = 'active';
```

**audit_log** - Compliance-grade audit trail
```sql
CREATE TABLE audit_log (
    audit_id BIGSERIAL PRIMARY KEY,
    event_type VARCHAR(50) NOT NULL,
    actor_id UUID REFERENCES accounts(account_id),
    target_type VARCHAR(50),
    target_id UUID,
    details JSONB NOT NULL,
    timestamp TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    ip_hash BYTEA                          -- hashed IP for abuse prevention
);

CREATE INDEX idx_audit_time ON audit_log(timestamp);
CREATE INDEX idx_audit_actor ON audit_log(actor_id, timestamp);
```

### 2.3 Core operations

**Earning coins from a purchase:**

```sql
-- atomic transaction
BEGIN;

-- 1. Verify purchase is valid (from payment processor webhook)
SELECT verify_payment_confirmed(:payment_id);

-- 2. Calculate loyalty reward based on purchase type
SELECT calculate_reward(:payment_type, :payment_amount) INTO :reward_amount;

-- 3. Record the transaction
INSERT INTO transactions (tx_type, to_account_id, amount, reference_id, metadata)
VALUES ('earn_purchase', :account_id, :reward_amount, :payment_id,
        jsonb_build_object('payment_type', :payment_type, 'payment_amount', :payment_amount));

-- 4. Update balance
UPDATE balances
SET amount = amount + :reward_amount, last_updated = NOW()
WHERE account_id = :account_id;

-- 5. Update issuance log
INSERT INTO issuance_log (category, amount, cumulative_issued)
SELECT 'purchase_reward', :reward_amount,
       COALESCE((SELECT cumulative_issued FROM issuance_log ORDER BY log_id DESC LIMIT 1), 0) + :reward_amount;

-- 6. Write audit log
INSERT INTO audit_log (event_type, actor_id, target_type, target_id, details)
VALUES ('coin_earned', NULL, 'account', :account_id,
        jsonb_build_object('amount', :reward_amount, 'source', 'purchase'));

COMMIT;
```

**Operator monthly rewards:**

```sql
-- Batch operation run by cron monthly
INSERT INTO transactions (tx_type, to_account_id, amount, reference_id, metadata)
SELECT 'earn_operator',
       op.account_id,
       calculate_operator_reward(op.uptime_pct, op.audit_score, op.data_volume),
       'monthly_reward_' || TO_CHAR(NOW(), 'YYYY_MM'),
       jsonb_build_object('uptime', op.uptime_pct, 'month', TO_CHAR(NOW(), 'YYYY-MM'))
FROM operator_performance op
WHERE op.month = DATE_TRUNC('month', NOW() - INTERVAL '1 month');

-- Apply 30-day holding period
UPDATE balances
SET holding_period_release_at = NOW() + INTERVAL '30 days'
WHERE account_id IN (SELECT to_account_id FROM transactions WHERE tx_type = 'earn_operator' AND timestamp > NOW() - INTERVAL '1 hour');
```

**Redeeming coins:**

```sql
BEGIN;

-- 1. Check balance
SELECT amount INTO :current_balance FROM balances WHERE account_id = :account_id FOR UPDATE;

IF :current_balance < :item_cost THEN
    ROLLBACK;
    RAISE EXCEPTION 'Insufficient balance';
END IF;

-- 2. Deduct from balance
UPDATE balances SET amount = amount - :item_cost WHERE account_id = :account_id;

-- 3. Record transaction (burn)
INSERT INTO transactions (tx_type, from_account_id, amount, reference_id, metadata)
VALUES ('redeem', :account_id, :item_cost, :item_sku,
        jsonb_build_object('item', :item_sku));

-- 4. Create redemption record
INSERT INTO redemptions (account_id, item_sku, coin_cost, status)
VALUES (:account_id, :item_sku, :item_cost, 'pending');

-- 5. Queue fulfillment
INSERT INTO fulfillment_queue (redemption_id, priority) VALUES (...);

COMMIT;
```

**Peer-to-peer marketplace transfer:**

```sql
BEGIN;

-- 1. Lock the listing
UPDATE marketplace_listings SET status = 'pending' WHERE listing_id = :listing_id AND status = 'active';

-- 2. Verify both parties have required items
-- (Details depend on specific item types)

-- 3. Execute the swap atomically
-- Case: buyer pays GoCoin, seller delivers item
UPDATE balances SET amount = amount - :coin_amount WHERE account_id = :buyer_id;
UPDATE balances SET amount = amount + (:coin_amount - :marketplace_fee) WHERE account_id = :seller_id;

-- 4. Record transactions
INSERT INTO transactions (tx_type, from_account_id, to_account_id, amount, reference_id)
VALUES ('transfer', :buyer_id, :seller_id, :coin_amount - :marketplace_fee, :listing_id),
       ('burn', :buyer_id, NULL, :marketplace_fee, 'marketplace_fee_' || :listing_id);

-- 5. Transfer the item (update item ownership records)
UPDATE items SET owner_id = :buyer_id WHERE item_id = :item_id;

-- 6. Complete listing
UPDATE marketplace_listings SET status = 'completed', completed_at = NOW() WHERE listing_id = :listing_id;

COMMIT;
```

### 2.4 Supply cap enforcement

The 100M GoCoin soft cap is enforced at the application layer:

```sql
CREATE OR REPLACE FUNCTION check_supply_cap()
RETURNS TRIGGER AS $$
DECLARE
    current_supply BIGINT;
    supply_cap CONSTANT BIGINT := 100000000;  -- 100M GoCoin
BEGIN
    IF NEW.tx_type LIKE 'earn_%' THEN
        SELECT cumulative_issued INTO current_supply FROM issuance_log ORDER BY log_id DESC LIMIT 1;
        IF (current_supply + NEW.amount) > supply_cap THEN
            RAISE EXCEPTION 'Supply cap would be exceeded';
        END IF;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER enforce_supply_cap
BEFORE INSERT ON transactions
FOR EACH ROW EXECUTE FUNCTION check_supply_cap();
```

### 2.5 Performance targets

| Operation | Target latency | Target throughput |
|:----------|:---------------|:------------------|
| Balance lookup | <5ms | 10,000+ req/s |
| Earn transaction | <50ms | 1,000 req/s |
| Redemption | <100ms | 500 req/s |
| Marketplace listing | <200ms | 100 req/s |
| Marketplace trade | <500ms | 50 req/s |
| Monthly batch (operator rewards) | <5 minutes | 10,000 operators |

PostgreSQL easily handles these loads with standard hardware and appropriate indexing.

### 2.6 High availability

**Replication:**
- Streaming replication to 2 standby nodes
- Automatic failover via repmgr or Patroni
- Target RTO: 60 seconds
- Target RPO: 0 (synchronous replication to primary standby)

**Geographic distribution:**
- Primary: Germany (Frankfurt datacenter)
- Secondary: Germany (Hamburg datacenter)
- Backup: EU (Amsterdam, read-only)

**Monitoring:**
- Prometheus + Grafana stack
- Alerting on replication lag, query performance, disk usage
- 24/7 on-call rotation after Phase 2

### 2.7 Backup and recovery

**Backup strategy:**
- Hourly incremental backups (pgBackRest)
- Daily full backups to offsite storage
- Weekly cold backup to separate region
- Backup integrity verified weekly

**Recovery procedures:**
- Point-in-time recovery tested monthly
- Full disaster recovery test quarterly
- Target RTO: 4 hours for complete system rebuild
- Documentation kept current with infrastructure

### 2.8 Data retention

In line with GDPR and German commercial law:

| Data | Retention | Reason |
|:-----|:----------|:-------|
| Active balances | Ongoing | Service continuity |
| Transaction records | 10 years | HGB § 257, AO § 147 |
| Audit logs | 5 years | DSA compliance |
| Marketplace listings | 2 years after close | Dispute resolution |
| Account metadata | Until account closure + 30 days | User convenience |

---

## 3. Phase 3+ (optional): Permissioned blockchain

If strategic need arises (community demand for transparency, enterprise requirement for verifiable ledger, regulatory preference), a permissioned blockchain implementation is available as Phase 3+ option.

### 3.1 Technology evaluation

Three candidates evaluated:

| Technology | Pros | Cons |
|:-----------|:-----|:-----|
| Hyperledger Fabric | Mature, Linux Foundation backing, strong enterprise adoption | Complex setup, steeper learning curve |
| Hyperledger Besu | Ethereum-compatible, familiar to developers, simpler | Less specialized for permissioned use |
| R3 Corda | Designed for financial use cases | Smaller community, licensing complexity |

**Preferred candidate:** Hyperledger Fabric, based on maturity and alignment with loyalty program use case.

### 3.2 Architecture principles

If implemented, the permissioned chain would:

- Run validator nodes operated by a trusted consortium (Foundation + 3-5 partner organisations)
- Use Practical Byzantine Fault Tolerance (PBFT) consensus
- Process 1,000-5,000 transactions per second (adequate for loyalty use case)
- Maintain privacy through channel-based data separation
- Provide on-chain audit trail visible to participants
- Synchronise with the relational database for queries

### 3.3 Governance

Consortium governance for validator nodes:

- Foundation + 3-5 partner organisations as validators
- Governance board decides on major changes
- Validators compensated in EUR for operations (not GoCoin)
- Consortium members have pseudonymous visibility
- Foundation remains the sole coin issuer

### 3.4 GDPR considerations

Blockchain immutability creates GDPR challenges. Mitigations:

- Store only hashed references to personal data on-chain
- Personal data remains in the off-chain database with normal deletion capability
- On-chain data pseudonymous (account IDs, not names)
- EDPB Guidelines 02/2025 on blockchain guidance followed
- DPIA conducted before launch

### 3.5 Why not Phase 1

Permissioned blockchain adds significant complexity for marginal benefit at small scale:

- More infrastructure (validator nodes, consensus, networking)
- More operational expertise required
- More compliance considerations
- Slower transactions
- Higher cost per operation

The relational database achieves 95% of the benefits (transparent records, audit trails, immutability through append-only design) at 5% of the complexity. The permissioned chain makes sense only when:

- Community clearly values on-chain transparency over database transparency
- Validator consortium provides meaningful decentralisation
- Scale justifies the operational overhead

These conditions are more likely to emerge in Phase 3+ as the ecosystem matures.

---

## 4. Integration with ecosystem

### 4.1 Payment integration

Purchase rewards triggered by payment processor webhooks:

```
User purchases Pro subscription
   ↓
Payment processor (Stripe/PayPal/SEPA) confirms payment
   ↓
Webhook to GoNode backend
   ↓
Backend verifies payment authenticity
   ↓
Loyalty coin reward calculated and issued
   ↓
User notified of coin earn
```

### 4.2 GoUNITY identity

Account identifiers link to GoUNITY certificates:

```
User authenticates with GoUNITY certificate
   ↓
Certificate DN hashed to identifier_hash
   ↓
Account record located or created
   ↓
Session established with account context
```

No plaintext user data stored in the ledger - only the hashed identifier.

### 4.3 Hardware binding (GoKey integration)

For premium operations, hardware-anchored identity via GoKey:

```
High-value operation requested (large marketplace trade, redemption)
   ↓
GoKey signature required in addition to session
   ↓
Signature verified against account's registered GoKey
   ↓
Operation executed if signature valid
```

This creates an additional security layer for high-value actions without affecting routine operations.

### 4.4 Marketplace integration

Marketplace listings and trades use the core ledger:

- Listing creates a reservation on seller's coins/items
- Acceptance triggers atomic swap
- Dispute resolution can reverse trades within time window
- Audit log records all marketplace activity

---

## 5. Security

### 5.1 Threat model

Relevant threats for the loyalty ledger:

| Threat | Likelihood | Impact | Mitigation |
|:-------|:-----------|:-------|:-----------|
| SQL injection | Low | High | Parameterized queries, input validation |
| Account takeover | Medium | High | Multi-factor authentication, anomaly detection |
| Database compromise | Low | High | Encryption at rest, access controls, audit logs |
| Insider threat | Low | High | Separation of duties, audit logging, least privilege |
| Marketplace fraud | Medium | Medium | Dispute resolution, rate limiting, pattern detection |
| DDoS on marketplace | Medium | Low | Rate limiting, CDN, autoscaling |
| Ledger inconsistency | Low | High | Atomic transactions, daily reconciliation, backups |

### 5.2 Access control

**Database access tiers:**

| Role | Permissions |
|:-----|:------------|
| Application (read-write) | Transactions, balances (no direct deletion) |
| Read-only reporting | Read-only access to all tables |
| Admin (operations) | Schema changes, emergency operations (audited) |
| Emergency access | Break-glass access with mandatory review |

**Principle of least privilege:** Developers work against development databases; production access is restricted and audited.

### 5.3 Encryption

- **In transit:** TLS 1.3 for all connections
- **At rest:** AES-256 disk encryption
- **Sensitive fields:** Additional column-level encryption where applicable
- **Backups:** Encrypted with separate keys

### 5.4 Audit and monitoring

- All operations logged to `audit_log` table
- External audit log mirror (append-only, separate system)
- Anomaly detection on unusual patterns
- Regular access reviews
- Quarterly security audits

### 5.5 Incident response

- 24/7 monitoring after Phase 2
- Incident response playbook documented
- Communication templates for user notifications
- Coordination with SECURITY.md processes
- Post-incident review within 30 days

---

## 6. Compliance integration

### 6.1 DSA compliance

Marketplace integration points for DSA:

- Notice-and-action mechanism writes to `audit_log` and `moderation_actions`
- Statement of reasons records kept
- Transparency report data queries prepared
- Automated content detection for prohibited items

### 6.2 GDPR compliance

- User data export queries: prepared and tested
- Deletion requests: cascade through appropriate tables (preserving audit requirements)
- Consent management: separate tables for explicit consents
- Data minimisation: only necessary fields captured

### 6.3 DAC7 reporting

Annual reporting infrastructure:

- Quarterly data aggregation for trading user summaries
- Annual report generation aligned with BZSt schema
- User notification workflow for reportable activity
- 10-year data retention for reporting records

### 6.4 Tax calculation

For operator rewards:
- Monthly EUR-equivalent valuation based on redemption value
- Cumulative annual totals per operator
- Annual tax statements generated automatically

---

## 7. Comparison with old smart contract design

| Dimension | Old (Solidity) | New (Database) |
|:----------|:---------------|:---------------|
| Implementation language | Solidity | Go + SQL |
| Deployment target | Arbitrum L2 | PostgreSQL cluster |
| Gas cost per operation | ~$0.10-1.00 | Free |
| Transaction finality | 1-5 seconds | Milliseconds |
| Audit cost | 50,000 - 200,000 EUR per contract | Standard software testing |
| Upgrade mechanism | Complex (migration contracts) | Standard software releases |
| Emergency response | Timelock + multisig | Database operations |
| Dev complexity | High (EVM, gas optimization, security) | Low (standard web dev) |
| Throughput | ~10-50 TPS (Arbitrum) | 1,000+ TPS easily |
| Storage cost | Expensive (~$1/KB on-chain) | Cheap (~$0.01/GB) |
| Querying | Limited (event logs, state lookups) | Full SQL |
| Regulatory status | Crypto asset under MiCA | Standard database records |
| Integration | Web3 libraries required | Standard REST/GraphQL |
| Failure modes | Consensus bugs, MEV, flash loans | Standard DB failure modes |

---

## 8. Implementation timeline

### 8.1 Phase 1 implementation (Months 3-9)

**Month 3-4: Foundation**
- Database schema implementation
- Core application layer
- Basic API endpoints
- Unit and integration tests

**Month 5-6: Operations**
- Earning flows (purchase, operator, community)
- Balance queries and transaction history
- Account management
- Admin tools

**Month 7-8: Redemption**
- Redemption catalog
- Fulfillment workflow
- Item tracking
- Customer support tools

**Month 9: Launch**
- Load testing
- Security audit
- Monitoring deployment
- Soft launch with limited users

### 8.2 Phase 2 (Months 9-15)

- Operator rewards live
- Holding period mechanics
- Performance optimization
- Compliance integrations (DSA, DAC7 prep)

### 8.3 Phase 3 (Months 15-21)

- Marketplace development
- Dispute resolution
- DSA full compliance
- DAC7 reporting infrastructure
- Decision point on permissioned blockchain

### 8.4 Phase 3+ if needed (Months 21+)

- Permissioned blockchain evaluation
- Pilot with subset of functionality
- Migration plan if adopted
- Parallel operation during transition

---

## 9. Operational runbook

### 9.1 Routine operations

**Daily:**
- Monitoring dashboard review
- Backup verification
- Anomaly detection review
- Support ticket triage

**Weekly:**
- Performance metrics review
- Security log review
- Capacity planning check
- Minor updates and patches

**Monthly:**
- Supply report generation
- Transparency report data
- External backup verification
- Disaster recovery drill
- Operator reward batch processing

**Quarterly:**
- Security audit
- Compliance review
- Schema change planning
- Major version updates

### 9.2 Emergency procedures

**Database unavailability:**
1. Automated failover to standby
2. Application degrades gracefully (read-only mode)
3. Status page updated
4. Users notified via in-app and email
5. Root cause analysis within 24 hours

**Suspected breach:**
1. Immediate isolation of affected systems
2. Investigation team assembled
3. User data assessment
4. Regulatory notification if required (72 hours GDPR)
5. User notification if personal data affected
6. Coordinated public disclosure

**Supply cap breach:**
1. Immediate alert to operations team
2. Investigation of cause
3. Correction via compensating transactions if needed
4. Root cause fix
5. Public transparency about incident

### 9.3 Reconciliation

Daily reconciliation ensures ledger integrity:

```sql
-- Verify sum of balances matches cumulative issuance - cumulative burns
SELECT
    (SELECT SUM(amount) FROM balances) AS total_balances,
    (SELECT SUM(amount) FROM transactions WHERE tx_type LIKE 'earn_%') AS total_issued,
    (SELECT SUM(amount) FROM transactions WHERE tx_type IN ('redeem', 'burn')) AS total_burned,
    (SELECT SUM(amount) FROM transactions WHERE tx_type LIKE 'earn_%') -
    (SELECT SUM(amount) FROM transactions WHERE tx_type IN ('redeem', 'burn')) AS expected_balance;
```

Any discrepancy triggers immediate investigation.

---

## 10. Why this design is better

### 10.1 For users

- No crypto wallet complexity
- No seed phrases to lose
- No gas fees
- Fast, familiar experience
- Consumer protection applies normally
- Can dispute transactions through normal channels

### 10.2 For the Foundation

- 1,000,000+ EUR in savings vs. smart contract deployment
- Standard operational tooling
- Normal hiring pool (not limited to Solidity experts)
- Easier regulatory compliance
- Lower ongoing costs
- Normal insurance availability

### 10.3 For the ecosystem

- Integrates easily with web apps and mobile
- Standard authentication patterns
- Familiar business logic
- Easy to extend with new features
- Lower barrier for third-party integration
- Scales naturally with user growth

### 10.4 For regulators

- Well-understood technology
- Clear legal classification
- Standard compliance patterns
- Established precedent (Payback, Miles, Steam)
- Normal audit procedures
- Familiar dispute resolution

---

## 11. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [Tokenomics](TOKENOMICS.md) | Economic design | This repo |
| [Architecture and Security](ARCHITECTURE_AND_SECURITY.md) | Network architecture | This repo |
| [Wire Protocol](WIRE_PROTOCOL.md) | Communication protocol | This repo |
| [Legal Compliance](LEGAL_COMPLIANCE.md) | Regulatory framework | This repo |
| [Business Model](BUSINESS_MODEL.md) | Revenue and economics | This repo |
| GoUNITY | Identity and authentication | Separate repo |
| GoKey | Hardware identity | SimpleGo repo |

---

*GoNode Ledger Architecture v2 - April 2026 (replaces v1 Smart Contracts design)*
*IT and More Systems, Recklinghausen, Germany*
