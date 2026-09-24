# Procedural Diversity Metrics

## Goal

A generator is not diverse merely because screenshots differ. Production QA should answer four separate questions:

1. **Validity** — can this seed function?
2. **Decision diversity** — does it ask the player to do something meaningfully different?
3. **Perceptual diversity** — will players remember it as different?
4. **Experience-shape diversity** — does challenge, recovery and navigation unfold differently over time?

## Quality gates before novelty

Hard-fail seeds that violate reachability, collision, slope, spawn, resource or other gameplay invariants. Optimize novelty only among valid candidates. Broken content is not useful diversity.

Separate cheap static validity from dynamic playability. A level can pass topology and collision checks yet fail once moving hazards, enemy interactions, timing and resource consumption are simulated.

## Decision signatures

For deterministic test agents, normalize traces into compact signatures such as:

- route/branch sequence
- turn pattern
- jump/attack/boost events
- hazard exposures
- resource pickups/uses
- encounter order
- backtracking distance
- safe/unsafe time ratio

Compare signatures across seeds. High screenshot diversity with low signature diversity indicates cosmetic variation rather than mechanical variety. Solution/action traces are especially useful across presentation changes because they encode interaction demand rather than art.

## Route heatmaps

Aggregate normalized agent occupancy over many seeds. Use them to reveal repeated practical corridors, nominal branches that are almost never useful, over-dominant spawn/goal relationships, repeated choke points and unused generated space.

Do not stop at one aggregate heatmap. Cluster decision signatures first and render occupancy/transition maps per strategy cluster; otherwise multiple viable strategies can collapse into one fuzzy average.

## Expressive-range dashboard

Choose descriptors tied to player decisions, for example:

- route alternatives
- traversal length
- branch entropy
- hazard density
- resource slack
- planning search cost
- execution tolerance
- encounter transition entropy
- pressure/recovery streak length

Track coverage, density, clusters and outliers rather than only averages or extrema. Coverage means occupied behavior regions, not raw seed count.

## Difficulty decomposition

Do not collapse difficulty to one scalar when possible. Separate solution/search burden, precision/timing burden, input density, resource pressure and recovery margin.

Run more than one player model. A seed's effective difficulty is conditional on policy/skill, so compare novice-like, baseline, expert-like and exploit-seeking/safety policies when feasible. Large agent disagreement is itself a review signal.

## Pacing signatures

Treat generated difficulty as a sequence rather than an average. Record:

- encounter-type sequence / n-grams
- threat curve
- resource/recovery curve
- peak count and peak spacing
- longest consecutive-pressure run
- time/distance from a peak to meaningful recovery
- dead/low-demand streaks

Weight spatial threat by traversal probability to estimate experienced pressure rather than merely generated pressure.

## Landmark and junction readability

A useful landmark is **visible × distinctive × stable × decision-relevant**. At important junctions evaluate visible landmark IDs, approach-view silhouette/features, angular separation and branch identity.

Also compare branch heading, width, elevation, lighting/biome class and destination role. Flag forks where alternatives are perceptually too similar before the player commits.

For 3D generators, measure visibility along actual gameplay trajectories. Store first-visible distance, route-visible fraction, longest occluded interval, last visible distance before a consequential junction, and visibility transition rate. Rendering-correct occlusion is not equivalent to gameplay-readable occlusion.

Treat rapid visible/hidden transitions as **occlusion chatter**. Critical cues need enough continuous exposure to be identified, not merely a high count of visible frames.

## 3D road continuity

Validate generated roads at four layers: topology, geometry, traversal dynamics and semantics. A visually continuous surface can still have disconnected nav edges, collision seams, illegal lane direction or an undrivable curvature/grade jump.

Track connected components, articulation points, graph bridges/cut-edges, alternate-route ratio, lane endpoint mismatch, curvature/grade/width discontinuities and deterministic baseline-driver completion. Connectivity is stronger when useful alternate routes survive a blocked edge.

## Skyline signatures

For canonical gameplay viewpoints, sample horizon elevation by azimuth and retain dominant peak/landmark IDs, height-band occupancy and peak spacing. Compare these structural signatures across seeds/districts rather than relying on RGB difference. Cosmetic facade/weather changes should not hide repeated large-scale massing.

## Strategy diversity

Trace distance alone can reward meaningless variation. Where multiple agents/policies are available, compare their outcome vectors across the same seed/opponent/context matrix. Useful strategies should have different response strengths and weaknesses, not merely different paths.

## Visual-semantic repetition

Use deterministic canonical cameras and presentation settings. Cheap perceptual hashes can identify near-duplicates, but do not stop at RGB.

Where feasible export:
- normalized depth
- collision / walkability
- semantic class
- gameplay affordance
- landmark/object identity
- road/lane/drivable mask for generated driving worlds
- major occluder identity for critical-cue diagnostics

Compare objective, road/room topology, hazard/cover layout, landmark placement/silhouette, enemy-space and large-scale spatial rhythm. Weight gameplay-relevant classes more heavily than decorative foliage/particles.

Cosmetic noise should not trick the test into calling two structurally identical worlds diverse, and similar colors should not hide major geometry movement.

## Adversarial seed and camera search

After baseline random sampling, deliberately search sparse behavior cells and failure boundaries. Useful objectives include:

- minimum resource slack
- maximum unavoidable damage
- extreme path/search cost
- exploit reward per minute
- navigation ambiguity
- longest recovery delay
- low route redundancy
- high policy disagreement

For 3D worlds, also search route/camera parameter space for minimum landmark visibility, maximum pre-junction ambiguity, road-mask seam discontinuity, semantic/depth disagreement and occlusion chatter. Rare alignment failures often occupy too little viewpoint space for random screenshots to find efficiently.

Preserve and mutate near-failures, not only hard failures. Borderline valid seeds and camera positions reveal fragile margins that simple invariant rejection can hide.

## Coverage stopping criteria

Procedural spaces are usually not exhaustible. Track rolling discovery separately for random and adversarial cohorts:

- new behavior cells / N seeds
- new severe failures / N seeds
- new high-disagreement cases / N seeds

A test budget is approaching saturation only when these rates remain below explicit thresholds for repeated windows. Re-open coverage whenever generator logic, gameplay rules or descriptor definitions change materially.

Raw seed count is not evidence of coverage if new seeds only add density to known behavior clusters.

## Failure minimization

For severe procedural failures, shrink the generated case where representation permits: remove rooms, enemies, decorators or parameter deviations while re-running the failure predicate.

Store both original and minimized reproductions with generator/build version, agent trace, descriptors and relevant semantic/depth artifacts. Compact repros make generator bugs substantially more actionable.

## Regression strategy

Run fixed canonical seeds, large fresh random cohorts and adversarial cohorts. Compare descriptor and pacing-signature distributions between generator versions. Preserve worst-N and near-boundary seeds permanently.

A generator update can keep mean difficulty unchanged while silently making runs flatter, spikier, more exhausting, or collapsing previously viable strategy clusters. Compare cluster occupancy and tails, not only means.

For 3D worlds, canonical fixtures must include shipped camera semantics (height, pitch, FOV, aspect and follow offset). Free-editor-camera screenshots are not equivalent regression evidence.

## Human calibration

Automated metrics filter and diagnose; they do not replace playtests. Periodically compare metric predictions with blind human judgments of repetition, difficulty, pacing, fatigue, readability and memorability.

Version metric definitions and thresholds. Retire or reweight metrics that do not predict the intended experience. If humans repeatedly distinguish seeds inside one automated behavior cell, revise the descriptor space.

Use a feedback loop: **automated search → worst/novel/disagreement seeds → human classification → new predicate/descriptor → search again**.

## Recommended pipeline

Canonical regression → random cohort → static invariant gates → road/topology seam gates when applicable → dynamic multi-policy simulation → decision/strategy clustering → pacing signatures → route-weighted heatmaps → gameplay-camera landmark/junction analysis → skyline signatures → behavior coverage → adversarial seed/camera search → RGB/depth/semantic regression → failure minimization → worst/novel/disagreement review → human calibration → repeat until discovery saturation.

## Playtest checklist

- Do visually different seeds require different decisions?
- Are most seeds clustered in one descriptor region?
- Are apparent alternate routes actually used?
- Are multiple route clusters genuinely different strategies?
- Is difficulty coming from planning or execution?
- Are challenge peaks spaced intentionally?
- Is recovery available soon enough after peaks?
- Do important forks have distinguishable cues before commitment?
- Are landmarks visible from the decisions they are meant to support?
- Do critical landmarks remain visible long enough to identify rather than chatter?
- Are generated roads connected in nav/collision/lane semantics as well as pixels?
- Do connected roads remain drivable at intended speed across seams?
- Does the road graph have useful redundancy rather than one fragile bridge edge?
- Do skyline signatures reveal structural repetition hidden by decorative variance?
- Are novel seeds valid rather than pathological?
- Which valid seeds have the smallest safety margins?
- Which seeds pass static checks but fail dynamically?
- Does semantic/depth comparison reveal repetition or regression hidden by RGB?
- Are rare catastrophic seeds hidden by good averages?
- Did the new generator version lose or overpopulate behavior clusters?
- Has new-cluster and severe-failure discovery actually saturated?
- Do multiple policies strongly disagree on solvability or risk?
- Can severe failures be reduced to compact reproductions?
- Do automated scores correlate with blinded human judgments?
- Did human review create better automated predicates/descriptors?
