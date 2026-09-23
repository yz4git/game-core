# Replay Lifecycle, Authority & Privacy

Replay is not only a playback feature. It is a lifecycle spanning recording, validation, learning, spectating, sharing, retention and eventual incompatibility.

## 1. Declare replay purpose

A replay may serve:
- immediate self-review
- competitive evidence
- QA reproduction
- spectator entertainment
- coaching
- long-term archival

Do not assume one retention/privacy policy fits every purpose.

## 2. Version and retention policy

Store at minimum:
- replay format version
- game build
- protocol version
- content/map version
- mode/ruleset
- match/run ID
- creation time
- retention class / expiry

Possible policies:
- same-patch interactive playback
- migration-supported playback
- metadata-only archive
- rendered-video fallback

A bounded recent list is reasonable when users can explicitly pin/save important runs.

## 3. Authority

Competitive validation should use authoritative state or data verifiable against it. Client presentation may contain prediction and reconciliation artifacts and should not silently become the official truth.

## 4. Spectator trust role

Spectators should be least-authority clients:
- read-only session capability
- no gameplay command authority
- separate spectator identity/token where applicable
- no hidden/private state unless explicitly required by the role

## 5. Fan-out architecture

Large spectator counts should not linearly load the latency-critical match server. When scale requires it:

`authoritative simulation → replay/snapshot stream → spectator replicator/distribution → viewers`

Measure whether spectator count changes player simulation/network quality.

## 6. Analysis controls

High-value replay controls:
- pause / step
- speed change
- event jump
- first-person / follow / free / tactical cameras
- player/entity switching
- bookmarks
- useful overlays

Optimize time-to-answer, not feature count.

## 7. Explanatory overlays

Replay overlays should reveal relationships hidden during live play, for example:
- route divergence
- objective pressure
- aggro/target choice
- resource state
- line of sight
- split delta
- team rotation

Avoid simply duplicating the normal HUD.

## 8. Privacy boundary

Raw replay data may contain information not visible during playback. Before export/share, minimize:
- account/internal IDs
- session/auth identifiers
- private team/debug state
- unnecessary chat/social metadata
- precise device/network identifiers

Prefer public replay identities and purpose-specific export. A rendered clip may be safer than a raw interactive artifact for casual sharing.

## 9. Long-term preservation

Interactive replay depends on old simulation semantics. Important records may need:
- validated result metadata
- integrity hash
- key statistics
- rendered video/highlight
- event summary

so evidence remains after interactive playback expires.

## 10. Spectator analytics

Useful aggregate measures include:
- camera switches
- rewind/event-jump points
- tactical-overlay use
- viewer exits
- watch duration
- repeated focus on specific encounters

Use them to distinguish compelling moments from confusing ones. Avoid collecting identity when aggregate behavior is sufficient.

## QA checklist

- What happens to a replay after a patch?
- Can a pinned replay survive automatic eviction?
- Does replay reconstruction agree with authoritative result?
- Can spectator clients mutate match state?
- Does spectator load degrade players?
- Can shared replay files expose hidden/private identifiers?
- Can users reach a decisive moment quickly?
- Are incompatible rulesets clearly labeled?
- What remains when interactive replay support ends?
