# Research Coverage

自動・継続調査で同じ資料や同じ原則を繰り返さないための進捗表。

最終更新: 2026-09-24 / Batch 24

## Completed / substantially sampled

### Historical / magazine / preservation foundation
- Gaming Alexandria Magazine Archive / Magazine Sets
- Family Computer Magazine / Nintendo Fun Club News / GamePro / LOGiN / Beep / EGM / Super Play
- PC Engine Fan — complete run indexed; 1993/1994 touch-contrast sampling
- Famimaga 64 — 1996–1998 complete holdings indexed
- Play Meter / Monthly Coin Journal / Japan Amusement Monthly / Game Yuu II
- Micom BASIC / Program Pochette / Technopolis / Marukatsu / K-POWER / Game Hihyō
- Batch 23 historical sports context: Play Meter 1977/1988/1990, GamePro 1989, Technopolis 1987, Family Computer Magazine 1990, Canadian Coin Box 1990
- Batch 24 procedural/readability historical cross-sample: Micom BASIC 1984, Family Computer Magazine 1985/1990, Comptiq 1988/1990, Canadian Coin Box 1986

### Related developer / technical / design material
- Gamest / Computer Gaming World / Game Developer / GDC Vault
- Apple game/touch HIG and WWDC
- procedural-generation / city-road / PCG evaluation literature
- UGC moderation / returner matchmaking case studies
- arcade operator/service manuals and historical sales/settings material
- PlayFab Game Saves / save migration-recovery references
- GGPO / Source networking / deterministic and snapshot networking references
- Blizzard Overwatch replay/spectator and Unity authority/spectator material
- smartphone thumb-reach / grip-span ergonomics research
- FIFA 13/17/22 and EA SPORTS FC 25 tactical/off-ball AI developer material
- TacticAI football tactical graph-model research
- AIIDE PCG evaluation / expressive-range / survival-analysis references
- multi-agent PCGRL and multi-agent behavioural-diversity research
- Neon Chrome procedural-generation public breakdown

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
- 22: adaptive touch ergonomics / handedness / reachability / occlusion / haptic density / thermal fatigue / cross-input equivalence
- 23: sports teammate/off-ball AI / hierarchical team intent / role contracts / spatial relations / intent hysteresis / counterfactual AI QA
- 24: procedural pacing signatures / multi-skill difficulty curves / route-weighted threat / recovery budget / landmark-junction readability / clustered strategy heatmaps / counterfactual strategy diversity / human metric calibration

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
- docs/procedural-diversity-metrics.md — expanded Batch 24 pacing/readability/strategy metrics
- docs/procedural-pacing-readability-qa.md
- docs/save-resilience-and-migration.md
- docs/sports-game-abstraction.md — expanded Batch 23 teammate/off-ball AI guidance

See docs/ for remaining genre/system guides.

## Next priorities — high

### Procedural automated QA — follow-up
- empirical landmark/readability threshold calibration with human route-choice data
- multi-agent adversarial seed search for rare exploits
- encounter pacing signatures for shooter/racing/RPG-specific semantics
- visual-semantic descriptors using geometry/depth/segmentation rather than screenshot hashes
- generator coverage stopping criteria: when fresh cohorts stop finding new behavior clusters

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
- sports AI follow-up: multi-agent assignment conflict / role-transition hysteresis / teammate option-quality benchmark corpus
- crafting economy
- accessibility across genres
- photo/replay sharing privacy and metadata
- live balance telemetry
- economy inflation monitoring
- arcade linked-team queue/dropout and skill-redemption transparency

## Rule for future runs
1. 既存内容と重複しない
2. 実装・QA・プレイテストへ落とせる
3. source -> mechanism -> principleへ抽象化する
4. copyright-protected表現を保存しない
5. 自動バッチと手動バッチが競合したら差分のみ追加する
