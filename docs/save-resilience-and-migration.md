# Save Resilience & Migration

Save data is a compatibility and recovery system, not just serialization.

## 1. Version the schema explicitly

Every persisted state should carry a save-format version independent from the game/build version.

Keep released migrations. A player can skip multiple updates and return years later.

## 2. Use sequential migrations

Prefer:

`v1 → v2 → v3 → current`

over one opaque `old → current` converter.

Each step should have one purpose and a regression fixture.

## 3. Validate semantics after parsing

A file can parse successfully and still be invalid.

Validate at minimum:
- finite numeric values
- enum/range validity
- required IDs/references
- inventory/capacity invariants
- progression consistency
- world/slot identity
- generator/content compatibility where relevant

Do this after deserialization and after migration.

## 4. Make saving transactional

Use the conceptual sequence:

1. serialize candidate
2. write candidate/staging state
3. verify integrity and semantics
4. commit/advance active pointer
5. retain previous known-good generation

Never overwrite the only known-good state before the replacement is validated.

For IndexedDB, treat transaction `complete` as the success boundary. A successful individual request is not enough to display SAVE COMPLETE.

## 5. Keep a recovery horizon

Do not keep only several nearly identical autosaves.

Useful layers:
- current candidate
- previous known-good
- session-start backup
- milestone backup
- optional manual/export snapshot

This protects against corruption discovered late.

## 6. Diagnose before repair

Recovery should initially be read-only.

Inspect active and backup generations, select a valid source, copy it into a candidate, validate, then commit. Do not mutate the original evidence while diagnosing.

## 7. Preserve the pre-migration generation

Do not immediately destroy the old-format save after a migration appears to succeed. Keep it until the migrated state has passed validation and a safe later commit.

## 8. Treat cloud sync as history reconciliation

Two devices can both contain valid but divergent progress.

Persist enough metadata to reason about that history:
- save UUID
- revision
- base/parent revision where useful
- timestamp
- device/session identifier
- progression summary

Do not assume newest timestamp always represents the desired state.

## 9. Make conflicts understandable

When automatic merge is unsafe, present gameplay meaning rather than filenames:
- chapter/location
- playtime
- level
- important unlocks
- timestamp
- device

The player should be able to predict what choosing either side will preserve or lose.

## 10. Separate identity from mutable state

Validate:
- owner/profile
- slot/world ID
- save UUID
- schema version
- content/game version

A valid payload bound to the wrong identity is not automatically safe to load or merge.

## 11. Reject future schemas safely

If a save schema is newer than the running code understands:
- do not guess
- do not autosave over it
- preserve the bytes/state
- explain that a newer compatible build is required

## 12. Export/import safely

Where appropriate, exported snapshots should include:
- schema version
- save UUID
- revision
- timestamp
- game/build metadata
- integrity checksum/signature as appropriate

Validate imported state before replacing local state.

## 13. CI fault matrix

Test more than normal save/load:
- every historical schema fixture
- truncated candidate
- invalid checksum
- malformed but parseable values
- interruption between stage and commit
- future schema
- duplicate/stale revision
- divergent offline device branches
- failed migration step
- recovery from previous generation

The key metric is not “did load fail?” but “could this fault erase all recoverable progress?”

## 14. Treat browser quota as runtime state

Do not hardcode a presumed browser save capacity. Query `navigator.storage.estimate()` where supported and treat both usage and quota as approximate values.

Keep headroom rather than filling the reported quota. A valid write can still fail with `QuotaExceededError`.

## 15. Separate atomicity from retention

An IndexedDB transaction can commit atomically and the origin can still be evicted later under browser/device storage policy.

These are different guarantees:
- transaction atomicity: this save operation is all-or-nothing
- persistence/retention: committed data remains available later

Request persistent storage where appropriate, but treat grant/denial as a runtime capability rather than a correctness prerequisite.

## 16. Give storage classes explicit priority

Recommended order under pressure:

1. active/current known-good save
2. previous known-good / milestone recovery
3. user-authored or explicitly pinned content
4. unpinned replay/highlight cache
5. regenerable asset/cache data

A replay cache or offline asset cache must not be allowed to consume the reserve needed for the next critical checkpoint.

## 17. Reserve peak transactional footprint

Steady-state save size is not enough. Migration or staged replacement can temporarily require old + candidate + metadata + validation working state.

Maintain a critical reserve sized for the largest expected transaction, and prune disposable data before crossing it.

## 18. Make quota failure recoverable

On quota/storage failure:

1. do not destroy known-good data
2. classify the failure
3. prune only disposable classes
4. re-estimate if possible
5. retry a bounded number of times
6. expose recovery/export guidance if the save still cannot commit

Never loop indefinitely or silently pretend the save succeeded.

## 19. Detect origin-wide loss separately from corruption

If all local stores disappear together, treat that differently from a malformed record. Browser eviction, explicit site-data deletion and private browsing lifecycle can remove the whole local origin state.

Before silently creating a replacement campaign, check whether account/cloud/export evidence indicates recoverable prior progress.

## 20. Test runtime contexts separately

For browser games, test at least:
- normal Safari/browser tab
- Home Screen PWA where supported
- private browsing where relevant
- low-storage device condition
- persistence granted / denied / unsupported

The same URL does not imply the same durability policy in every runtime context.

## 21. Keep storage telemetry structural

Useful diagnostics:
- estimated usage/quota ratio
- persistence/durability tier
- candidate save bytes
- number and age of recovery generations
- transaction outcome
- quota/I/O failure class
- cleanup class and bytes reclaimed

Avoid uploading raw save payloads when these structural metrics are sufficient.

## 22. Version content dependencies separately from the save schema

A save can have a supported schema but still reference absent DLC, mods, remote catalogs, maps, scripts, items or quests.

Persist a content manifest or manifest hash and enough stable dependency identity to diagnose the mismatch before mutating state.

## 23. Classify missing dependencies by criticality

Useful classes:
- OPTIONAL — cosmetic/presentation-only; safe placeholder may exist
- DEGRADABLE — gameplay state can continue under an explicit fallback
- REQUIRED — normal play should not continue until restored/remapped
- WORLD-CRITICAL — defines the current simulation space or indispensable progression

Do not use one universal `null` fallback.

## 24. Use immutable persistent IDs, remaps and tombstones

Display names, asset paths and package layout change over time. Persist logical IDs that survive refactors.

For shipped IDs:
- rename via explicit remap/alias tables
- never guess from similar strings
- tombstone removed IDs so unrelated future content cannot accidentally reuse them

## 25. Separate entitlement from content presence

DLC can be owned but not currently installed or available. Likewise, local files alone do not necessarily prove current entitlement.

Model at least:
- owned/entitled
- installed/present
- available/retrievable
- version-compatible

Recovery UX should point to the correct failure dimension.

## 26. Make degraded loads read-only

If required dependencies are unresolved, do not allow normal autosave/overwrite. Otherwise a temporary missing-DLC/mod condition can permanently erase objects that would have returned after reinstall.

Prefer:

`PREFLIGHT → DEPENDENCY_CHECK → READY | DEGRADED_READONLY | BLOCKED_RECOVERABLE | UNSUPPORTED`

Only enter the normal save loop from a fully validated playable state.

## 27. Preserve unknown state when safe

When content is temporarily unavailable, preserve unresolved records as opaque/quarantined state where feasible instead of dropping them.

If the package later returns, attempt explicit rehydration and semantic validation. Unknown state must never execute as trusted gameplay logic merely because bytes were preserved.

## 28. Validate semantics after fallback/remap

Preventing a crash is not sufficient. Missing content can break:
- inventory/equipment invariants
- quest progression
- economy totals
- companion ownership
- map/world topology
- return portals/checkpoints

Run subsystem validation after every remap, placeholder or evacuation operation.

## 29. Archive released content manifests

Long-lived save compatibility depends on knowing which content catalog a historical save referenced.

Keep released manifest/catalog identities and representative save fixtures. Test historical save → historical manifest → supported upgrade path, not only old schema → current executable.

## 30. Test removal and restoration as a round trip

A game that merely boots after content removal may still destroy state.

CI should exercise:
- disable/remove dependency
- inspect degraded state without destructive save
- restore dependency
- reload/rehydrate
- compare stable semantic summaries against the original

The restoration half is essential.

## 31. Validate transitive dependencies

A directly referenced package can itself depend on another package/catalog/version.

Resolve dependency closure during preflight and report the root missing requirement where possible. In multiplayer/shared state, negotiate required content capabilities before entering authoritative simulation.

## 32. Define a compatibility horizon

Supporting every historical schema/content combination forever may be impossible. Make the boundary explicit:
- fully migrate
- read-only recovery/export
- requires stepping-stone build/content
- unsupported but preserved

Beyond the support horizon, failure must still avoid overwriting user data.

## 33. Model divergent saves as branches

When two devices modify state after a shared revision, preserve enough ancestry to identify a true fork rather than choosing by timestamp.

Prefer a three-way semantic comparison:

`base → branch A`

`base → branch B`

This distinguishes inherited old values from actual edits.

## 34. Assign merge semantics per persistent domain

A save blob contains values with different algebra. Declare the policy explicitly rather than applying one merge rule to everything.

Examples:
- discovered codex IDs: set union may be safe
- monotonic achievements: union may be safe
- best score: max may be safe if the scoring rule permits it
- currency / consumables: final balances alone are generally unsafe to merge
- mutually exclusive quest choices: branch conflict, not numeric max

Technical convergence is not proof of gameplay validity.

## 35. Give one-time rewards stable grant identity

If the same unique reward is earned independently on two branches, adding inventory counts duplicates it.

Persist stable grant/reward IDs where cross-device reconciliation matters. Merge grant identity first, then derive or validate inventory effects.

## 36. Treat deletion as persistent information

For mergeable objects, absence is ambiguous. A deleted object can otherwise reappear when reconciled with an unchanged ancestor copy.

Keep tombstones or equivalent operation provenance through the reconciliation horizon. Compact them only after relevant branches can no longer return.

## 37. Partition atomic units around invariants

Conflict granularity should reflect gameplay coupling, not file convenience.

Keep state that must change consistently in the same atomic/reconciliation unit. Separate truly independent slots or collections so unrelated changes do not create needless conflicts.

## 38. Separate race detection from semantic resolution

Write locks/version tokens detect that the base changed. They do not decide whether the new gameplay states can be joined.

On a conflict:
1. refetch current state
2. find ancestry if available
3. compute semantic deltas
4. apply domain-specific merge policies
5. validate the candidate globally
6. retry against the new concurrency token

Blind retry/overwrite is not conflict resolution.

## 39. Stage and validate merge candidates

Treat automatically merged state like an untrusted migration result.

Validate both local and cross-domain invariants before commit: inventory/equipment, economy, quests, world position/topology, unlock exclusivity, unique rewards, and content references.

Preserve both parent revisions until the merged candidate has become a later known-good generation.

## 40. Design progression for future mergeability

Offline/cloud reconciliation often requires information that a final snapshot does not contain: grant IDs, transaction provenance, explicit decisions, deletion history, authority and ancestry.

For every persistent domain, define before shipping:
- stable identity
- authority
- monotonic vs non-monotonic behavior
- legal merge operator (if any)
- exclusivity/invariants
- deletion policy
- provenance needed
- post-merge validator
- automatic vs assisted vs branch-choice-only resolution

## 41. Treat origin as part of persistence compatibility

Browser-local storage is scoped to origin. A deployment that changes scheme, host or port can make an otherwise valid save unreachable.

Separate persistence preflight into:
1. locate/acquire the save
2. parse/migrate/validate the save

A redirect to a new host does not migrate IndexedDB or `localStorage`.

## 42. Preserve an old-origin migration path

Before changing a public web-game origin, ship export/migration support on the old origin. Keep a minimal migration shell available for a defined compatibility horizon rather than replacing it immediately with a redirect-only endpoint.

Dormant players may skip every intermediate release; source retirement should therefore be based on migration/returner evidence, not only deployment age.

## 43. Prefer explicit portable handoff over ambient cross-origin access

Cross-site storage-access mechanisms are privacy/permission features and are not a general substitute for first-party save transfer.

Prefer one of:
- explicit validated export/import
- short-lived one-time server handoff
- authenticated cloud/account reconciliation

Migration should still work when third-party storage is blocked.

## 44. Give portable saves an identity/integrity envelope

A portable package should carry enough context to reject wrong-game, wrong-profile, stale or incompatible imports before they replace local progress.

Useful fields include:
- format/schema version
- game ID
- save UUID and revision
- profile/world identity
- source origin and timestamp
- content compatibility identity
- integrity/authenticity metadata appropriate to the trust model

Local browser state is persistence, not authority: server-authoritative economy, entitlements and ranked facts must be reconciled with their authority source.

## 45. Stage cross-origin imports transactionally

Use:

`ACQUIRE → VERIFY ENVELOPE → STAGE → IDENTITY CHECK → MIGRATE → SEMANTIC VALIDATE → AUTHORITY RECONCILE → COMMIT → ACK`

Do not delete source state or overwrite the destination's only known-good generation before destination commit succeeds.

If server-assisted transfer tokens are used, make them short-lived, one-time and narrowly scoped.

## 46. Add origin transitions to persistence CI

Do not test only old-save/new-build pairs on one localhost origin. Include real distinct-origin fixtures:
- old host → new host
- source available / unavailable
- browser tab / Home Screen PWA
- third-party storage blocked
- destination quota failure
- wrong profile/game import
- dormant returner skipping intermediate builds

The test must prove that the transfer mechanism recovered progress rather than accidentally sharing a test storage namespace.

## Playtest / QA checklist

- Can every shipped save fixture migrate to current?
- Can QA identify the exact failing migration step?
- Can malformed-but-parseable data reach gameplay?
- What survives interruption at each save transaction point?
- How far back is the recovery horizon?
- Can cloud conflicts silently discard desired progress?
- Can an old build damage a newer save?
- Can import overwrite local progress before validation?
- Is automatic recovery visible in diagnostic logs?
- Does SAVE COMPLETE wait for transaction completion?
- What happens when quota failure occurs before, during and after candidate staging?
- Can replay/cache growth starve the next critical save?
- Is enough reserve kept for migration's peak temporary footprint?
- Can an origin-wide local-data loss be distinguished from save corruption?
- Does persistence denial degrade safely?
- Can the player recover after deliberate local website-data deletion using export/cloud where supported?
- Does preflight distinguish unsupported schema from missing content?
- What happens when DLC is owned but not installed?
- Can optional, required and world-critical missing content follow different policies?
- Does a degraded load disable autosave and overwrite?
- Can removed content be restored without losing its previous state?
- Do renamed IDs use explicit remaps rather than heuristics?
- Are removed persistent IDs protected from accidental reuse?
- Are transitive package dependencies checked?
- Can QA reproduce a save against its historical content manifest?
- Does remove → restore round-trip recover the same important semantic state?
- Can the system identify a common ancestor for divergent offline branches?
- Is each persistent domain's merge operator documented and semantically justified?
- Can currency or consumables duplicate through branch merge?
- Does earning the same unique reward on both branches deduplicate by grant identity?
- Can an explicit deletion resurrect after sync?
- Can mutually exclusive quest facts coexist after an automatic merge?
- Does a write-lock conflict trigger semantic re-evaluation rather than blind overwrite?
- Is a merged candidate globally validated before commit?
- Are both parent branches recoverable after a bad merge?
- Is repeated reconciliation idempotent where declared mergeable?
- If the deployment origin changes, can the system distinguish inaccessible legacy storage from a genuinely new player?
- Has a real old-origin save been transferred without relying on redirect behavior?
- Can migration succeed with third-party storage blocked?
- Can a wrong-game/wrong-profile portable save be rejected before destructive write?
- Does a destination quota failure leave both source and destination known-good state recoverable?
- Can a one-time migration token be replayed after successful claim?
- Are server-authoritative economy/entitlement facts revalidated rather than trusted from portable local state?
- Have normal Safari and Home Screen PWA origin-migration paths both been exercised?
