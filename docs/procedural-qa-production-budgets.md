# Procedural QA Production Budgets

Use this guide when automated procedural testing is large enough that agent CPU, GPU rendering, storage, CI duration, or human triage limits coverage.

## Goal

Optimize for **trustworthy new evidence per unit cost**, not raw seed count.

A useful QA campaign preserves three properties simultaneously:
- longitudinal comparability through fixed canonical tests;
- population evidence through unbiased random sampling;
- rare-failure discovery through adaptive/adversarial search.

Never let the third silently consume the first two.

## Cost-escalation funnel

Run the cheapest valid discriminator first:

**STATIC → CHEAP AGENT → FULL AGENT → MULTI-POLICY → SELECTIVE RENDER → HUMAN CONFIRMATION**

A candidate earns promotion through one or more of:
- new behavior cell/signature;
- small failure margin;
- high predicted severity;
- high uncertainty;
- policy disagreement;
- canonical/regression relevance;
- changed dependency requiring revalidation.

Do not render or run expensive policies uniformly when cheap semantic evidence already shows duplication.

## Budget units

For every candidate/stage record at least:
- CPU milliseconds;
- GPU milliseconds where relevant;
- simulated frames/ticks;
- solver/search expansions;
- peak memory;
- bytes retained/transferred;
- wall time;
- outcome/failure signature;
- behavior cell and margin vector.

Report seeds/hour only beside evidence-normalized measures such as:
- new behavior cells / CPU-hour;
- new severe signatures / CPU-hour;
- confirmed severe issues / human-review hour;
- new boundary cells / compute-hour.

## Fixed floors before adaptive allocation

Each release campaign should reserve:
1. **canonical floor** — deterministic regression fixtures;
2. **unbiased floor** — fresh random sample for population estimates;
3. **adaptive remainder** — frontier, disagreement, novelty, severe-failure and mutation search.

Percentages are project-specific. The invariant is that adaptive search cannot erase the canonical or unbiased floor.

## Stage-specific work caps

Protect CI from pathological cases with explicit limits on:
- solver expansions;
- simulated ticks;
- per-case CPU time;
- memory;
- render frames;
- trace size.

Cap exhaustion is not an ordinary discard. Classify it (`TIMEOUT`, `EXPANSION_CAP`, `FRAME_CAP`, `MEMORY_CAP`), retain partial evidence, and send a bounded sample to an extended-budget queue. Repeated cap exhaustion is itself a regression signal.

## Cost-aware sharding

Do not shard only by numeric seed range when case cost is heavy-tailed.

Maintain a cheap predicted-cost model using static descriptors and recent telemetry. Bin-pack work so predicted CPU/GPU cost is balanced across shards, then use work stealing or a residual queue for estimation error.

Track:

`shard_imbalance = max(shard_wall_time) / median(shard_wall_time)`

A high value means available machines are idle while one pathological shard determines feedback time.

## Semantic caching

Cache expensive stages by dependency fingerprint rather than seed alone.

Possible dependency keys:
- generator version;
- ruleset/content epoch;
- collision/navigation build;
- agent/policy version;
- descriptor/margin schema;
- renderer/camera/lighting version for visual artifacts.

A renderer-only change should not automatically invalidate deterministic solver evidence. A collision or ruleset change usually should.

## Discovery vs confirmation

Cheap agents and proxies should search broadly. Expensive/high-fidelity agents and human play should confirm:
- top-severity candidates;
- high uncertainty;
- policy disagreement;
- newly discovered failure signatures;
- near-boundary cases;
- representative samples used for calibration.

Do not confuse search efficiency with truth. A cheap metric is valuable when it ranks what deserves confirmation.

## Adaptive allocation by marginal evidence

In rolling windows calculate:
- new behavior cells / cost;
- new severe signatures / cost;
- disagreement cases / cost;
- uncertainty reduction / cost;
- human-confirmed precision of promoted cases.

After the fixed floors are satisfied, shift incremental budget toward cohorts/operators with higher expected information gain. Require repeated windows before reallocating strongly so noise does not make the scheduler thrash.

## Artifact retention hierarchy

Always retain reproduction-critical metadata:
- seed/parent;
- build and semantic fingerprints;
- mutation/repair delta where applicable;
- descriptors/margins;
- outcome and failure signature;
- cost telemetry.

Retain expensive traces, screenshots, video, depth/semantic buffers and checkpoints selectively for:
- canonical fixtures;
- failures and novel signatures;
- frontier/boundary cases;
- policy/human disagreement;
- a small unbiased audit sample.

Expire redundant passing media before reproduction-critical metadata.

## Selective visual QA

Use semantic signals to decide what deserves full rendering:
- changed collision/affordance signature;
- landmark/visibility risk;
- mechanical novelty;
- worst-N margins;
- changed renderer dependencies;
- representative behavior cells.

Keep a small random visual sample to detect blind spots in the semantic selector.

## Cost regressions

Compare cost distributions across builds, not only correctness:
- p50/p95/p99 CPU time;
- p50/p95/p99 solver expansions;
- simulated frames;
- GPU/render time;
- peak memory;
- artifact bytes;
- timeout/cap rate.

Break these down by behavior cell and failure class. A generator that still passes but doubles validation cost reduces future test breadth and may indicate pathological runtime complexity.

## CI ladder

### Pull request smoke
Canonical subset + cheap static predicates. Fast and deterministic.

### Pull request targeted
Dependency-aware impacted cells, known failure families, and cached-stage reuse.

### Mainline
Full canonical suite + minimum unbiased random cohort + bounded adversarial budget.

### Nightly
Broader boundary search, multi-policy confirmation, selective semantic rendering.

### Deep campaign
Extended-budget timeouts, human calibration, large device/thermal/storage matrices, and expensive long-tail searches.

When a deep campaign finds a bug, shrink it into the cheapest stable canonical fixture possible so future detection moves to an earlier tier.

## Stopping rule

Do not stop because a round number of seeds was reached. Stop adaptive expansion when all are true:
- canonical required fixtures pass;
- unbiased sample floor is complete;
- rolling new behavior-cell gain is below a calibrated threshold for repeated windows;
- rolling severe-failure discovery is similarly saturated;
- disagreement/uncertainty discovery is saturated enough for the release risk;
- no unresolved high-severity cluster remains;
- residual untested risk and exhausted budgets are reported.

The threshold must be calibrated from real generator history; it is not a universal constant.

## Scheduler heuristic

A scheduler may rank optional promotion with an estimate like:

`expected_information_gain × consequence × uncertainty / expected_cost`

Do not use this scalar to override hard safety/gameplay requirements. Canonical regressions, sacred playability invariants, security/economy boundaries, and known severe signatures receive mandatory validation.

## Dashboard

Track at minimum:
- canonical/random/adversarial compute share;
- CPU/GPU hours by stage and cohort;
- new behavior cells / CPU-hour;
- new severe signatures / CPU-hour;
- human-confirmed precision;
- timeout/cap rate;
- p95/p99 case cost;
- cache hit rate by semantic stage;
- shard imbalance;
- retained bytes per actionable case;
- estimated full-canonical reproduction cost;
- residual risk at budget exhaustion.

## Playtest / production questions

- Which stage currently consumes the most cost without changing decisions?
- Which cheap predicate can reject or deduplicate work before full simulation?
- Are pathological timeouts preserved as evidence rather than disappearing?
- Did adaptive search starve unbiased sampling?
- Which cohort/operator produces the most actionable evidence per compute-hour?
- Is one shard dominating feedback latency?
- Are semantic cache invalidation keys too broad or dangerously narrow?
- Are rich artifacts retained because they aid reproduction, or merely because they are easy to collect?
- Did a generator change make validation materially more expensive despite the same pass rate?
- What residual risk remains when the declared budget is exhausted?
