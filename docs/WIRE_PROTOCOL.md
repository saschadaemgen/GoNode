# GoNode Wire Protocol

**Document version:** Season 1 | April 2026
**Component:** GoNode network protocol specification
**Copyright:** 2026 Sascha Daemgen, IT and More Systems, Recklinghausen
**License:** AGPL-3.0

---

## Overview

This document specifies the wire protocol for communication between GoNode service nodes and between clients and service nodes. Any implementation following this specification should be able to interoperate with reference implementations.

The protocol is layered on TLS 1.3 for transport security, uses binary framing for efficiency, and supports both request-response and streaming patterns. All protocol messages are defined using Protocol Buffers (protobuf) v3 for portability and forward compatibility.

The protocol specifies four categories of interaction:

| Category | Between | Purpose |
|:---------|:--------|:--------|
| Client-to-Node | User client, service node | Send/receive messages, upload/download files |
| Onion routing | Client, 3 intermediate nodes, target node | Anonymise source and destination |
| Node-to-Node (swarm) | Service nodes in same swarm | Replicate, coordinate, reach quorum |
| Audit | Audit coordinator, target node | Challenge data availability |

**Version:** Protocol version 1 (this document).
**Wire format:** Protocol Buffers v3 over TLS 1.3.
**Port defaults:** 7000 (peer-to-peer), 7001 (client), 7002 (audit).

---

## 1. Transport layer

### 1.1 TLS 1.3 configuration

All GoNode communication occurs over TLS 1.3. No exceptions.

**TLS parameters:**

| Parameter | Value |
|:----------|:------|
| Version | TLS 1.3 (RFC 8446) only, no fallback |
| Cipher suites | TLS_AES_256_GCM_SHA384, TLS_CHACHA20_POLY1305_SHA256 |
| Key exchange | X25519 preferred, P-256 fallback |
| Signature algorithms | Ed25519 preferred, ECDSA P-256 fallback |
| Session resumption | Pre-Shared Keys (PSK) for operators |
| 0-RTT data | Disabled (replay attack protection) |

### 1.2 Certificate pinning

Nodes publish their Ed25519 public key on-chain when registering. All peers verify connections against this registered key, not the TLS certificate CA hierarchy.

```
TLS handshake extension:
  application_layer_protocol_negotiation = "gonode/1"
  Additional extension = "gonode-pinned-key"
    Value: SHA-256 hash of expected Ed25519 public key

Verification:
  1. Complete TLS handshake
  2. Extract peer's server certificate
  3. Check Ed25519 signature in certificate extension
  4. Verify signature matches registered on-chain key
  5. If mismatch: abort connection, log attempted MITM
```

### 1.3 Connection lifecycle

```
Client initiates connection:
  1. TCP SYN to target node:7001
  2. TLS 1.3 handshake with key pinning
  3. Send HELLO frame with protocol version
  4. Receive HELLO_ACK with server capabilities
  5. Begin protocol operations

Connection maintenance:
  - Keepalive every 30 seconds (PING/PONG frames)
  - Idle timeout: 5 minutes (configurable)
  - Graceful shutdown: send GOODBYE frame, wait for ACK

Connection reuse:
  - Same client/node pair should reuse connections
  - Multiple streams multiplexed over single TLS connection
  - Connection pooling on client side for efficiency
```

---

## 2. Framing format

### 2.1 Frame structure

All messages are transmitted as binary frames:

```
+-------------+---------+-------+-------+--------+
| Length (4B) | Type(1B)| Flags | RsvID | Payload |
+-------------+---------+-------+-------+--------+
| big-endian  |  enum   | (1B)  | (4B)  | varlen |
+-------------+---------+-------+-------+--------+

Length: total frame size including header (max 16 MB)
Type: frame type enum (see 2.2)
Flags: per-type flag bits
ReservedID: stream identifier for multiplexing (0 = control)
Payload: protobuf-encoded content
```

**Header size:** 10 bytes fixed.

### 2.2 Frame types

| Type | Code | Direction | Purpose |
|:-----|:-----|:----------|:--------|
| HELLO | 0x01 | Both | Initial handshake |
| HELLO_ACK | 0x02 | Both | Handshake acknowledgement |
| PING | 0x03 | Both | Keepalive request |
| PONG | 0x04 | Both | Keepalive response |
| REQUEST | 0x10 | C->N | Client operation request |
| RESPONSE | 0x11 | N->C | Client operation response |
| STREAM_DATA | 0x12 | Both | Streaming data chunk |
| STREAM_END | 0x13 | Both | Streaming complete |
| REPLICATE | 0x20 | N->N | Replication request |
| REPLICATE_ACK | 0x21 | N->N | Replication acknowledgement |
| AUDIT_CHALLENGE | 0x30 | Audit->N | Audit challenge |
| AUDIT_RESPONSE | 0x31 | N->Audit | Audit response |
| GOODBYE | 0xFE | Both | Graceful shutdown |
| ERROR | 0xFF | Both | Error notification |

### 2.3 Protocol Buffers schema

Top-level schema file (simplified excerpt):

```protobuf
syntax = "proto3";
package gonode.v1;

message Frame {
  uint32 length = 1;
  FrameType type = 2;
  uint32 flags = 3;
  uint32 reserved_id = 4;
  bytes payload = 5;
}

enum FrameType {
  FRAME_UNKNOWN = 0;
  FRAME_HELLO = 1;
  FRAME_HELLO_ACK = 2;
  FRAME_PING = 3;
  FRAME_PONG = 4;
  FRAME_REQUEST = 16;
  FRAME_RESPONSE = 17;
  FRAME_STREAM_DATA = 18;
  FRAME_STREAM_END = 19;
  FRAME_REPLICATE = 32;
  FRAME_REPLICATE_ACK = 33;
  FRAME_AUDIT_CHALLENGE = 48;
  FRAME_AUDIT_RESPONSE = 49;
  FRAME_GOODBYE = 254;
  FRAME_ERROR = 255;
}
```

---

## 3. Handshake

### 3.1 HELLO frame

Sent by initiating party immediately after TLS handshake:

```protobuf
message Hello {
  uint32 protocol_version = 1;    // 1 for this specification
  string client_software = 2;      // e.g. "gonode-go/0.1.0"
  bytes operator_pubkey = 3;       // Ed25519, 32 bytes (for node peers)
  repeated string capabilities = 4; // e.g. ["store", "relay", "onion"]
  uint64 timestamp = 5;            // unix seconds, for replay protection
  bytes signature = 6;             // Ed25519 signature of all preceding fields
}
```

**Validation rules:**

- `protocol_version` must match supported version; else ERROR
- `timestamp` within 5 minutes of wall clock; else ERROR
- `signature` must verify against `operator_pubkey`; else ERROR
- `capabilities` determines what operations this peer can perform

### 3.2 HELLO_ACK frame

Response from receiving party:

```protobuf
message HelloAck {
  bool accepted = 1;
  string reason = 2;               // if !accepted
  uint32 protocol_version = 3;
  repeated string capabilities = 4; // server's capabilities
  uint32 max_frame_size = 5;       // server's max accept size
  uint32 idle_timeout_seconds = 6;
  bytes session_id = 7;            // for potential resumption
}
```

If `accepted` is false, the connection closes after this frame.

---

## 4. Client-to-node operations

### 4.1 Request/Response pattern

All client operations follow request-response:

```
Client                           Node
  |                               |
  |--- REQUEST (type, payload) -->|
  |                               | (processing)
  |<-- RESPONSE (status, data) ---|
```

Unique `reserved_id` in each request correlates with response.

### 4.2 Message queue operations

**Create queue:**

```protobuf
message CreateQueueRequest {
  bytes queue_id = 1;              // 32 bytes, random
  bytes recipient_pubkey = 2;      // Ed25519 pub key of queue owner
  uint32 ttl_seconds = 3;          // 86400 default (1 day)
  uint32 max_messages = 4;         // 1000 default
}

message CreateQueueResponse {
  ResponseStatus status = 1;
  bytes queue_id = 2;
  uint64 created_at = 3;
  uint64 expires_at = 4;
  uint32 assigned_swarm = 5;       // For verification
}
```

**Send message:**

```protobuf
message SendMessageRequest {
  bytes queue_id = 1;
  uint32 message_index = 2;        // Monotonic within queue
  bytes ciphertext = 3;            // 16 KB exactly (SimpleX requirement)
  bytes sender_auth = 4;           // Authentication tag
}

message SendMessageResponse {
  ResponseStatus status = 1;
  uint32 replication_count = 2;    // How many swarm members acked
  uint64 stored_at = 3;
}
```

**Poll messages:**

```protobuf
message PollMessagesRequest {
  bytes queue_id = 1;
  uint32 from_index = 2;           // Starting index
  uint32 max_count = 3;            // Default 10
}

message PollMessagesResponse {
  ResponseStatus status = 1;
  repeated Message messages = 2;
  bool more_available = 3;
}

message Message {
  uint32 index = 1;
  bytes ciphertext = 2;
  uint64 stored_at = 3;
  bytes server_signature = 4;     // Proof of storage from swarm
}
```

**Delete message (after read):**

```protobuf
message DeleteMessageRequest {
  bytes queue_id = 1;
  uint32 message_index = 2;
  bytes recipient_signature = 3;  // Proves recipient consents to delete
}
```

### 4.3 File transfer operations (XFTP layer)

**Upload shard:**

```protobuf
message UploadShardRequest {
  bytes shard_id = 1;              // SHA-256 of shard content
  bytes shard_data = 2;            // Up to 4 MB
  uint32 retention_hours = 3;      // How long to store
  bytes uploader_signature = 4;
}

message UploadShardResponse {
  ResponseStatus status = 1;
  bytes shard_id = 2;
  uint64 stored_until = 3;
  bytes server_receipt = 4;        // Signed by node for later verification
}
```

**Download shard:**

```protobuf
message DownloadShardRequest {
  bytes shard_id = 1;
  bytes requester_auth = 2;        // Authorisation proof
}

message DownloadShardResponse {
  ResponseStatus status = 1;
  bytes shard_data = 2;
  bytes server_signature = 3;
}
```

### 4.4 Response status codes

```protobuf
enum ResponseStatus {
  STATUS_UNKNOWN = 0;
  STATUS_OK = 1;
  STATUS_NOT_FOUND = 2;
  STATUS_UNAUTHORIZED = 3;
  STATUS_QUOTA_EXCEEDED = 4;
  STATUS_INVALID_ARGUMENT = 5;
  STATUS_TEMPORARILY_UNAVAILABLE = 6;
  STATUS_WRONG_SWARM = 7;
  STATUS_INTERNAL_ERROR = 8;
  STATUS_RATE_LIMITED = 9;
}
```

---

## 5. Onion routing protocol

### 5.1 Sphinx packet format

Based on the Sphinx paper (Danezis & Goldberg, 2009) with modern cryptography:

```protobuf
message SphinxPacket {
  bytes version = 1;               // 1 byte, protocol version
  bytes ephemeral_key = 2;         // 32 bytes, X25519 ephemeral public key
  bytes routing_info = 3;          // 384 bytes, per-hop encrypted routing
  bytes header_mac = 4;            // 32 bytes, HMAC of header
  bytes payload = 5;               // 16 KB (messages) or 400 KB (shards)
  bytes payload_mac = 6;           // 32 bytes, HMAC of payload
}
```

Total packet size: 16,480 bytes (messages) or 400,480 bytes (shards). Fixed size prevents traffic analysis.

### 5.2 Per-hop processing

Each hop performs these steps in constant time:

```
Receive SphinxPacket P from previous hop:
  1. Verify header_mac: H = HMAC-SHA256(our_session_key, header_fields)
     If H != P.header_mac: drop packet
  2. Compute ECDH shared secret: s = X25519(our_private_key, P.ephemeral_key)
  3. Derive keys from s: (next_session_key, payload_key, next_mac_key) = HKDF(s)
  4. Decrypt one layer of routing_info: next_routing = AES-CTR(session_key, P.routing_info[32:])
  5. Extract next hop info: (next_hop_address, next_header_mac) = next_routing[0:32]
  6. Compute next packet's ephemeral_key: P'.ephemeral_key = X25519_mul(P.ephemeral_key, blinding_factor)
  7. Construct P' with new routing, forward to next_hop
  8. Wait random 50-200ms (jitter for timing obfuscation)
  9. Forward P' to next_hop_address
```

### 5.3 Building an onion route

Client selects 3 intermediate nodes and constructs Sphinx packet:

```
Client selects route [N1, N2, N3, Target]:
  - N1: entry guard (semi-persistent per session)
  - N2: middle relay (random per message)
  - N3: exit relay (chosen near target's swarm)
  - Target: swarm member for recipient queue

Construct Sphinx packet:
  Layer 4 (target): payload = inner message
  Layer 3 (N3): encrypt layer 4 with N3's pubkey
  Layer 2 (N2): encrypt layer 3 with N2's pubkey
  Layer 1 (N1): encrypt layer 2 with N1's pubkey
  
  Final packet has 4 nested encryption layers
  Each hop peels one layer, sees only next hop's identity
```

### 5.4 Entry guard selection

To resist statistical deanonymisation attacks, clients use semi-persistent entry guards:

- Client randomly selects 3 entry guards at first connection
- Entry guards rotate every 30-60 days
- Client avoids switching guards unless unavailable
- Prevents global adversary from learning user's usage patterns through constant guard churning

---

## 6. Node-to-node (swarm) protocol

### 6.1 Swarm membership

When a node registers on Arbitrum, smart contracts emit `NodeRegistered` event. Other nodes observe this event and update their swarm membership tracking.

```protobuf
message SwarmMembership {
  uint64 epoch = 1;                // Epoch number
  bytes swarm_id = 2;              // 32 bytes
  repeated SwarmMember members = 3;
}

message SwarmMember {
  bytes operator_pubkey = 1;       // Ed25519
  bytes network_address = 2;       // Encoded endpoint
  uint32 slot_index = 3;           // Position within swarm (0 to 9)
  uint64 joined_at = 4;
}
```

At each epoch boundary (every 24 hours), the VRF beacon determines which nodes belong to which swarms. Nodes compute this locally from on-chain data.

### 6.2 Replication protocol

When a node receives a message from a client, it replicates to other swarm members:

```
Node A (primary, received message M from client):
  1. Store M locally
  2. Compute replication_id = SHA-256(M || timestamp)
  3. For each peer N in swarm:
     Send REPLICATE(M, replication_id) to N
  4. Wait for 3 of 5-10 ACKs (quorum)
  5. Return success to client

Node N (replica):
  1. Receive REPLICATE from A
  2. Verify A is current swarm member
  3. Check if M already stored (idempotency)
  4. Store M locally if not already
  5. Return REPLICATE_ACK(replication_id) to A
```

```protobuf
message ReplicateRequest {
  bytes replication_id = 1;
  bytes queue_id = 2;
  uint32 message_index = 3;
  bytes ciphertext = 4;
  uint64 timestamp = 5;
  bytes primary_signature = 6;     // Primary node signs for authentication
}

message ReplicateAck {
  bytes replication_id = 1;
  bool stored = 2;                 // false = already had it
  bytes peer_signature = 3;        // Peer signs confirmation
}
```

### 6.3 Anti-entropy (gossip repair)

Nodes periodically exchange message inventories to detect and repair missing replications:

```protobuf
message InventoryRequest {
  bytes queue_id = 1;              // Or all queues if omitted
  uint32 min_index = 2;
  uint32 max_index = 3;
}

message InventoryResponse {
  bytes queue_id = 1;
  repeated uint32 stored_indices = 2;
  bytes bloom_filter = 3;          // For large sets, bloom instead of list
}
```

Repair strategy:

- Every 10 minutes, each node picks random peer
- Exchange inventories for one queue at a time
- If peer has message this node is missing, request it
- If this node has message peer is missing, offer it
- Detects and repairs replication gaps without central coordinator

### 6.4 Swarm consensus

For operations requiring swarm-wide agreement (e.g., slashing evidence), nodes use a lightweight BFT protocol:

```protobuf
message ConsensusProposal {
  bytes proposal_id = 1;
  uint64 epoch = 2;
  ProposalType type = 3;           // e.g., slash_accusation, parameter_change
  bytes proposal_data = 4;
  bytes proposer_signature = 5;
}

enum ProposalType {
  PROPOSAL_UNKNOWN = 0;
  PROPOSAL_SLASH_ACCUSATION = 1;
  PROPOSAL_PARAMETER_CHANGE = 2;
  PROPOSAL_MEMBERSHIP_CHANGE = 3;
}

message ConsensusVote {
  bytes proposal_id = 1;
  bool approve = 2;
  bytes voter_signature = 3;
}
```

Consensus achieved when 2/3+ of swarm members approve within time window.

---

## 7. Audit protocol

### 7.1 Challenge format

```protobuf
message AuditChallenge {
  bytes challenge_id = 1;          // 32 bytes, unique
  bytes target_node = 2;           // Ed25519 pubkey of target
  ChallengeType type = 3;
  bytes target_block_id = 4;       // Specific block to prove
  bytes challenge_data = 5;        // Type-specific parameters
  uint64 deadline = 6;             // Unix seconds, response deadline
  bytes committee_signature = 7;   // Threshold sig from audit committee
}

enum ChallengeType {
  CHALLENGE_UNKNOWN = 0;
  CHALLENGE_HMAC = 1;              // Compute HMAC over block
  CHALLENGE_PARTIAL_HASH = 2;      // Hash specific byte range
  CHALLENGE_MERKLE_PATH = 3;       // Provide Merkle inclusion proof
}
```

### 7.2 Challenge types

**Type 1: HMAC challenge**

```
Challenge: "Prove you have block B"
Data: challenge_data = nonce (random 32 bytes)

Response: HMAC-SHA256(node_secret || nonce, block_content)
```

**Type 2: Partial hash challenge**

```
Challenge: "Hash bytes X to Y of block B"
Data: challenge_data = (offset uint32, length uint32)

Response: SHA-256(block_content[offset:offset+length])
```

**Type 3: Merkle path challenge**

```
Challenge: "Provide Merkle path to prove block B in your set"
Data: challenge_data = Merkle root (32 bytes)

Response: inclusion proof (sibling hashes from block to root)
```

### 7.3 Response format

```protobuf
message AuditResponse {
  bytes challenge_id = 1;
  bytes target_node = 2;
  bytes response_data = 3;         // Type-specific response
  uint64 computed_at = 4;
  bytes node_signature = 5;        // Ed25519 signature by target node
}
```

### 7.4 Challenge frequency and distribution

Each node receives approximately 10 challenges per hour, distributed uniformly at random times:

```
Challenge scheduling:
  Every hour, audit coordinator:
    1. Sample random nodes from active set
    2. For each sampled node:
       a. Select random blocks the node claims to store
       b. Generate appropriate challenge type
       c. Sign challenge with committee threshold signature
    3. Dispatch challenges via BFT appchain gossip
    4. Collect responses over next 60 minutes
    5. Score responses: correct + fast = best
    6. Update reputation database
```

---

## 8. Error handling

### 8.1 ERROR frame

```protobuf
message Error {
  ErrorCode code = 1;
  string message = 2;              // Human-readable
  bytes details = 3;               // Structured details (if any)
  uint32 correlates_with = 4;      // reserved_id of failed operation
}

enum ErrorCode {
  ERROR_UNKNOWN = 0;
  ERROR_PROTOCOL_VERSION = 1;      // Unsupported protocol version
  ERROR_AUTHENTICATION_FAILED = 2;
  ERROR_AUTHORIZATION_FAILED = 3;
  ERROR_MALFORMED_FRAME = 4;
  ERROR_RATE_LIMITED = 5;
  ERROR_STORAGE_FULL = 6;
  ERROR_INTERNAL = 7;
  ERROR_TIMEOUT = 8;
  ERROR_CONNECTION_LOST = 9;
}
```

### 8.2 Retry strategy

Client-side retry rules:

| Error code | Retry? | Backoff |
|:-----------|:-------|:--------|
| TEMPORARILY_UNAVAILABLE | Yes | Exponential, max 30s |
| RATE_LIMITED | Yes | Respect Retry-After if provided |
| STORAGE_FULL | No | Switch to different node |
| TIMEOUT | Yes | Linear, max 10s |
| AUTHENTICATION_FAILED | No | Fix auth, try again |
| PROTOCOL_VERSION | No | Fail fast, user error |

### 8.3 Circuit breaker

Clients maintain a circuit breaker for each node connection:

```
State: CLOSED (normal), OPEN (failing), HALF_OPEN (testing recovery)

CLOSED -> OPEN when:
  - 5 consecutive failures in 30 seconds, OR
  - Error rate > 50% over 10 requests

OPEN -> HALF_OPEN after:
  - 60 seconds cooldown

HALF_OPEN -> CLOSED when:
  - 3 consecutive successes

HALF_OPEN -> OPEN when:
  - Any failure
```

---

## 9. Rate limiting

### 9.1 Default limits

Per-client limits to prevent resource exhaustion:

| Operation | Free tier | Pro tier |
|:----------|:----------|:---------|
| Messages per queue per hour | 120 | 3,600 |
| New queues per day | 5 | 100 |
| File uploads per hour | 10 (100 MB each max) | 100 (10 GB each max) |
| File downloads per hour | 100 | 1,000 |
| Audit responses per hour | unlimited | unlimited |

### 9.2 Quota enforcement

```
On each request:
  1. Compute client_identifier = hash(TLS client cert public key)
  2. Look up quota bucket for client_identifier
  3. Check if operation allowed under current bucket
  4. If allowed: decrement bucket, allow operation
  5. If not: return ERROR_RATE_LIMITED with retry_after
  6. Refill bucket based on rate (e.g., 1 msg / 30 sec)
```

### 9.3 DDoS protection

At the TLS/network layer:

- SYN flood protection (Linux kernel defaults)
- Connection limit per source IP (100 concurrent)
- Request rate limit per IP (1000 req/min for anonymous, unlimited for authenticated)
- Priority queue for established clients with good reputation
- Tarpitting for suspected attackers (slow but not blocked)

---

## 10. Wire protocol versioning

### 10.1 Version negotiation

HELLO frame includes `protocol_version`. Both parties must support a common version:

```
If client.version == server.version:
  Use this version
Else:
  Return ERROR_PROTOCOL_VERSION
```

No version negotiation downgrade (prevents downgrade attacks).

### 10.2 Versioning strategy

| Change type | Handling |
|:-----------|:---------|
| New frame type | Minor version bump, both sides must support |
| New field in message | Backward-compatible (protobuf field numbers) |
| Breaking schema change | Major version bump, coordinated rollout |
| Security fix | Immediate release, old versions deprecated |

### 10.3 Deprecation timeline

- New version announced: 6 months before default switch
- Default switch: new implementations use new version
- Old version deprecated: 12 months after announcement
- Old version EOL: 18 months after announcement

---

## 11. Reference implementation

The reference implementation is written in Go and available at github.com/saschadaemgen/GoNode. Alternative implementations are encouraged:

| Language | Status | Maintainer |
|:---------|:-------|:-----------|
| Go | Primary | Foundation |
| Rust | Planned (Phase 2) | Community + Foundation |
| TypeScript | Planned (Phase 3) | Community |
| Python | Planned (Phase 4) | Community |
| Swift/Kotlin | Future | For mobile clients |

Test vectors and compliance test suite published in `tests/protocol-compliance/`.

---

## 12. Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [GoNode Architecture](ARCHITECTURE_AND_SECURITY.md) | Full architecture context | This repo |
| [GoNode Smart Contracts](SMART_CONTRACTS.md) | Economic layer interfaces | This repo |
| [SimpleGo SMP](https://github.com/saschadaemgen/SimpleGo) | Inner protocol layer | SimpleGo repo |
| [GoBot Wire Protocol](https://github.com/saschadaemgen/GoBot) | Client integration example | GoBot repo |

---

*GoNode Wire Protocol v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
