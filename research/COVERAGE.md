# Research Coverage

自動・継続調査で同じ資料や同じ原則を繰り返さないための進捗表。

最終更新: 2026-09-24 / Batch 22

## Completed / substantially sampled

### Historical / magazine / preservation foundation
- Gaming Alexandria Magazine Archive / Magazine Sets
- Family Computer Magazine / Nintendo Fun Club News / GamePro / LOGiN / Beep / EGM / Super Play
- PC Engine Fan — complete run indexed; 1993/1994 touch-contrast sampling
- Famimaga 64 — 1996–1998 complete holdings indexed
- Play Meter / Monthly Coin Journal / Japan Amusement Monthly / Game Yuu II
- Micom BASIC / Program Pochette / Technopolis / Marukatsu / K-POWER / Game Hihyō

### Related developer / technical / design material
- Gamest / Computer Gaming World / Game Developer / GDC Vault
- Apple game/touch HIG and WWDC — Game Controls, virtual/physical controllers, adaptive touch layouts, haptics
- procedural-generation / city-road / PCG evaluation literature
- UGC moderation / returner matchmaking case studies
- arcade operator/service manuals and historical sales/settings material
- PlayFab Game Saves / save migration-recovery references
- GGPO / Source networking / deterministic and snapshot networking references
- Blizzard Overwatch replay/spectator and Unity authority/spectator material
- smartphone thumb-reach / grip-span ergonomics research

## Well-covered batches

- 01–06: foundational principles / arcade science / review culture / Japanese lineage / RPG-ADV / AI-coop
- 07: fighting / racing / shooter recovery / puzzle / economy / arcade onboarding
- 08: audio / horror / save / teaching / encounters / community / UGC
- 09: rhythm / camera / inventory / procedural generation / local shared play
- 10: strategy UI / local multiplayer / accessibility / rewards / crafting
- 11: sports abstraction / narrative choice / speedrun / strategy automation / automated validation
- 12: procedural city / replay-spectator / touch / UGC discovery / comeback
- 13: replay determinism-regression / iPhone safe-area-haptics / UGC version-remix / returner recalibration / procedural regression
- 14/14B: arcade operations / attract / photo mode / procedural and production operations
- 15: physical arcade controls / embodied input / platform differentiation
- 16: continue / redemption / kit economics / public-play conversion
- 17: calibration / maintenance diagnostics / linked network / payout invariants
- 18: save migration / corruption recovery / cloud conflict / fault injection
- 19: rollback / prediction / interpolation / mobile reconnect / desync
- 20: procedural decision signatures / heatmaps / semantic repetition
- 21: replay lifecycle / authority / spectator scale / privacy / analytics
- 22: adaptive touch ergonomics / handedness / reachability / occlusion / haptic density / long-session thermal fatigue / cross-input semantic equivalence

## Dedicated guides

Core specialist set includes:
- docs/touch-controller-ergonomics.md
- docs/adaptive-touch-ergonomics.md
- docs/touch-production-qa.md
- docs/physical-arcade-interface-design.md
- docs/input-calibration-and-diagnostics.md
- docs/rollback-mobile-network-design.md
- docs/replay-spectator-telemetry.md
- docs/replay-lifecycle-privacy.md
- docs/procedural-diversity-metrics.md
- docs/save-resilience-and-migration.md

See docs/ for the remaining genre/system guides from earlier batches.

## Next priorities — high

### Procedural automated QA — follow-up
- semantic visual descriptors beyond screenshot hashes
- multi-agent route/strategy diversity
- generated encounter pacing signatures
- automated landmark/readability metrics
- human-calibrated repetition thresholds

### Replay / telemetry — follow-up
- privacy threat-model details for user-generated replay sharing
- long-term format migration and archival corpus
- spectator anti-cheat / hidden-information delay
- automated highlight quality evaluation
- replay storage quotas / eviction stress tests

### Touch / physical interaction — follow-up
- empirical thresholds for layout adaptation / hysteresis
- controller-to-touch competitive fairness telemetry
- device-size matrix and thumb-occlusion automated overlays
- sustained-performance + thermal ergonomics automation
- motor-accessibility presets validated per genre

### Arcade / public-play follow-up
- linked cabinets / team-vs-team queue and dropout behavior
- public demo / convention conversion telemetry
- skill-based redemption transparency / payout volatility
- maintenance frequency / component degradation effects on play

### Save / resilience — follow-up
- semantic merge of independent progression branches
- content-DLC removal / missing-mod compatibility
- browser storage quota / partial-write behavior
- recovery UX/privacy and long-lived fixture corpus

### Networked action — follow-up
- rollback CPU/memory budgets on mobile Safari
- host/authority migration under dropout
- matchmaking network-quality thresholds
- cheating/security boundaries for client prediction
- protocol/version migration

## Next priorities — medium

- narrative consequence telemetry
- sports teammate/off-ball AI
- crafting economy
- accessibility across genres
- photo/replay sharing privacy and metadata
- live balance telemetry
- economy inflation monitoring

## Rule for future runs

1. 既存内容と重複しない
2. 実装・QA・プレイテストへ落とせる
3. source -> mechanism -> principleへ抽象化する
4. copyright-protected表現を保存しない
5. 自動バッチと手動バッチが競合したら差分のみ追加する
