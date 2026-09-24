# Network-quality Matchmaking

## Goal

Matchmaking should not merely find available players. It should form a session whose network conditions can support the mode's actual simulation, fairness and stakes without making queue time unnecessarily long.

## 1. Separate gates from preferences

Use four classes:

- `INVARIANT` — build/protocol/content/trust compatibility; never relaxed by waiting
- `FLOOR` — minimum playable network envelope for this mode
- `RELAXABLE` — constraints that may widen over queue time
- `PREFERENCE` — candidate ranking only

A good skill match must never compensate for a connection outside the simulation's playable floor.

## 2. Match on a common feasible region

For server/relay play, evaluate the intersection of regions acceptable to every required participant. Do not simply average each player's best ping.

Useful group metrics:
- common viable region count
- worst-member RTT to selected region
- party RTT spread
- worst-member loss/jitter band
- confidence/age of QoS measurements

## 3. Network quality is a vector

Do not tune from median ping alone. Where available, retain:
- RTT p50/p95
- jitter p95
- packet loss
- burst-loss length
- route stability / repeated-probe variance
- effective update cadence

Then validate which dimensions predict real corrections, disconnects and player abandonment for the game.

## 4. Time-based expansion is a quality-loss curve

Do not jump from `strict` to `anything` after one timeout.

Example conceptual sequence:
1. best common region + tight skill
2. same network floor + wider skill
3. wider secondary preferences
4. alternate still-playable regions
5. explicit user choice to continue widening or keep strict search

Never relax correctness, protocol or security invariants.

## 5. Expansion order is genre-specific

### Rollback fighting
Protect timing/correction quality strongly. Widen skill before accepting network conditions that create excessive correction or delay.

### Racing
Protect route stability and common-region viability. Rating spread can often widen before unstable network paths.

### Co-op action
Party continuity and state correctness may matter more than tight skill equality.

### Turn-based / asynchronous
Latency constraints can be much looser; reconnect, protocol compatibility and durable-state correctness dominate.

### Ranked / tournament
Use stricter network and trust floors than casual/custom modes because irreversible outcomes have higher stakes.

## 6. Every partition is a population tax

Separate queues/pools for platform, input method, region, mode, rank or ruleset improve specificity but reduce candidate density.

Before adding a partition, estimate:
- concurrent compatible population
- eligible candidates per minute
- p50/p95 wait
- fallback route
- measurable quality gain from the partition

Remove or merge partitions that create large wait cost without corresponding match-quality benefit.

## 7. QoS measurements expire

Runtime QoS is a prediction of the upcoming route. Store measurement age and confidence. If measurements become stale, remeasure or lower confidence instead of silently treating them as current truth.

## 8. Close the telemetry loop

Join pre-match and in-match data:

`TICKET → QOS → EXPANSION STAGE → SELECTED REGION → SESSION → ACTUAL NETWORK → GAMEPLAY OUTCOME`

Minimum useful correlation fields:
- matchmaking ticket/session ID
- queue and expansion stage
- selected region
- pre-match QoS vector
- in-match RTT/jitter/loss
- rollback/correction statistics
- disconnect/reconnect
- first-120-second quit
- rematch/continue
- skill outcome / surrender where relevant

A configured rule passing is not proof that the resulting match was good.

## 9. Calibrate thresholds as classifiers

For every candidate network floor calculate:
- false accept: admitted match later proves unplayable/unfair
- false reject: rejected candidate would likely have played acceptably
- added p50/p95 queue time
- quality improvement among admitted matches

Prefer empirically calibrated boundaries over universal folklore numbers.

## 10. Party policy

Do not let averages hide a bad edge. For hard playability, consider worst-member constraints. If one member destroys the common feasible region set, surface that as a party-level condition rather than silently degrading everyone.

## 11. Player communication

Communicate the trade-off without exposing abuse-sensitive internals:
- `Searching best connection`
- `Expanding skill range`
- `Searching wider regions`
- `Strict connection preference`

When practical, allow players to choose whether longer waiting is preferable to wider quality bounds.

## 12. Production test matrix

Test with synthetic populations and real telemetry across:
- dense vs sparse regions
- solo vs parties
- narrow vs wide skill distributions
- stable high RTT vs low RTT + jitter
- isolated vs burst loss
- fresh vs stale QoS
- peak vs off-peak population
- strict ranked vs casual policies
- cross-platform/input partitions
- expansion boundaries immediately before/after each stage

## Review checklist

- Are network floors distinct from weighted preferences?
- Is there at least one common feasible region for every formed group?
- Are hard rules truly non-relaxable?
- Does queue expansion degrade the least harmful dimension first?
- Are party gates based on worst relevant member rather than only average?
- Is QoS measurement age recorded?
- Can each queue partition justify its population cost?
- Are pre-match predictions compared with actual match telemetry?
- Are thresholds evaluated for both false accepts and false rejects?
- Do ranked/high-stakes modes use an appropriate stricter envelope?
- Can players understand when search quality is being widened?
- Are wait p95 and match-quality metrics reviewed together rather than separately?
