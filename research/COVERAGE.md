# Research Coverage

自動・継続調査で同じ資料や同じ原則を繰り返さないための進捗表。

最終更新: 2026-09-24 / Batch 28

## Completed / substantially sampled

### Historical / magazine / preservation foundation
- Gaming Alexandria Magazine Archive / Magazine Sets
- Family Computer Magazine / Nintendo Fun Club News / GamePro / LOGiN / Beep / EGM / Super Play
- PC Engine Fan — complete run indexed; 1993/1994 touch-contrast sampling
- Gekkan PC Engine — complete 1988–1994 run indexed
- Famimaga 64 — 1996–1998 complete holdings indexed
- Play Meter / Monthly Coin Journal / Japan Amusement Monthly / Game Yuu II
- Micom BASIC / Program Pochette / Technopolis / Marukatsu / K-POWER / Game Hihyō
- Batch 23 historical sports context: Play Meter 1977/1988/1990, GamePro 1989, Technopolis 1987, Family Computer Magazine 1990, Canadian Coin Box 1990
- Batch 24 procedural/readability historical cross-sample: Micom BASIC 1984, Family Computer Magazine 1985/1990, Comptiq 1988/1990, Canadian Coin Box 1986
- Batch 25 replay/spectator historical cross-sample: Family Computer Magazine holdings, Famimaga 64 1996–1998, TV Gamer 1997, Monthly Coin Journal 1998, Gamejin 1999
- Batch 26 procedural QA cross-sample: Technopolis 1987/1994, PC Engine Fan 1994, Gekkan PC Engine 1988–1994, Famimaga 64 1996, Game Yuu II 1996, Monthly Coin Journal 1998
- Batch 27 constrained-hardware/network context cross-check: Family Computer Magazine, Technopolis, Famimaga 64, Play Meter / Monthly Coin Journal preservation sets
- Batch 28 save-media / persistence cross-sample: Beep 1985, Family Computer Magazine 1990, PC Engine Fan 1994 + complete-run index, Famimaga 64 1996–1998, Dengeki G's Engine 1996–1997, Used Games 1996–2000, Game Lab 1999, Play Meter / Monthly Coin Journal 1996–1998

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
- Riot Games League of Legends Replay API
- FDG / Honor of Kings / gameplay-video multi-modal highlight detection research
- player-reaction / outlying-behavior highlight research
- spectator state-delay and replay privacy implementation references
- AIIDE generic level evaluation / gameplay action-graph constraints / static+dynamic puzzle validation
- PCG solution-action-sequence similarity / affordance-rich tile embeddings
- space-time WFC and local-vs-global solvability research
- Quality Diversity / constrained MAP-Elites game-content research
- 2026 FPS MAP-Elites topology vs emergent gameplay evaluation
- Batch 27: WebKit JavaScriptCore lifecycle performance / JetStream 3, Apple Safari Web Inspector CPU/energy guidance, MDN Page Visibility / rAF / PerformanceObserver / Long Animation Frame / Device Memory capability material
- Batch 28: WebKit Storage Policy / Safari 17 Storage API, MDN storage quota+eviction / StorageManager estimate+persist / IndexedDB transaction complete+abort, W3C IndexedDB atomic commit requirements

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
- 25: automated highlight quality / hard-negative highlight QA / causal clip boundaries / highlight diversity / spectator hidden-information authorization / field-level replay privacy / collusion-delay testing
- 26: adversarial procedural seed search / near-failure margins / static-vs-dynamic gates / semantic-depth-affordance visual regression / behavior-space coverage stopping / failure minimization / human-machine QA loop
- 27: mobile Safari rollback CPU/memory budgets / state-history bounds / allocation-stable re-simulation / fixed simulation vs display refresh / background-resume discontinuity / sustained thermal-performance QA / presentation-first degradation
- 28: browser save quota / runtime storage estimates / IndexedDB transaction commit boundaries / origin eviction / persistence tiers / critical storage reserve / quota fault injection / recovery-aware startup

## Dedicated guides

Core specialist set includes:
- docs/touch-controller-ergonomics.md
- docs/adaptive-touch-ergonomics.md
- docs/touch-production-qa.md
- docs/physical-arcade-interface-design.md
- docs/input-calibration-and-diagnostics.md
- docs/rollback-mobile-network-design.md — expanded Batch 27 with browser/mobile performance budgets
- docs/replay-spectator-telemetry.md
- docs/replay-lifecycle-privacy.md
- docs/automated-highlight-spectator-safety.md
- docs/procedural-diversity-metrics.md — expanded through Batch 26 adversarial coverage
- docs/procedural-pacing-readability-qa.md
- docs/adversarial-procedural-qa.md
- docs/save-resilience-and-migration.md — expanded Batch 28 with browser quota/eviction resilience
- docs/sports-game-abstraction.md — expanded Batch 23 teammate/off-ball AI guidance

See docs/ for remaining genre/system guides.

## Next priorities — high

### Procedural automated QA — follow-up
- empirical calibration of behavior-space stopping thresholds on real generator histories
- genre-specific adversarial objectives for shooter/racing/RPG/puzzle
- 3D occlusion / skyline / road continuity semantic visual tests
- mutation operators that preserve validity while searching near failure boundaries
- production cost budgets: seeds/hour, agent CPU, render-buffer storage and CI sharding

### Replay / telemetry — follow-up
- long-term format migration and archival corpus
- replay storage quotas / eviction stress tests
- privacy-preserving highlight model evaluation across genres
- highlight-signature thresholds calibrated against human comprehension
- spectator collusion threat models per genre/mode

### Touch / physical interaction — follow-up
- empirical thresholds for layout adaptation / hysteresis
- controller-to-touch competitive fairness telemetry
- device-size matrix and thumb-occlusion automated overlays
- sustained-performance + thermal ergonomics automation
- motor-accessibility presets validated per genre

### Save / resilience — follow-up
- semantic merge of independent progression branches
- content-DLC removal / missing-mod compatibility
- recovery UX/privacy and long-lived fixture corpus
- storage reserve thresholds calibrated on real save/replay/cache growth
- cross-origin / deployment-origin migration and save portability

### Networked action — follow-up
- empirical rollback budget calibration across iPhone performance tiers
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
