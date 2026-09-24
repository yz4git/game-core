# Host and Authority Migration

## Goal

Peer-hosted multiplayer should survive loss of the current host without creating two truths, duplicating players/rewards, or pretending that lobby ownership alone restores the match.

## Separate the roles

Treat these as distinct even when one machine normally holds all of them:
- lobby/session owner
- simulation authority
- per-object authority
- transport connection
- stable match-scoped player identity

Changing one role must not silently grant another.

## Migration lifecycle

Recommended production state machine:

```text
RUNNING(epoch N)
→ HOST_SUSPECTED
→ HOST_LOST
→ COMMIT_BARRIER
→ ELECT
→ HOST_ELECTED(epoch N+1)
→ RESTORE CHECKPOINT
→ REBIND IDENTITIES / OWNERSHIP
→ SEMANTIC VALIDATION
→ RESYNC PEERS
→ READY BARRIER
→ RUNNING(epoch N+1)
```

Election and world restoration are separate success conditions.

## Authority epoch

Every authoritative state/change should be attributable to an authority epoch or term. When migration advances from N to N+1, late packets or a returning former host from epoch N cannot overwrite newer truth.

Test asymmetric partitions where different peers detect host loss at different times. The design must not permit split-brain authority.

## Candidate selection

Apply correctness gates before performance ranking.

Eligibility:
- authenticated current member
- compatible protocol/build/content
- sufficient migration checkpoint/state
- no integrity/desync failure

Then rank eligible candidates using measured properties such as:
- connection stability / loss / jitter
- reachability to remaining peers
- sustained simulation headroom
- rollback/resimulation budget

Do not elect solely by lowest ping or strongest device if that peer cannot reconstruct authoritative state.

## Migration checkpoint

A survivable checkpoint should include or reconstruct:
- session/match ID
- protocol/build/content version
- authority epoch and tick
- stable player IDs
- world state
- ownership/authority map
- match phase/timers
- RNG/event sequence state
- committed score/objective/economy state
- one-shot event/grant dedupe IDs
- integrity checksum

Checkpoint cadence is a fairness budget. Measure how much confirmed-looking gameplay can be lost at the worst failure timing.

## Identity and reconnect

Transport IDs are disposable. Gameplay identity is not.

Use stable match-scoped player IDs/reconnect credentials so a new connection can reclaim the correct avatar, inventory, score and owned objects without spawning duplicates.

A returning former host joins the new epoch as an ordinary peer unless an explicit handoff protocol says otherwise.

## Object disconnect policy

Every authoritative network entity class should choose one policy:
- transfer authority
- freeze until owner returns
- AI takeover
- persist unowned
- expire after grace period
- destroy

Test soft disconnect and hard loss separately.

## Commit barrier

During authority ambiguity, do not let unbounded speculative gameplay create two branches. Use a short explicit barrier. Inputs may be queued only when their later acceptance can be determined safely.

Be especially strict for:
- purchases/currency
- unique pickups/rewards
- match-ending scores
- irreversible objective transitions
- ownership transfers

## Semantic validation before resume

Deserialization success is insufficient. Validate:
- unique player/entity identity
- exactly one valid simulation authority
- ownership references resolve
- score/progression does not regress illegally
- timers/match phase are coherent
- unique rewards are not duplicated
- RNG/event sequence is legal
- objective ownership is consistent

Only then reopen actionable input.

## UX

Communicate distinct stages rather than a generic spinner:
- HOST LOST
- RESTORING MATCH
- SYNCING PLAYERS
- RESUMING

Do not display success before semantic validation. Make it clear whether actions issued near the failure boundary counted.

## Telemetry

Track:
- host-loss reason
- election ms
- restore ms
- total control-unavailable ms
- checkpoint age at loss
- restored tick distance
- candidate rejection reason
- orphan/transfer entity counts
- semantic invariant failures
- reconnect attempts
- post-migration desync
- completion rate after migration
- quit rate shortly after migration

## Fault injection

Kill or partition the host during:
- idle movement
- combat/hit resolution
- unique reward grant
- finish/goal/score adjudication
- round/scene transition
- ownership transfer
- another client's reconnect
- burst loss/jitter
- mobile background/suspend
- checkpoint creation

Run with asymmetric partitions and different peer counts. A migration system tested only by cleanly pressing “Leave” is not production-tested.

## Playtest questions

- Does host election ever complete before world restoration and incorrectly resume play?
- Can two peers believe they are authority?
- Can reconnect duplicate a player or reward?
- Can the former host return with stale state?
- What is the worst acknowledged gameplay lost from checkpoint age?
- Are object ownership policies visible and deterministic?
- Can a migration during an irreversible transaction be reconciled?
- Does the slowest eligible mobile host retain enough sustained CPU/network headroom?
- Do players understand what happened and whether their last action counted?
