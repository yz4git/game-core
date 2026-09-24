# Adversarial Procedural QA

## Purpose

Procedural QA must answer more than “did many seeds run?” A production generator needs evidence that common behavior is covered, rare severe failures are actively hunted, and visually novel output is mechanically meaningful.

## Three cohorts

Always keep three distinct seed cohorts:

1. **Canonical** — fixed regression seeds retained across versions.
2. **Random** — fresh unbiased samples that estimate ordinary population behavior.
3. **Adversarial** — seeds/parameters deliberately searched near failure boundaries, sparse behavior cells and exploit-rich regions.

Do not report them as one combined pass rate.

## Cheap gates before expensive simulation

Run structural checks first:
- connectivity / reachability
- collision and clearance
- legal spawn/goal placement
- slope/jump margins
- key-lock/progression ordering
- resource lower bounds
- finite coordinates / geometry sanity

Then run dynamic simulation for survivors. Timing, enemies, moving hazards and resource consumption can invalidate structurally legal content.

## Search near the boundary

Preserve not only failures but **near-failures**. Record margins such as:
- minimum jump tolerance
- minimum clearance
- minimum resource slack
- maximum unavoidable damage
- longest recovery delay
- route redundancy
- timing-window slack

Mutate seeds around the smallest margins. Borderline-valid content is often more useful than obviously corrupt content because it exposes fragile assumptions.

## Adversarial objectives

Reward player-relevant evidence, not visual strangeness:
- unreachable or barely reachable goals
- exploit reward/minute
- unavoidable damage
- extreme route cost
- navigation ambiguity
- resource starvation
- long pressure without recovery
- one-policy-only solvability
- semantic repetition despite cosmetic diversity

Use multiple objectives rather than collapsing all risk to one scalar when possible.

## Behavior-space coverage

Count discovered behavior cells/clusters, not merely seeds.

Useful dimensions include:
- route/branch entropy
- mechanic usage
- resource slack
- pressure/recovery signature
- solution trace
- strategy outcome vector
- traversal risk
- landmark/junction readability

A million seeds in ten cells is not broad coverage.

## Coverage stopping criterion

For rolling windows, track:
- new behavior cells per N seeds
- new severe failures per N seeds
- new agent-disagreement cases per N seeds

Require saturation across repeated windows for both random and adversarial cohorts before declaring a test budget sufficient. Keep severe-failure thresholds stricter than novelty thresholds.

Re-open the search whenever generator logic, gameplay rules or descriptors change materially.

## Semantic visual regression

Canonical screenshots are useful but insufficient. Export deterministic buffers where feasible:
- RGB
- depth
- collision / walkability
- semantic class
- gameplay affordance
- object/landmark ID

Weight differences by gameplay role. Objective, road, hazard, cover, enemy silhouette and landmark changes should matter more than foliage or particles.

Depth catches structural movement hidden by similar colors. Semantic/affordance buffers catch mechanically identical worlds disguised by cosmetic variation.

## Policy disagreement

Run several policies or skill models against the same seed. Flag large disagreement in:
- completion
- route
- damage
- resource use
- time
- exploit yield

“One agent can solve it” is weaker evidence than robust solvability across appropriate policies.

## Failure shrinking

When possible, minimize a failing generated case while preserving its failure predicate. Remove rooms, objects, decorators or parameter deviations and re-test.

Store:
- original seed
- minimized reproduction
- generator/build version
- failure predicate
- agent/input trace
- semantic/depth snapshots
- behavior descriptors

## Human calibration loop

Automated search and human playtests should exchange information:

**search → worst/novel/disagreement seeds → human classification → new predicate/descriptor → search again**

A recurring human complaint should become a machine-checkable detector when feasible.

## Release dashboard

Track at minimum:
- canonical regressions
- random/adversarial seeds tested
- hard-invalid rate
- dynamic-failure rate
- new behavior cells / 1k seeds
- new severe failures / 1k seeds
- behavior occupancy distribution
- agent disagreement rate
- solution-trace duplicate ratio
- semantic/depth regression magnitude
- minimized repro size

## Batch 39 — Validity-preserving mutation

Adversarial search should stay near the **valid-content manifold** instead of spending most of its budget producing trivial corruption.

### Semantic mutation vocabulary

Prefer mutations that preserve domain meaning:
- move a junction rather than randomize road vertices
- move an objective to another reachable branch rather than randomize coordinates
- redistribute encounter budget rather than add arbitrary enemies
- move a resource later in a valid progression rather than delete it
- alter landmark reveal timing rather than randomize every building

If a mutation cannot be described in gameplay language, check whether it is testing a useful production risk.

### Invariant classes

Before mutation, classify constraints:

- **Sacred** — must never break during this experiment.
- **Repairable** — may be restored by a bounded local repair.
- **Measured** — the target margin; allowed to approach zero or fail.

A repair must be logged. Large repair distance means the child is no longer a useful local experiment and should normally be rejected.

### Margin-vector search

Do not reduce playability to one boolean. Export signed margins such as:
- clearance
- reaction-time slack
- resource slack
- move-count surplus
- alternate-route cost
- visibility-before-decision
- unavoidable damage
- recovery distance

Search toward zero while remaining valid. Keep Pareto/frontier cases so one failure dimension does not erase another.

### Compound boundaries

After mapping individual margins, search intersections: narrow clearance + late cue; low ammo + long pressure; weak route redundancy + moving occlusion. Many production failures emerge from combinations of individually acceptable conditions.

Track boundary-pair and boundary-triple coverage separately from single-margin extremes.

### Adaptive mutation strength

Per operator, adapt step size from:
- valid-offspring rate
- behavior novelty
- margin improvement
- repair distance

Increase step size when children remain valid but behavior is stagnant. Decrease it when validity collapses or when refining a discovered boundary.

### Archive parents by information gain

Do not keep only the single worst seed. Preserve parents representing:
- distinct behavior cells
- distinct failure signatures
- different margin-frontier regions
- policy/human disagreement clusters

This prevents search from collapsing into one bug basin.

### Ancestry and semantic shrinking

For every retained adversarial case store:
- parent fixture/seed
- mutation operator and parameters
- semantic delta
- repair delta
- generator/build version
- margin vector
- behavior/failure signature

Shrink failures using the same semantic vocabulary as mutation. Minimize semantic delta before raw object count, while preserving sacred invariants and the failure predicate.

### Operator telemetry

Per release and per mutation operator track:
- attempts
- valid-before-repair rate
- valid-after-repair rate
- median/p95 repair distance
- new behavior cells / 1k attempts
- new boundary cells / 1k attempts
- new severe failure signatures / 1k simulations
- duplicate failure ratio
- human-confirmed issue precision
- simulation/render cost

Large changes in these yields after a generator revision are themselves regression signals.

### Recommended pipeline

**KNOWN-GOOD PARENT → SEMANTIC MUTATION → SACRED-INVARIANT CHECK → BOUNDED REPAIR → STATIC VALIDATION → MARGIN VECTOR → DYNAMIC SIMULATION → BEHAVIOR/FAILURE SIGNATURE → ARCHIVE/DISCARD → SEMANTIC SHRINK → REGRESSION FIXTURE**

## Playtest questions

- Are rare severe failures being searched for deliberately?
- Which valid seeds have the smallest safety margins?
- Which seeds pass static checks but fail dynamically?
- Do local-valid structures fail global progression?
- Are visually different seeds affordance-identical?
- Did a generator update lose behavior clusters?
- Has fresh discovery actually saturated?
- Are current descriptors hiding human-perceived differences?
- Can each severe procedural bug be reproduced compactly?
- Did human review improve the next automated search?
- Which mutation operators mostly create trivial invalidity?
- Which valid cases lie near two or more failure boundaries at once?
- Did repair preserve the intended mutation or silently replace it?
- Can a retained failure be explained as a short semantic delta from a known-good parent?
- Did a generator revision make an important mutation operator lose reach?