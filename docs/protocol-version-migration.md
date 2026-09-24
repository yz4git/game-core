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

An additive/defaultable field can permit an older reader or writer in one direction without proving the reverse path.

## Capability negotiation
For graceful mixed-version operation, negotiate explicit feature IDs. Required capability mismatch rejects the connection. Optional capability intersection defines which optional behavior may be used. Never guess feature support from semantic version ordering alone.

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

## Failure UX
Unsupported clients should get a deterministic reason rather than a generic network error:
- update required
- session is on an older incompatible version
- server cohort temporarily unavailable
- optional feature unavailable but session can continue

Never auto-retry an incompatibility forever.

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

## CI fixture corpus
Preserve representative artifacts per supported epoch:
- handshake/fingerprint fixtures
- RPC/command serialization fixtures
- replicated snapshots
- reconnect/session metadata
- migration checkpoints
- invites/join references

Test N/N, every advertised mixed-version path, and clean rejection of unsupported pairs. Include cached web client, reconnect after app update, rolling server deployment and host migration.

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
