# Rollback and Mobile Network Action

## Goal

Fast networked games cannot remove propagation delay. They decide **where the delay and uncertainty become visible**. The design target is to preserve the genre's important decisions while making corrections understandable and bounded.

## Architecture by gameplay need

### Rollback / input prediction
Good fit when local input timing is critical and simulation can be deterministic/recoverable.

Requirements:
- deterministic gameplay simulation
- compact restorable state
- input history
- fast re-simulation
- side effects separated from authoritative logic
- desync checks

### Snapshot interpolation
Good fit for many remote/world actors where smooth presentation matters more than showing their newest state instantly.

Costs:
- intentional remote presentation delay
- bandwidth versus snapshot-rate trade-off

### State synchronization
Useful for non-deterministic physics. Synchronize enough state to extrapolate, correct authoritative simulation, then smooth only presentation.

## Delay versus correction budget

Measure together:
- local input delay
- rollback frequency
- rollback depth
- correction magnitude
- prediction hit rate

A tiny fixed delay can be preferable if it removes many visible corrections. Do not tune from ping alone.

## Jitter and packet-loss policy

Track:
- RTT median and p95
- jitter p95
- isolated loss
- burst-loss length
- reordering
- effective update cadence

Use a bounded prediction/extrapolation horizon. When confidence expires, transition to an explicit degraded/reconnect state instead of inventing increasingly wrong gameplay.

## Lag compensation as rules

Define:
- which interactions are rewindable
- maximum rewind duration
- what historical state is retained
- whether projectiles/hitscan/melee differ
- what the defender sees
- how replays explain adjudication

Fairness is not simply "maximum compensation"; it is a documented temporal policy that remains understandable at its limits.

## Reconnect state machine

Recommended lifecycle:

DISCONNECTED
→ RECONNECTING
→ AUTHENTICATING
→ SNAPSHOT
→ CATCHUP
→ READY

Do not allow actionable stale state during recovery. Define what happens to queued local inputs and ownership/authority changes.

## Mobile fault scenarios

Test changing conditions, not only fixed latency:
- stable Wi-Fi → jitter spike → recovery
- Wi-Fi → cellular-like loss profile
- burst loss during attack/turn/collision
- background/suspend → resume
- reconnect during authority migration
- bandwidth collapse while snapshots continue
- repeated short disconnects

## Determinism / desync diagnostics

Failure artifacts should preserve:
- build/protocol version
- match seed
- tick
- recent inputs
- RNG state or stream identifiers
- global checksum
- subsystem hashes
- earliest divergent tick

A final-state mismatch alone is insufficient.

## Presentation boundary

Authoritative correction can be immediate while presentation is smoothed. Never let cosmetic smoothing feed back into collision, hit timing or authoritative physics.

Audio, particles, camera shake and haptics need rollback-safe event IDs so re-simulation does not duplicate them.

## Spectator / replay

Player compensation may use a different temporal view from spectators. Store enough event timing metadata that a replay does not make valid hits or collisions appear impossible.

## Playtest checklist

- Is local control responsive under expected RTT?
- Are corrections less harmful than equivalent input delay?
- Does jitter cause worse artifacts than stable high ping?
- Is extrapolation bounded?
- Can high-latency hits be explained?
- Can reconnect restore authority without stale interaction?
- Can the first desync tick be reproduced?
- Do rollback side effects duplicate?
- Does spectator playback agree with adjudicated results?
- Are mobile transition scenarios in automated QA?
