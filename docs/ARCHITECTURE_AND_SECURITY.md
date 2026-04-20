# GoNode Architecture and Security

**Document version:** Season 1 | April 2026
**Component:** GoNode protocol architecture and threat model
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the complete architecture of GoNode and the security properties of each layer. GoNode is the decentralised infrastructure layer for the SimpleGo messaging ecosystem. Following the redesign from crypto-token economics to closed-loop loyalty system, the architecture has been simplified: the economic/tokenomic layer on Arbitrum is gone, replaced by a straightforward loyalty ledger (see SMART_CONTRACTS.md). The core networking, cryptographic, and routing architecture remains unchanged.

**Architecture at a glance:**

```
+---------------------------------------------------+
|  Application Layer                                |
|  SimpleGo, SimpleGoX, GoBot, GoLab, GoMarket      |
+---------------------------------------------------+
|  Identity Layer                                   |
|  GoUNITY certificates + GoKey hardware binding    |
+---------------------------------------------------+
|  Loyalty Ledger Layer                             |
|  PostgreSQL (Phase 1) or permissioned chain       |
|  (Phase 3+) for GoCoin accounting                 |
+---------------------------------------------------+
|  Message Routing Layer                            |
|  3-hop Sphinx onion routing over SMP              |
+---------------------------------------------------+
|  Swarm Coordination Layer                         |
|  5-10 node swarms, VRF membership, 24h rotation   |
+---------------------------------------------------+
|  Storage Layer                                    |
|  Reed-Solomon RS(10, 16) erasure coding           |
+---------------------------------------------------+
|  Cryptographic Layer                              |
|  6 layers: 5 from SimpleX + 1 onion hop encryption|
|  ML-KEM-768 post-quantum ready                    |
+---------------------------------------------------+
|  Transport Layer                                  |
|  TLS 1.3 with hybrid post-quantum handshake       |
+---------------------------------------------------+
|  Physical Layer                                   |
|  ESP32-S3 hardware, eFuse-bound identity          |
+---------------------------------------------------+
```

Each layer is independently secure. Compromise of one layer does not defeat security at other layers.

---

## 1. Design principles

### 1.1 Defence in depth

No single layer provides the security guarantee. Five of the eight layers (cryptographic, routing, swarm, identity, hardware) contribute independently to the security posture. An attacker must defeat multiple layers simultaneously to compromise a user.

### 1.2 Zero-knowledge by design

The infrastructure does not know who users are. Operators cannot identify user content, destination, or metadata beyond what is strictly necessary to route messages. This is not a policy choice but an architectural invariant: even if operators wanted to surveil, the architecture does not provide that capability.

### 1.3 Progressive decentralisation

At launch, the Foundation operates bootstrap infrastructure. Over time (Phase 1 through Phase 4), operations transition to independent operators via the GoNode infrastructure. The loyalty system rewards operators for contributing resources.

### 1.4 Post-quantum ready

All long-term cryptographic choices include post-quantum variants. ML-KEM-768 handshakes alongside X25519 provide defense against future quantum adversaries while maintaining current efficiency.

### 1.5 Hardware-anchored where possible

Operators can bind their identity to physical hardware (GoKey devices) via eFuse, creating a cryptographic root of trust that cannot be cloned or extracted. This is optional for users but available for high-value operations.

### 1.6 Simplicity in the economic layer

Unlike the previous design, the loyalty ledger does not rely on blockchain consensus, smart contracts, or distributed economic logic. This separation allows the networking architecture to remain complex where it needs to be (cryptography, routing) while the bookkeeping remains simple.

---

## 2. Application layer

### 2.1 Supported clients

| Client | Platform | Role |
|:-------|:---------|:-----|
| SimpleGo | iOS, Android, desktop | Primary messenger |
| SimpleGoX | ESP32-S3 hardware | High-security standalone device |
| GoBot | Server-side bot framework | Automated message processing |
| GoLab | Web | Community platform (Twitter/Git hybrid) |
| GoMarket | Web + mobile | Ecosystem marketplace |
| Third-party via SDK | Various | Custom integrations |

### 2.2 Client authentication

All clients authenticate to GoNode infrastructure via:

- **GoUNITY certificate** (Ed25519, issued by certificate authority)
- **Optional GoKey signature** (hardware-bound, for premium operations)
- **TLS client certificate** (connection-level authentication)

### 2.3 Client capabilities

Clients communicate with the network through these operations:

| Operation | Purpose |
|:----------|:--------|
| send_message | Deliver message to recipient |
| fetch_messages | Receive queued messages |
| store_file | Upload file to distributed storage |
| retrieve_file | Download file from storage |
| subscribe_channel | Subscribe to broadcast channel |
| query_balance | Check GoCoin loyalty balance |
| redeem_coins | Exchange coins for ecosystem items |
| marketplace_action | Interact with P2P marketplace |

---

## 3. Identity layer

### 3.1 GoUNITY certificates

Identity in the GoNode ecosystem is mediated by GoUNITY, an Ed25519-based certificate authority that issues identity certificates. These certificates:

- Bind a public key to a pseudonymous identifier
- Are not tied to real-world identity by default
- Can optionally include hardware attestation (via GoKey)
- Support revocation via short-lived certificates (renewed weekly)
- Follow RFC 5280 X.509 structure with Ed25519 signatures

### 3.2 Identity hierarchy

```
Root CA (offline, HSM-protected)
    |
    +-- Intermediate CA (for user identities)
    |       |
    |       +-- User certificate 1
    |       +-- User certificate 2
    |       +-- ...
    |
    +-- Intermediate CA (for operator identities)
            |
            +-- Operator certificate (eFuse-bound)
            +-- Operator certificate (eFuse-bound)
            +-- ...
```

Root CA kept offline in hardware security module. Intermediates stay online for issuing and revocation. Revocation available via OCSP and CRL.

### 3.3 Hardware binding via GoKey

For operators and high-security users, GoKey devices provide hardware-bound identity:

- ESP32-S3 chip with eFuse-protected private key
- Key cannot be extracted even with physical access
- Signatures verified against the burned public key on chip
- Replacement device requires re-enrollment
- Revocation takes effect within 24 hours

### 3.4 Pseudonymous identifiers

The ecosystem never requires real names. Users can:

- Register with only an email (verified, for account recovery)
- Use a random pseudonym or a chosen handle
- Change pseudonyms (certificates reissued)
- Operate entirely pseudonymously

Real name is only required for:

- DAC7 reporting above thresholds (EUR 2,000/year or 30+ marketplace transactions)
- Dispute resolution escalations
- Large hardware orders (shipping)
- Enterprise contracts

---

## 4. Loyalty ledger layer

### 4.1 Role in the architecture

The loyalty ledger tracks GoCoin balances and transactions for users, operators, and the Foundation. Details are in SMART_CONTRACTS.md. Key architectural points:

- **Separate from message routing:** Coin transactions and message routing are independent. The Foundation can operate the ledger without visibility into message content, and message routing operates without reference to coin balances.
- **Ledger operates centrally:** Phase 1 uses PostgreSQL; optional migration to permissioned blockchain in Phase 3+. Either approach does not require blockchain consensus for routing decisions.
- **Loyalty bookkeeping has no routing implications:** A user's coin balance does not affect how their messages are routed. This is different from the old design where stake influenced routing.

### 4.2 Integration points

| Event | Ledger action |
|:------|:--------------|
| User pays for Pro subscription | Earn coins recorded |
| User pays for hardware | Earn coins recorded |
| Operator completes monthly period | Monthly rewards calculated and credited |
| User redeems coins | Balance deducted, fulfillment queued |
| User posts on marketplace | Listing created, coins locked |
| Marketplace trade completes | Balances swapped, fee burned |
| User shares coins with another user | Transfer transaction |

### 4.3 What the ledger does not do

The loyalty ledger explicitly does not:

- Control message routing
- Gate access to basic services (free tier always available)
- Track message metadata
- Process payments in EUR (payment processor does that)
- Issue rewards for monetary transactions outside the ecosystem
- Enable cash-out to EUR or other currencies

---

## 5. Message routing layer

### 5.1 Routing model

Messages are routed through swarms using 3-hop Sphinx onion routing:

```
Sender
   |
   | (encrypted 4 times: recipient + 3 hops)
   v
Swarm 1 (entry swarm)
   | Strips outer layer, learns next hop
   |
   v
Swarm 2 (middle swarm)
   | Strips layer, learns next hop
   |
   v
Swarm 3 (exit swarm)
   | Strips layer, delivers to recipient's storage
   |
   v
Recipient (via SMP fetch)
```

Each swarm sees only its predecessor and successor. No swarm sees the complete path.

### 5.2 Sphinx format

Following the Sphinx Mix Network specification (Danezis & Goldberg, 2009):

- Each packet is fixed size (prevents traffic analysis)
- Each layer encrypted with per-hop symmetric keys derived from ephemeral Diffie-Hellman
- Header includes only next-hop routing info (also encrypted)
- Padding ensures constant size throughout route
- Reply blocks allow anonymous reply routing

### 5.3 Swarm selection

Entry, middle, and exit swarms are selected:

- From the current epoch's active swarm set
- Using client-side random selection (not dictated by infrastructure)
- With geographic and jurisdictional diversity requirements
- Avoiding swarms known to the user as compromised

### 5.4 Traffic analysis resistance

| Technique | Defeats |
|:----------|:--------|
| Sphinx onion routing | Origin-destination correlation |
| Constant packet size | Size-based traffic analysis |
| Cover traffic (optional Pro feature) | Volume-based traffic analysis |
| Random routing | Route prediction |
| Swarm rotation every 24h | Long-term correlation |
| Jurisdictional diversity | Nation-state collusion |

---

## 6. Swarm coordination layer

### 6.1 Swarm structure

A swarm is a group of 5-10 nodes that collaborate on:

- Routing a subset of messages
- Storing message fragments using erasure coding
- Providing redundancy for member failure
- Sharing audit responsibilities

### 6.2 Swarm membership

Membership is determined by:

- **VRF (Verifiable Random Function):** Deterministic but unpredictable assignment
- **Epoch-based rotation:** Members change every 24 hours
- **Geographic/jurisdictional balance:** No swarm with all members in one country
- **Performance history:** Poorly performing nodes less likely to be selected

### 6.3 Epoch randomness

Swarm assignment uses ECVRF-EDWARDS25519-SHA512-TAI per RFC 9381:

```
VRF_output = VRF(private_key, epoch_seed || node_id)
Swarm = hash(VRF_output) mod num_swarms
```

Seed comes from a distributed beacon (drand) for unpredictability.

### 6.4 Operator incentives

Operators run nodes because:

- They earn GoCoin loyalty rewards (see TOKENOMICS.md)
- They contribute to a privacy infrastructure they believe in
- They gain access to ecosystem features and community status

Unlike the old design, operators do not:

- Need to stake money or tokens
- Risk slashing of stake
- Participate in complex economic games
- Need to understand tokenomics

Operator requirements are simple: reliable hardware, good network connectivity, reasonable uptime, honest behavior.

### 6.5 Operator requirements

Hardware specifications:

| Tier | CPU | RAM | Storage | Network |
|:-----|:----|:----|:--------|:--------|
| Entry | 2 cores | 4 GB | 100 GB SSD | 100 Mbps, 1 TB/mo |
| Standard | 4 cores | 8 GB | 500 GB SSD | 1 Gbps, unlimited |
| Enterprise | 8 cores | 16 GB | 2 TB NVMe | 10 Gbps, unlimited |

Operational requirements:

- 99.0% uptime minimum (entry), 99.9% (enterprise)
- Static IP address
- Open ports configured correctly
- Monitoring endpoint responsive
- Timely security updates

---

## 7. Storage layer

### 7.1 Erasure coding approach

Files and large messages use Reed-Solomon RS(10, 16) erasure coding:

- Original data split into 10 fragments
- Reed-Solomon parity generates 6 additional fragments
- Total: 16 fragments distributed across swarm members
- Any 10 fragments can reconstruct the original
- Storage overhead: 1.6x

### 7.2 Durability target

With RS(10, 16) and 16 independent storage nodes:

- Can tolerate up to 6 simultaneous node failures
- Node failure rate assumption: 1% annually
- Durability: 99.999999999% (11 nines)

This is roughly equivalent to AWS S3 durability but achieved without centralized infrastructure.

### 7.3 Audit challenge protocol

Storage nodes are audited to verify they still hold their fragments:

```
Audit protocol (every hour, per node):
1. Auditor challenges node: "Prove you have fragment X"
2. Node computes HMAC(fragment_X, nonce) and returns
3. Auditor verifies HMAC against expected value
4. Failure = audit failure recorded
5. Cumulative failures = swarm rebuilds fragment on different node
```

Challenges are:

- Lightweight (HMAC, no expensive cryptography)
- Frequent (hourly per node)
- Unpredictable (random nonces)
- Verifiable by multiple parties

### 7.4 Why not Filecoin-style PoRep/PoSt

The old design considered Filecoin's Proof-of-Replication and Proof-of-Spacetime. Reasons we chose audit-based approach:

- PoRep/PoSt are computationally expensive (GPU required)
- Requires complex cryptographic setup
- Heavy storage overhead for proofs
- Audit approach provides equivalent guarantees at fraction of cost

### 7.5 File encryption

Files are end-to-end encrypted before chunking:

- Sender encrypts with XChaCha20-Poly1305 AEAD
- Each chunk has its own authenticated tag
- Fragment-level encryption (not just end-to-end) adds layer against any one node
- Metadata (size, type) also encrypted

Even if an attacker obtained all 16 fragments of a file, they would see only random-looking data without the encryption key.

---

## 8. Cryptographic layer

### 8.1 Six layers of encryption

Messages pass through six independent encryption layers:

**Layer 1 (SimpleX SMP protocol):** Each queue has a unique encryption key derived from initial key agreement. Messages encrypted with XChaCha20-Poly1305.

**Layer 2 (Double Ratchet):** SimpleX uses the Signal Protocol's Double Ratchet for forward secrecy. Each message has a unique key derived from the ratchet state.

**Layer 3 (Per-contact keys):** Each contact pair has distinct keys derived during handshake. A compromise of one contact does not affect others.

**Layer 4 (Session keys):** Each connection establishes session keys via ephemeral Diffie-Hellman (X25519). Forward secrecy for the session.

**Layer 5 (Queue encryption):** Queue-level encryption prevents operators from correlating message bodies with queue metadata.

**Layer 6 (Sphinx onion):** Each of the 3 hops adds a layer of Sphinx encryption (X25519 + ChaCha20).

### 8.2 Primitive choices

| Purpose | Algorithm | Library |
|:--------|:----------|:--------|
| Symmetric encryption | XChaCha20-Poly1305 AEAD | libsodium |
| Key exchange | X25519 | libsodium |
| Digital signatures | Ed25519 | libsodium |
| Hashing | SHA-256, SHA-512 | Go stdlib / libsodium |
| HMAC | HMAC-SHA256 | libsodium |
| KDF | BLAKE2b | libsodium |
| Random | OS CSPRNG (getrandom) | Go stdlib |
| VRF | ECVRF-EDWARDS25519-SHA512-TAI | custom impl per RFC 9381 |
| Post-quantum KEM | ML-KEM-768 | CRYSTALS-Kyber |

### 8.3 Post-quantum readiness

Post-quantum threat model: a sufficiently powerful quantum computer could break X25519 and Ed25519. Mitigation:

- **Hybrid handshakes:** X25519 + ML-KEM-768. Both must be broken for compromise.
- **Signature transition plan:** Move to ML-DSA (Dilithium) when standardised and mature.
- **Long-lived keys:** Rotated more frequently as quantum capability advances.
- **Store-now-decrypt-later defence:** Hybrid approach protects retroactively encrypted traffic.

### 8.4 Key management

- **Root CA keys:** Offline in HSM, used only for certificate issuance
- **Intermediate CA keys:** Online but restricted access, used for user/operator certificates
- **User keys:** Generated client-side, stored in platform keystore
- **Operator keys:** Generated by GoKey device, never leaves hardware
- **Session keys:** Ephemeral, never stored
- **Fragment encryption keys:** Derived per-message from sender's master key

---

## 9. Transport layer

### 9.1 TLS 1.3 with hybrid PQ

All connections use TLS 1.3 with:

- Server authentication via certificate (ECDSA-P384 + Ed25519 as composite)
- Hybrid key exchange: X25519 + ML-KEM-768
- Cipher suite: TLS_CHACHA20_POLY1305_SHA256
- SNI always encrypted (ECH when available)
- 0-RTT disabled (not necessary, avoids replay complications)

### 9.2 Connection architecture

Clients connect to swarm members, not directly to destination:

```
Client --TLS--> Swarm 1 member (entry)
                   |
                   | (internal routing)
                   v
                Swarm 2 member (middle)
                   |
                   v
                Swarm 3 member (exit)
                   |
                   v
                Destination
```

Internal swarm-to-swarm traffic uses mutual TLS with certificate pinning.

### 9.3 Bandwidth efficiency

Optimization techniques:

- Batching: Multiple messages in single transport packet
- Compression: Optional per-connection (careful vs. CRIME-style attacks)
- Persistent connections: HTTP/3 where applicable
- Selective retransmission: QUIC-like behavior

---

## 10. Physical and hardware layer

### 10.1 ESP32-S3 hardware

SimpleGo hardware devices use Espressif ESP32-S3:

- 240 MHz dual-core CPU
- 512 KB SRAM + 8 MB PSRAM
- Secure boot with eFuse-stored keys
- USB OTG and Wi-Fi/BLE
- Widely available, well-audited, open documentation

### 10.2 eFuse security

Critical keys stored in eFuse:

- **Manufacturing key:** Burned at production, proves device authenticity
- **User binding key:** Burned at user enrolment, binds device to user
- **Revocation key:** Burned at emergency revocation

Key properties:

- Physically irreversible (one-time programmable silicon)
- Not accessible to software after burning
- Used only by hardware crypto accelerator
- Survives firmware updates and resets

### 10.3 Secure boot

Devices boot only signed firmware:

1. ROM bootloader verifies signature using burned key
2. Bootloader loads application partition
3. Application verifies own signature
4. Application runs with hardware isolation

Any modification to firmware breaks signature verification and prevents boot.

### 10.4 Physical attack resistance

Realistic threat model acknowledges:

- Attacker with physical access and lab equipment can extract keys from most MCUs
- eFuse is harder to attack than flash storage but not invulnerable
- Motivated nation-state attacker with silicon-level capability can compromise
- Defense: detect rather than prevent (attested boot measurements)

For most users, physical access protection is adequate against opportunistic attackers and sufficient for routine use.

---

## 11. Threat model and scenarios

### 11.1 Scenario: Passive network observer

**Attacker capability:** Observes network traffic but cannot modify or inject.

**Attacker goal:** Identify who is communicating with whom.

**Defenses:**

- Sphinx onion routing obscures sender-receiver relationship
- Constant packet sizes prevent size-based correlation
- Cover traffic (Pro feature) prevents volume correlation
- TLS encrypts content

**Residual risk:** Global adversary observing all traffic could perform statistical correlation over long periods.

**Mitigation beyond protocol:** Client-side delay randomization, traffic shaping.

### 11.2 Scenario: Malicious single swarm member

**Attacker capability:** Controls 1 node in a swarm of 5-10.

**Attacker goal:** Learn message content or metadata.

**Defenses:**

- Sphinx: node sees only previous/next hop, not source or destination
- End-to-end encryption: node cannot decrypt content
- Erasure coding: node holds only 1 of 16 fragments (insufficient to reconstruct)

**Residual risk:** Node knows which swarm fragments belong together.

**Mitigation:** 30-day fragment rotation, fragment re-encryption at rotation.

### 11.3 Scenario: Multiple colluding swarm members

**Attacker capability:** Controls 3+ nodes in same swarm.

**Attacker goal:** Reconstruct message content.

**Defenses:**

- Needs 10 fragments to decode Reed-Solomon; 3 is insufficient
- Even with 10, still needs encryption key (held by recipient)
- VRF-based assignment makes coordinated takeover hard

**Residual risk:** Sophisticated attacker could try to gain 10+ nodes in target swarm.

**Mitigation:** Large operator base dilutes attacker share; jurisdictional diversity requirements prevent nation-state concentration.

### 11.4 Scenario: Swarm-level collusion

**Attacker capability:** All 3 swarms in a message's route collude.

**Attacker goal:** Correlate sender and receiver.

**Defenses:**

- VRF randomization makes it unlikely attacker controls all 3 chosen swarms
- Even with full path visible, end-to-end encryption protects content
- Padding and cover traffic reduce correlation confidence

**Residual risk:** Well-resourced attacker could compromise many swarms.

**Mitigation:** Large total operator count (target 1000+ by Phase 3) makes 3-swarm compromise probabilistically expensive.

### 11.5 Scenario: Compromised GoUNITY CA

**Attacker capability:** Compromises the certificate authority.

**Attacker goal:** Issue fraudulent certificates to impersonate users or operators.

**Defenses:**

- Root CA offline in HSM
- Intermediate CAs have limited delegation
- Certificate transparency logs expose fraudulent issuance
- Revocation available within hours

**Residual risk:** Time window between compromise and detection.

**Mitigation:** Short certificate lifetimes (weekly renewal), transparency monitoring.

### 11.6 Scenario: Physical attack on hardware device

**Attacker capability:** Physical possession of user's SimpleGo device.

**Attacker goal:** Extract keys or access messages.

**Defenses:**

- eFuse-protected keys resist basic extraction
- Secure boot prevents firmware tampering
- Device can be remotely revoked
- No plaintext keys in flash or RAM after boot

**Residual risk:** Nation-state lab with silicon-level attack capability.

**Mitigation:** User policy (device PIN), revocation on loss, limited key material on device.

### 11.7 Scenario: Quantum computer

**Attacker capability:** Possesses large-scale quantum computer.

**Attacker goal:** Decrypt currently-encrypted traffic (store-now-decrypt-later).

**Defenses:**

- Hybrid ML-KEM-768 + X25519 for forward secrecy
- Post-quantum signatures in roadmap (ML-DSA when ready)
- Long-term keys sized for post-quantum security

**Residual risk:** Transition period for signatures before PQ signatures mature.

**Mitigation:** Defense-in-depth; even if signatures broken, encryption still needs quantum computer; monitor NIST PQ standards for transition.

### 11.8 Scenario: Regulatory compulsion

**Attacker capability:** Government compels Foundation or operators to provide information.

**Attacker goal:** Identify specific users or decrypt their messages.

**Defenses:**

- Architecture prevents Foundation from knowing user identity (zero-knowledge design)
- Operators cannot decrypt user messages (end-to-end encryption)
- Metadata minimization limits what could be provided
- Jurisdictional diversity limits any single government's reach
- Transparent Terms of Service about cooperation with authorities under proper process

**Residual risk:** Future traffic can be observed (passive network scenario 11.1 applies).

**Mitigation:** Hardware-anchored identity, client-side controls, public transparency reports.

---

## 12. Security engineering processes

### 12.1 Development security

- Code review required for all changes
- Automated static analysis (staticcheck, gosec)
- Dependency scanning for vulnerabilities
- Reproducible builds with published hashes
- Mandatory security training for developers

### 12.2 Audit schedule

| Audit | Frequency | Scope |
|:------|:----------|:------|
| Internal code review | Continuous | All changes |
| Dependency audit | Monthly | Third-party libraries |
| External security audit | Annual | Full codebase |
| Penetration test | Annual | Infrastructure |
| Red team exercise | Biannual | End-to-end |
| Compliance audit | Annual | Legal/regulatory |

### 12.3 Disclosure policy

Vulnerability disclosure coordinated per SECURITY.md:

- 90-day coordinated disclosure default
- Immediate disclosure for already-exploited vulnerabilities
- Bug bounty program from Phase 2 onwards
- Hall of fame recognition for researchers

### 12.4 Incident response

See Section 9 of SMART_CONTRACTS.md for database/ledger incidents. For network and cryptographic incidents:

- Detection: continuous monitoring, anomaly detection
- Triage: severity assessment within 1 hour
- Response: incident commander, communications, investigation
- Recovery: coordinated patches, operator notification
- Review: post-incident analysis, lessons learned documented

---

## 13. Comparison with old architecture

| Component | Old design | New design |
|:----------|:-----------|:-----------|
| Economic layer | Arbitrum L2 + 5 smart contracts | PostgreSQL or permissioned chain |
| Economic consensus | Blockchain finality | Database ACID |
| Operator stake | 10,000 GoCoin locked | No stake required |
| Slashing mechanism | 5-20% stake penalty | Poor performance reduces rewards |
| Rewards flow | Token emission via contracts | Database records |
| User payment | Crypto or EUR-to-crypto | EUR via standard payment processors |
| Routing decisions | Independent of economics | Independent of economics (unchanged) |
| Message encryption | 6 layers (unchanged) | 6 layers (unchanged) |
| Storage approach | Reed-Solomon RS(10,16) (unchanged) | Reed-Solomon RS(10,16) (unchanged) |
| Identity layer | GoUNITY certificates (unchanged) | GoUNITY certificates (unchanged) |
| Hardware binding | GoKey eFuse (unchanged) | GoKey eFuse (unchanged) |
| Post-quantum | ML-KEM-768 hybrid (unchanged) | ML-KEM-768 hybrid (unchanged) |
| Audit protocol | HMAC challenges (unchanged) | HMAC challenges (unchanged) |
| Swarm rotation | 24h epoch (unchanged) | 24h epoch (unchanged) |

**Summary:** The core network architecture is unchanged. Only the economic layer is simpler.

---

## 14. Performance and scale targets

### 14.1 Network scale targets

| Metric | Phase 1 | Phase 2 | Phase 3 | Phase 4 |
|:-------|:--------|:--------|:--------|:--------|
| Total operators | 50 | 200 | 500 | 1,500+ |
| Active swarms | 5 | 20 | 50 | 150+ |
| Active users | 500 | 5,000 | 50,000 | 500,000+ |
| Messages/day | 10,000 | 500,000 | 10M | 100M+ |
| File storage | 100 GB | 10 TB | 500 TB | 5+ PB |

### 14.2 Per-node performance targets

| Metric | Entry tier | Standard tier | Enterprise tier |
|:-------|:-----------|:--------------|:----------------|
| Messages/sec | 100 | 1,000 | 10,000 |
| Storage I/O | 100 MB/s | 1 GB/s | 10 GB/s |
| Concurrent connections | 1,000 | 10,000 | 100,000 |
| Audit challenges/hour | 10 | 100 | 1,000 |

### 14.3 End-user latency targets

| Operation | Target latency |
|:----------|:---------------|
| Message send (3-hop route) | <500ms |
| Message delivery | <1s |
| File upload (1 MB) | <2s |
| File download (1 MB) | <1s |
| Loyalty operation | <100ms |
| Marketplace browse | <200ms |

---

## 15. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [Wire Protocol](WIRE_PROTOCOL.md) | Protocol specifications | This repo |
| [Smart Contracts](SMART_CONTRACTS.md) | Loyalty ledger architecture | This repo |
| [Tokenomics](TOKENOMICS.md) | Economic design | This repo |
| [Legal Compliance](LEGAL_COMPLIANCE.md) | Regulatory framework | This repo |
| [Distributed Content Defense](DISTRIBUTED_CONTENT_DEFENSE.md) | Content integrity | This repo |
| [SimpleGo](https://github.com/saschadaemgen/SimpleGo) | Application layer | Separate repo |
| GoUNITY | Identity layer | Separate repo |
| GoKey | Hardware identity | SimpleGo repo |

---

*GoNode Architecture and Security v2 - April 2026 (updated for loyalty system)*
*IT and More Systems, Recklinghausen, Germany*
