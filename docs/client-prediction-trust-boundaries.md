# Client Prediction Trust Boundaries

## Goal

Keep network action responsive **without letting low-latency prediction become authority**. Security here is a gameplay architecture problem: decide what a client may predict, request, author, observe and make durable.

## Trust matrix first

For each domain define:

`domain | predict? | request? | author? | validator | time bound | idempotency key | visibility | durable consequence`

Do this for locomotion, aim, fire, hit, damage, pickup, ownership, score, result, currency, unique rewards, inventory and hidden opponent state.

## Prefer intent over claimed results

When authority can reconstruct the outcome, clients should send the smallest useful decision:
- input sequence + movement intent rather than final position
- fire/aim/timestamp rather than damage amount
- pickup request rather than inventory mutation
- purchase request rather than currency balance

The authority validates and applies the result.

## Validation pipeline

`REQUEST → ID/EPOCH → TEMPORAL WINDOW → RULE/STATE INVARIANTS → APPLY → ACK → RECONCILE → PRESENT`

Useful invariants:
- monotonic input/action sequence
- valid authority epoch/ownership generation
- maximum movement/state delta per time interval
- cooldown/action-rate bounds
- resource prerequisites
- valid match phase
- bounded lag-compensation timestamp
- unique grant/pickup not previously committed

Retries must pass the same gates. Irreversible actions need idempotency keys.

## Prediction and reconciliation

Prediction may make movement, animation and action feedback immediate. It remains provisional until authoritative acknowledgement.

On mismatch:
1. restore/apply canonical state
2. replay still-valid local inputs where appropriate
3. keep cosmetic smoothing out of authoritative collision/rules
4. deduplicate audio/particles/haptics by event identity

Never preserve a visually smooth but gameplay-false state just to hide correction.

## Lag compensation boundary

Server-side rewind improves honest high-latency aiming, but the rewind window is also an acceptance window for historical claims.

Define per action class:
- maximum rewind age
- accepted timestamp source/range
- history retained
- sub-tick policy
- occlusion/geometry rules
- defender-facing presentation

Telemetry: accepted rewind p50/p95/max, timestamp clamps/rejects and outcome changes near the boundary.

## Ownership is not authority

Keep separate concepts:
- identity: which player/account this is
- ownership: which player logically possesses/controls an object
- input authority: who may request control changes
- state authority: who defines canonical state
- visibility authority: which state the peer may observe

Version authority transfer with monotonic generation/epoch IDs. Old generations cannot reclaim truth because a delayed packet arrives later.

## Topology is a trust classification

### Dedicated/trusted authority
Strongest fit for ranked outcomes and valuable durable rewards.

### Listen host
Can validate guests, but the host process itself is participant-controlled. Store provenance; do not silently equate its integrity with a trusted dedicated service.

### Shared/client authority
Can provide excellent latency characteristics, but requires explicit extra validation for competitive consequences.

### Relay-only
The relay transports messages without understanding game truth. Treat match integrity as client-defined unless another validator exists.

A game can mix tiers: predicted movement may be low-trust while currency, unique rewards and ranked results require stronger authority.

## Hidden information

Server-authoritative writes do not stop wall-hacks if the client receives secret state.

Use least-privilege replication:
- interest management
- fog-of-war/server projection
- TEAM/PARTICIPANT/PUBLIC/PRIVATE/DEBUG visibility classes
- spectator-specific schemas

Measure hidden/private bytes delivered to clients that do not need them.

## Explainable security telemetry

Prefer concrete invariant events over an opaque cheat score:
- stale/duplicate input sequence
- timestamp clamp/reject
- movement envelope breach
- cooldown violation
- impossible resource delta
- stale authority generation
- duplicate grant suppression
- excessive rewind request
- invalid phase transition

Keep a short reproducible trace around severe events. Enforcement policy can aggregate evidence later.

## False-positive fault testing

Run honest clients through:
- high jitter
- burst loss
- reordering
- background/resume
- reconnect
- host migration
- duplicate delivery/retry

Measure false rejects, correction magnitude and violation events. A security rule that punishes normal network disorder is not production-ready.

## Playtest / review questions

- Can a client report a result that authority cannot derive or bound?
- Are time/rate constraints checked as well as numeric ranges?
- Can duplicate/replayed requests create a second irreversible result?
- Does ownership grant more write power than required?
- Can stale authority packets win after transfer/migration?
- Is ranked/reward eligibility appropriate for the session topology?
- Does lag compensation have a bounded, explainable fairness window?
- Are honest bad-network traces falsely flagged?
- Can presentation smoothing make the visible state contradict authoritative affordances?
- Does the client receive hidden information it never needs to render?

## Relationship to other guides

- `rollback-mobile-network-design.md`: prediction, rollback, correction, mobile performance
- `host-authority-migration.md`: authority loss/election/state restoration
- `replay-lifecycle-privacy.md`: public/private replay fields and archival trust
- `save-resilience-and-migration.md`: durable state, unique grants and idempotent recovery
