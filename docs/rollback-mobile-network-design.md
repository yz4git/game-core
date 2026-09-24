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

## Mobile Safari / browser performance budget — Batch 27

Rollback performance must be budgeted as a burst workload. One late remote input can require state restore plus several simulation ticks before the next visible frame, so average offline frame time is insufficient.

### Reserve headroom

For each supported mobile performance tier measure separately:
- normal simulation tick p50/p95/p99
- rendering p95/p99
- network processing p95
- snapshot save/load p95
- rollback re-simulation burst p95/max
- input-to-present p95

Do not intentionally fill the entire frame budget in ordinary offline play. The unused margin is resilience capacity for rollback, runtime/GC work and OS/browser variance.

### Bound state-history memory

Track:
- serialized authoritative bytes per state
- history ring-buffer capacity
- history high-water bytes
- temporary restore/copy high-water

Rollback memory is approximately state size × retained history plus working copies. Repeated deep rollback must not produce unbounded growth.

### Keep the rollback hot path allocation-stable

Reuse snapshot buffers, input/event arrays and scratch state where practical. A rollback burst multiplies allocation-heavy code and can turn correction into a garbage-collection spike.

### Never render every re-simulated tick

Intermediate catch-up frames need authoritative simulation, not full presentation. Simulation must advance with particles, camera, UI, audio and haptics suppressed or event-deduplicated.

### Display refresh is not simulation rate

`requestAnimationFrame()` follows the display's presentation cadence. Keep gameplay on an explicit fixed simulation clock so 60 Hz and high-refresh displays do not change game speed or deterministic results.

### Background/resume is a discontinuity

Hidden browser pages may stop animation callbacks and throttle timers. Do **not** interpret a long hidden interval as thousands of simulation ticks to catch up.

On resume, when authority may be stale, use:

VISIBLE
→ VERIFY SESSION
→ SNAPSHOT / DELTA
→ CATCHUP
→ READY

No stale world state should become actionable while this recovery is unresolved.

### Capability-layered telemetry

Browser performance APIs differ in support. Always keep app-level timing for simulation/render/rollback. Add PerformanceObserver, long-frame attribution or other browser metrics only when capability detection says they are available. Never depend on `deviceMemory` or a hardware fingerprint for correctness.

### Sustained mobile test

Cold-device benchmarks are insufficient. Run 20–30 minute fault traces and compare early versus late distributions for:
- simulation/render p95
- rollback burst time
- missed-frame rate
- correction magnitude
- reconnect time

This reveals lost headroom during sustained CPU/GPU load.

### Degradation ladder

When sustained budget pressure is detected, reduce presentation before game truth:
1. cosmetic particle/effect density
2. render resolution / DPR
3. expensive post effects and shadows
4. nonessential remote presentation detail

Do not alter authoritative collision, RNG, AI decisions, command timing or fixed simulation rules as a performance fallback.

### Compute-safe rollback limit

Treat the usable rollback window as:

`maxRollbackFrames = min(network-policy limit, compute-safe limit, memory-safe limit)`

If required rollback exceeds that envelope, transition to the defined delay/degraded/reconnect policy instead of entering an uncontrolled catch-up spiral.

## Authority migration boundary — Batch 31

Rollback/reconnect and host migration share state-history machinery but solve different failures. A reconnect assumes a valid authority still exists; host migration must first create a new authority and reconstruct canonical state.

Keep these phases distinct:

`HOST_LOST → COMMIT_BARRIER → ELECT → RESTORE → SEMANTIC_VALIDATE → RESYNC → READY`

Key rules:
- host election does not imply world-state migration
- transport connection ID is not player identity
- lobby/session ownership is not simulation authority
- advance an authority epoch/term on migration so stale hosts/packets cannot overwrite new truth
- migration checkpoints need ownership, RNG/event sequence, match phase and one-shot-event dedupe state in addition to ordinary world state
- choose candidates only after compatibility/state-integrity gates; then rank network/compute quality
- every network entity class needs an owner-disconnect policy
- do not reopen actionable input until semantic invariants pass

See `docs/host-authority-migration.md` for the production state machine and fault-injection matrix.

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
- Does common rollback depth fit inside reserved headroom on the slowest supported phone?
- Is rollback state-history memory bounded after repeated deep corrections?
- Is the re-simulation hot path allocation-stable after warm-up?
- Does 60/120 Hz presentation leave simulation speed unchanged?
- Does background/resume resynchronize rather than perform giant fixed-step catch-up?
- Does adaptive quality shed presentation before authoritative simulation?
- Does a sustained 20–30 minute run preserve enough rollback headroom?
- Can asymmetric host loss ever create two active authority epochs?
- Can a former host reconnect without restoring stale authority?
- Is checkpoint age within the acceptable lost-gameplay budget?
- Are unique rewards/scores/object ownership valid after migration at their transaction boundaries?
