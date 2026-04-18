# Security Policy

GoNode takes security seriously. This document describes how to report security vulnerabilities, how we respond to reports, and how we coordinate disclosure.

---

## Supported versions

Security updates are provided for the following versions:

| Version | Supported |
|:--------|:----------|
| main (unreleased) | Yes |
| Latest release | Yes |
| Previous release | Yes (90 days after new release) |
| Older releases | No |

Once GoNode reaches 1.0 (expected Season 6), we will follow semantic versioning with security updates for the current major version and the previous one.

---

## Reporting a vulnerability

### DO NOT open public issues for security vulnerabilities

Public issues are visible to attackers before we can fix the problem. Please use the private reporting channels below.

### Private reporting channels

**Primary: Email**

Send reports to: **security@gonode.dev**

GPG encryption is strongly encouraged. Our public key is published at:

- https://simplego.dev/gonode-security.gpg (once live)
- Key fingerprint: (to be published at Phase 1 launch)

**Secondary: GitHub Security Advisories**

Use GitHub's private vulnerability reporting feature at:
https://github.com/saschadaemgen/GoNode/security/advisories/new

This creates a private discussion between you and the maintainers.

**What to include in your report:**

```
1. Vulnerability type (e.g., remote code execution, privilege escalation,
   information disclosure, smart contract exploit, cryptographic flaw)

2. Affected component(s) (e.g., service node runtime, specific smart
   contract, wire protocol, onion routing)

3. Impact assessment (what an attacker can do)

4. Steps to reproduce (or proof of concept code)

5. Your environment (OS, Go version, GoNode version, network)

6. Suggested remediation (if you have one)

7. Your preferred attribution for the acknowledgement (real name,
   handle, or anonymous)

8. Whether you plan to publish research about this (and timeline)
```

---

## Response timeline

We commit to the following response timeline:

| Step | Timeline |
|:-----|:---------|
| Initial acknowledgement | Within 48 hours |
| Triage assessment | Within 7 days |
| Fix development begins | Within 14 days (for confirmed high/critical) |
| Fix deployed | Within 90 days (industry standard) |
| Coordinated public disclosure | After fix deployed + reasonable notice |

Critical vulnerabilities (remote code execution, fund loss, key compromise) may be fixed and deployed faster, with disclosure delayed until operators have updated.

---

## Severity classification

We use a simplified severity scale:

| Severity | Criteria | Example |
|:---------|:---------|:--------|
| **Critical** | Immediate fund loss, key exposure, or network-wide compromise | Smart contract drain, private key extraction, consensus failure |
| **High** | Significant impact, limited scope OR significant impact with mitigations | Node impersonation, stake theft, significant DoS |
| **Medium** | Moderate impact or narrow scope | Specific user targeting, limited information disclosure |
| **Low** | Minor impact, self-limiting | Rate limit bypass, minor protocol deviation |
| **Informational** | Best practice, not exploitable | Code quality issues, documentation gaps |

---

## Bug bounty program

A formal bug bounty program will launch at Phase 2 (Season 3, approximately month 14 of the project). Until then, we acknowledge researchers through:

- Public thanks in release notes
- Attribution in our CONTRIBUTORS.md
- Swag from the Foundation (stickers, t-shirts)
- Potential airdrop eligibility if substantial

**Planned bounty structure (Phase 2+):**

| Severity | Reward (USD equivalent) |
|:---------|:------------------------|
| Critical | $10,000 - $250,000 |
| High | $2,500 - $25,000 |
| Medium | $500 - $5,000 |
| Low | $100 - $1,000 |

Bounties will be paid in the researcher's choice of EURC, USDC, or GoCoin (post-TGE).

---

## Scope

### In scope

- GoNode service node runtime (github.com/saschadaemgen/GoNode)
- Smart contracts deployed to Arbitrum One
- Client library integrations
- Wire protocol implementation
- Onion routing layer
- Swarm coordination protocol
- Audit challenge protocol
- Official Foundation websites (simplego.dev/gonode)

### Out of scope

The following are excluded from responsible disclosure but may still interest us:

- Third-party integrations (report to the third party)
- Vulnerabilities in upstream dependencies (Go stdlib, OpenZeppelin, etc.) - report to upstream first
- Social engineering attacks against individuals
- Physical attacks against hardware
- DDoS attacks (except architectural amplification issues)
- Vulnerabilities requiring already-compromised user credentials
- Outdated software versions not under active support
- Issues in test/staging environments (unless they indicate production issues)

### Ethical boundaries

We ask that security researchers:

- Do not access, modify, or delete data belonging to other users
- Do not disrupt network operations during testing
- Stay within the scope described above
- Report vulnerabilities promptly once confirmed
- Follow coordinated disclosure timelines
- Do not use findings for personal gain (beyond authorised bounties)

Researchers who follow these guidelines will not face legal action for their research activities.

---

## Coordinated disclosure

We follow a 90-day coordinated disclosure timeline, consistent with industry standards (Project Zero, CERT/CC):

```
Day 0:   Vulnerability reported privately
Day 0-7: Triage and severity assessment
Day 7:   Acknowledgement of receipt sent
Day 7-14: Reproduction and impact analysis
Day 14:  Fix development begins (high/critical)
Day 30:  Draft fix ready for internal review
Day 60:  Fix ready for deployment
Day 60-75: Operators notified via private channel, asked to update
Day 75:  Fix deployed, network transitioning to patched version
Day 90:  Public disclosure with CVE (if applicable)
```

**Adjustments:**

- **Earlier disclosure** may be coordinated if the vulnerability is already being exploited
- **Later disclosure** may be requested for particularly complex issues or if operators need more time to update
- **Immediate disclosure** is never done without coordination except in extreme circumstances

---

## Smart contract specifics

Smart contracts have unique security considerations because they cannot be patched like traditional software. Our approach:

### Pre-deployment

- Minimum 2 independent security audits before mainnet
- Formal verification for critical paths (where feasible)
- Bug bounty on testnet deployments
- Extensive unit and integration testing (95%+ coverage)

### Post-deployment

- No upgrade mechanisms for economic logic (intentional)
- Timelock on parameter changes (minimum 24 hours)
- Multi-sig control during Phase 0-3 (3-of-5)
- Deployer keys burned at Phase 4 (month 36)
- Continuous monitoring via Forta agents

### Emergency response

If a critical smart contract vulnerability is discovered post-deployment:

```
Option 1: Pausable functions (Phase 0-3 only)
  - Foundation multisig can pause affected functions
  - Users protected while fix developed
  - Pause function removed at Phase 4

Option 2: Migration contract
  - Deploy new contract
  - Users migrate funds from old to new
  - Old contract remains but deprecated

Option 3: Live with the bug
  - If severity is low and no fix is safe
  - Document publicly, mitigate off-chain
```

We cannot guarantee recovery of user funds in the event of a critical smart contract exploit. Users should understand this risk.

---

## Cryptographic concerns

GoNode relies on several cryptographic primitives. If you find weaknesses:

- **In our implementations**: report via security@gonode.dev
- **In underlying algorithms** (Ed25519, X25519, AES, etc.): report to the algorithm maintainers, notify us for awareness
- **In our protocol design**: report via security@gonode.dev for architectural discussion
- **Post-quantum concerns**: especially welcome, as we actively monitor this space

Specific cryptographic dependencies:

| Primitive | Used for | Library |
|:----------|:---------|:--------|
| Ed25519 | Operator identity, signatures | libsodium |
| X25519 | Key agreement, onion routing | libsodium |
| XChaCha20-Poly1305 | AEAD message encryption | libsodium |
| SHA-256 | Hashing, HMAC | Go stdlib / libsodium |
| ML-KEM-768 | Post-quantum KEM | CRYSTALS-Kyber |
| Reed-Solomon | Erasure coding | klauspost/reedsolomon |
| ECVRF-EDWARDS25519 | Epoch randomness | RFC 9381 implementation |

---

## Security updates

### Release channels

- **Emergency releases**: Published to main branch, announced immediately via all channels
- **Security releases**: Published with 24-hour operator notification window
- **Regular releases**: Include accumulated security improvements

### Notification channels

Operators should subscribe to at least one:

- **Security mailing list**: security-announce@gonode.dev (once live)
- **GitHub security advisories**: watch the repository
- **Matrix channel**: #gonode-security:simplego.dev
- **RSS feed**: simplego.dev/gonode-security.rss

### Update urgency

| Severity | Operator Action Required |
|:---------|:-------------------------|
| Critical | Update within 24 hours |
| High | Update within 7 days |
| Medium | Update within 30 days |
| Low | Update at next convenient opportunity |

Nodes that run outdated software may be flagged and receive reduced rewards.

---

## Security architecture

For details on GoNode's security architecture, threat model, and defensive measures, see:

- [ARCHITECTURE_AND_SECURITY.md](docs/ARCHITECTURE_AND_SECURITY.md) - Full threat model
- [WIRE_PROTOCOL.md](docs/WIRE_PROTOCOL.md) - Protocol-level security
- [SMART_CONTRACTS.md](docs/SMART_CONTRACTS.md) - On-chain security

---

## Hall of fame

Security researchers who have contributed to GoNode's security will be listed here. Contributions are categorised by severity of finding.

This section will be populated as researchers report vulnerabilities. First entries expected during Phase 1 testnet.

---

## Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [Architecture and Security](docs/ARCHITECTURE_AND_SECURITY.md) | Threat model and defences | This repo |
| [Code of Conduct](CODE_OF_CONDUCT.md) | Community standards | This repo |
| [Contributing](CONTRIBUTING.md) | How to report and contribute | This repo |
| [SimpleGo Security](https://github.com/saschadaemgen/SimpleGo/blob/main/SECURITY.md) | Ecosystem security policy | SimpleGo repo |
| [GoBot Security](https://github.com/saschadaemgen/GoBot/blob/main/SECURITY.md) | Related component security | GoBot repo |

---

*GoNode Security Policy v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
