# Protocol and Version Migration for Networked Games

## Goal
Ship multiplayer updates without allowing incompatible clients to corrupt a session, while avoiding unnecessary population fragmentation.

## Compatibility identity
Do not use the player-facing version string as the only gate. Track at least:
- build ID — diagnostics/deployment identity
- protocol epoch — intentionally incompatible wire generation
- wire schema hash — RPC/command serialization contract
- replicated-state hash — authoritative replicated component contract
- rules/content compatibility ID — semantics that must agree
- required/optional capability IDs

Two builds may differ while remaining compatible; two builds with the same visible version may still be incompatible.

## Admission state machine
`TRANSPORT → HELLO → FINGERPRINT CHECK → CAPABILITY NEGOTIATION → AUTH → SESSION EPOCH → SNAPSHOT → VALIDATE → READY`

No actionable replicated entity should exist before compatibility is established.

## Compatibility matrix
Treat compatibility as potentially directional. Record separately:
- can read
- can write
- can join
- can host
- can reconnect
- can read replay
- can spectate recording

An additive/defaultable field can permit an older reader or writer in one direction without proving the reverse path. Live join and historical replay are different compatibility graphs: a pair may be unsafe for bidirectional live simulation but safe for one-way replay interpretation.

## Capability negotiation
For graceful mixed-version operation, negotiate explicit feature IDs. Required capability mismatch rejects the connection. Optional capability intersection defines which optional behavior may be used. Never guess feature support from semantic version ordering alone.

## Schema evolution rules
Treat serialized identities as durable API:
- never recycle retired field/RPC/component IDs inside an epoch
- reserve/tombstone removed identities
- prefer additive, defaultable fields when semantics permit
- unknown optional fields may be skipped only when they cannot change canonical outcome
- enum/state meaning changes require explicit migration, not merely a parser that accepts the number
- custom binary/NetSerialize-style payloads are explicit migration boundaries

Every custom serializer should carry its own format version and retain golden fixtures for each advertised reader path. CI should lint accidental ID reuse.

## Matchmaking
Protocol compatibility is an invariant, not a weighted preference:
1. compatibility cohort
2. trust/topology invariants
3. network playability floor
4. skill/party/mode constraints
5. preferences

Queue expansion must never cross an unsupported protocol boundary.

## Rolling deployment
Choose explicitly between:
- **hard cutover:** incompatible update; drain/finish old sessions and prevent cross-version joins
- **overlap:** N and N-1 are tested compatible; keep both server pools during adoption

Measure active-client adoption before retiring the old cohort. Web/PWA caches make stale clients a normal deployment case, not an exception.

## Session pinning
A running match owns a `sessionProtocolEpoch`. Deployment of a new build does not mutate that match's simulation semantics. New matchmaking can move to a newer epoch while old matches finish on their pinned epoch.

Reconnect checks the session epoch, not merely the latest production version.

## Host migration
Host candidates first pass:
- session protocol epoch
- schema/state compatibility
- required capabilities
- checkpoint readability

Only compatible candidates enter latency/compute/election scoring. Host election must not become an accidental protocol upgrade.

## Join references
Invites, reconnect tokens and cached network descriptors need:
- stable session identity
- protocol/session epoch
- expiry
- resolver indirection

Resolve the current endpoint and revalidate compatibility at join time; do not trust a cached endpoint indefinitely.

## Replay compatibility
Treat replay support as a first-class reader contract. A replay envelope should include at least:
`replayId, sourceBuildId, replayEpoch, networkVersion, rulesetId, contentId, schemaFingerprint, simulationFingerprint, requiredCapabilities, optionalCapabilities, checksumScheme`.

Recommended reader pipeline:
`CATALOG FILTER → ENVELOPE VERIFY → READER SELECTION → DEPENDENCY CHECK → DECODE → VERSIONED MIGRATION → SEMANTIC VALIDATION → CHECKSUM/DIVERGENCE CHECK → PLAYABLE | DEGRADED | MIGRATABLE | UNSUPPORTED`.

Compatibility metadata should be queryable before downloading or starting playback. UI can then distinguish playable, migratable, archive-only and unsupported recordings.

### Deterministic input replay
Input-only replay is not self-contained. The same inputs can diverge when simulation code, RNG order, physics, data tables, assets or configuration change. Record simulation/content fingerprints and periodic checksums. Either retain the compatible runtime/data bundle or provide an explicit transcode path.

### Snapshot checkpoints
Long event/input histories amplify migration risk. Periodic versioned canonical snapshots bound reconstruction depth. Migrate the checkpoint and the subsequent input/event tail independently, then validate their join.

### Dependency classes
Classify replay dependencies:
- simulation-critical
- interpretation-critical
- presentation-optional
- metadata-only

Only the latter categories may be omitted in degraded playback, and only when omission cannot alter canonical outcome.

### Transactional transcoding
Never overwrite the archival source. A converted replay is a new artifact containing source hash, converter version, target epoch and validation result. This preserves provenance and permits later correction of a faulty converter.

## Semantic validation
Deserialization success is not correctness. After schema conversion, validate:
- referenced entity/content existence or declared tombstones
- legal state-machine transitions
- ownership/authority invariants
- value/range constraints
- ruleset consistency
- deterministic checksum where applicable

A parser that produces impossible gameplay state is a failed migration.

## Failure UX
Unsupported clients should get a deterministic reason rather than a generic network error:
- update required
- session is on an older incompatible version
- server cohort temporarily unavailable
- optional feature unavailable but session can continue

Replay UI should likewise distinguish unsupported format, missing dependency, deterministic divergence, corruption and presentation-only degradation. Never auto-retry an incompatibility forever.

## Telemetry
Record without unnecessary personal data:
- client/server build IDs
- protocol/session epoch
- fingerprint mismatch category
- capability mismatch
- admission result
- reconnect result
- queue cohort population
- old-build adoption curve
- incompatibility rejection rate
- replay read attempts/results by epoch
- migration/transcode success rate
- first divergence tick/category

## CI fixture corpus
Preserve representative artifacts per supported epoch:
- handshake/fingerprint fixtures
- RPC/command serialization fixtures
- replicated snapshots
- reconnect/session metadata
- migration checkpoints
- invites/join references
- replay envelopes and recordings
- custom serializer boundary cases

Test N/N, every advertised mixed-version path, and clean rejection of unsupported pairs. Include cached web client, reconnect after app update, rolling server deployment and host migration.

For replay, test every advertised old→current reader path, removed/additive fields, unknown optional fields, changed enums, content drift, deterministic divergence, truncated/corrupt data, custom serializer versions, and transcode provenance. Run the oldest supported fixture, not only N-1.

## Compatibility retirement
Do not retire an old reader solely because it is old. Balance measured replay usage, maintenance/security risk, migration success and archival alternatives. Before removal, provide a validated export/transcode path when practical and preserve immutable source artifacts where policy permits.

## Release checklist
- Has compatibility changed semantically or only the build number?
- Is the protocol epoch bumped when required?
- Is N/N-1 support explicit and tested rather than assumed?
- Can matchmaking expansion cross protocol cohorts? It must not.
- Can an existing match finish after deployment?
- Can an updated client reconnect to an older live session safely?
- Can a stale invite resolve or fail clearly?
- Can host migration select only checkpoint-compatible peers?
- Are unsupported clients rejected before actionable state?
- Is old-cohort retirement based on measured adoption and active sessions?
- Were any serialized IDs reused after removal? They should not be.
- Does every custom serializer have a versioned old fixture?
- Can the current build read the oldest replay epoch it advertises?
- Does replay compatibility remain independent from live-join compatibility?
- Does migrated replay state pass semantic validation, not just decoding?
- Are deterministic replay dependencies fingerprinted and divergence checked?
- Does transcoding preserve the immutable source and provenance?
