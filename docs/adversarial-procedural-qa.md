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
