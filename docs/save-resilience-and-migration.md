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
