# Research Coverage

自動・継続調査で同じ資料や同じ原則を繰り返さないための進捗表。

最終更新: 2026-09-24 / Batch 19

## Completed / substantially sampled

### Historical / magazine / preservation foundation
- Gaming Alexandria Magazine Archive / Magazine Sets
- Family Computer Magazine
- Nintendo Fun Club News
- GamePro
- LOGiN — 1983 / 1984 / 1985 preservation sampling plus prior design passes
- Beep
- Play Meter — archive overview plus operator-setting / attract / session-economics / physical-interface / maintenance passes
- Micom BASIC / Program Pochette
- Technopolis
- Marukatsu / Gekkan / PC Engine Fan — complete PC Engine Fan run indexed
- EGM
- Game Hihyō
- K-POWER
- Monthly Coin Journal / Canadian Coin Box — 1989 / 1995 / 1996 / 1998 arcade-operations sampling
- Japan Amusement Monthly — 1992 sampling
- Game Yuu II — 1995–1996 sampling

### Related developer / technical / design material
- Gamest / 三辻富貴朗系
- Computer Gaming World
- Game Developer archives
- GDC Vault
- Apple game/touch HIG and WWDC
- procedural-generation / city-road literature
- UGC platform moderation guidelines
- returning-player matchmaking case studies
- International Arcade Museum eLibrary / Play Meter public text pages
- arcade operator earnings / settings historical syntheses
- SEGA Arcade History / product archive
- HCI Museum physical arcade controller records
- arcade operator/service manuals — calibration, I/O tests, network linking, payout configuration
- PlayFab Game Saves — cross-device sync, conflict handling, offline progression
- save-schema migration / backup-recovery implementation references
- Nintendo save corruption support documentation

## Well-covered batches

- 01–06: foundational principles / arcade science / review culture / Japanese lineage / RPG-ADV / AI-coop
- 07: fighting / racing / shooter recovery / puzzle / economy / arcade onboarding
- 08: audio / horror / save / teaching / encounters / community / UGC
- 09: rhythm / camera / inventory / procedural generation / local shared play
- 10: strategy UI / local multiplayer / accessibility / rewards / crafting
- 11: sports abstraction / narrative choice / speedrun / strategy automation / automated validation
- 12: procedural city / replay-spectator / touch / UGC discovery / comeback
- 13: replay determinism-regression / iPhone safe-area-haptics / UGC version-remix / returner recalibration / procedural regression
- 14: arcade operator tuning / session economics / attract-mode teaching / spectator conversion / photo-mode expression / procedural structural diversity
- 14B: headless procedural CI / replay operations / touch production QA / UGC trust-safety / returner matchmaking operations
- 15: physical arcade controls / cabinet ergonomics / embodied input / spectator-readable intent / platform differentiation / local co-op social feedback
- 16: continue / buy-in / redemption incentives / kit economics / public-play conversion / linked-play social structure
- 17: physical-input calibration / maintenance diagnostics / linked-network lifecycle / payout invariants / operator audits / reset domains
- 18: save schema migration / transactional writes / corruption recovery / backup horizon / cloud conflict / save identity / destructive fault injection
- 19: rollback / input prediction / interpolation / lag compensation / jitter and burst loss / mobile reconnect / desync diagnostics

## Dedicated guides

- docs/opponent-ai-and-balance.md
- docs/layered-accessibility-and-depth.md
- docs/fighting-game-design.md
- docs/racing-game-design.md
- docs/shooter-recovery-and-encounters.md
- docs/puzzle-planning.md
- docs/arcade-session-and-attract.md
- docs/game-economy-and-interface.md
- docs/audio-as-gameplay.md
- docs/horror-tension-design.md
- docs/save-and-failure-design.md
- docs/save-resilience-and-migration.md
- docs/teaching-and-documentation.md
- docs/encounter-and-camera-design.md
- docs/community-ugc-metagame.md
- docs/rhythm-game-design.md
- docs/rhythm-game-timing.md
- docs/camera-and-targeting.md
- docs/procedural-generation-quality.md
- docs/inventory-ergonomics.md
- docs/strategy-ui-information.md
- docs/local-multiplayer-design.md
- docs/accessibility-options.md
- docs/rewards-and-retention.md
- docs/crafting-system-design.md
- docs/sports-game-abstraction.md
- docs/narrative-choice-design.md
- docs/speedrun-challenge-design.md
- docs/strategy-automation.md
- docs/procedural-city-road-generation.md
- docs/replay-spectator-telemetry.md
- docs/touch-controller-ergonomics.md
- docs/ugc-discovery-moderation.md
- docs/long-term-comeback-design.md
- docs/replay-determinism-regression.md
- docs/procedural-regression-testing.md
- docs/ugc-versioning-remix.md
- docs/returning-player-recalibration.md
- docs/arcade-operations-economics.md
- docs/photo-mode-player-expression.md
- docs/procedural-ci-operations.md
- docs/replay-validation-operations.md
- docs/touch-production-qa.md
- docs/ugc-trust-safety-ops.md
- docs/returner-matchmaking-operations.md
- docs/physical-arcade-interface-design.md
- docs/continue-redemption-public-play.md
- docs/input-calibration-and-diagnostics.md
- docs/linked-play-reliability.md
- docs/rollback-mobile-network-design.md

## Next priorities — high

### Procedural automated QA — production scale
- route heatmaps
- geometry invariant checks
- visual semantic diff
- structural-diversity / decision-signature metrics
- aesthetic repetition detection

### Replay / telemetry — production scale
- server-authoritative validation
- replay privacy / sharing metadata
- replay storage retention
- spectator analytics

### Touch / physical interaction
- handedness presets
- dynamic control positioning
- haptic fatigue
- heat / long-session grip
- accessibility + touch interaction
- semantic equivalence metrics across touch/controller/keyboard

### Arcade / public-play follow-up
- linked cabinets / team-vs-team queue and dropout behavior
- public demo / convention conversion telemetry in modern deployments
- skill-based redemption transparency and payout volatility
- maintenance frequency / component degradation effects on play

### Save / resilience — follow-up
- semantic merge of independent progression branches
- content-DLC removal / missing-mod compatibility
- storage quota / partial-write behavior in browsers
- recovery UX and privacy
- long-lived save fixture corpus

### Networked action — follow-up
- rollback CPU/memory budgets on mobile Safari
- host/authority migration under dropout
- matchmaking network-quality thresholds
- cheating/security boundaries for client prediction
- protocol/version migration for long-lived multiplayer

## Next priorities — medium

- narrative consequence telemetry
- sports teammate/off-ball AI
- crafting economy
- accessibility across genres
- procedural aesthetics / repetition metrics deeper pass
- photo/replay sharing privacy and metadata
- live balance telemetry
- economy inflation monitoring

## Rule for future runs

1. 既存内容と重複しない
2. 実装・QA・プレイテストへ落とせる
3. source -> mechanism -> principleへ抽象化する
4. copyright-protected表現を保存しない
5. 自動バッチと手動バッチが競合したら差分のみ追加する
