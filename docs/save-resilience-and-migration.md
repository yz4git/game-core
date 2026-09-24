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
