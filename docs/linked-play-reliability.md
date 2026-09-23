# Linked Play Reliability

Networked multiplayer should be designed as a lifecycle, not only a match simulation.

## Explicit lifecycle

Model setup as:

`discover → identify → join → synchronize → ready → play → reconnect/leave`

Every transition needs timeout, retry and cancellation behavior.

## Identity and authority

Make participant identity, room/session identity and authority explicit. Never depend on connection order remaining stable after refresh/reconnect.

## Idempotent setup

Repeating join/setup must converge safely. Test duplicate requests, stale rooms, host not ready, reconnect during sync, refresh during join and simultaneous joins.

## Network diagnostics

Separate network health from gameplay quality. Record RTT, jitter, packet loss, disconnect/reconnect, correction/rollback count and resync duration. A bad prediction algorithm and a bad connection are different bugs.

## Public/team play

When several players share a public event, expose who is connected, ready, missing and reconnecting. Results should make meaningful contribution visible without turning diagnostics into blame.

## QA questions

- Can an interrupted setup recover without manual reset?
- Does reconnect preserve the correct identity?
- Can a stale client corrupt the active session?
- Can QA identify transport failure separately from simulation divergence?
- Is the match still understandable when one participant temporarily disappears?