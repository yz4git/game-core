# Procedural Diversity Metrics

## Goal

A generator is not diverse merely because screenshots differ. Production QA should answer four separate questions:

1. **Validity** — can this seed function?
2. **Decision diversity** — does it ask the player to do something meaningfully different?
3. **Perceptual diversity** — will players remember it as different?
4. **Experience-shape diversity** — does challenge, recovery and navigation unfold differently over time?

## Quality gates before novelty

Hard-fail seeds that violate reachability, collision, slope, spawn, resource or other gameplay invariants. Optimize novelty only among valid candidates. Broken content is not useful diversity.

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

Compare signatures across seeds. High screenshot diversity with low signature diversity indicates cosmetic variation rather than mechanical variety.

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

Track coverage, density, clusters and outliers rather than only averages or extrema.

## Difficulty decomposition

Do not collapse difficulty to one scalar when possible. Separate solution/search burden, precision/timing burden, input density, resource pressure and recovery margin.

Run more than one player model. A seed's effective difficulty is conditional on policy/skill, so compare novice-like, baseline and expert-like agents when feasible.

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

## Strategy diversity

Trace distance alone can reward meaningless variation. Where multiple agents/policies are available, compare their outcome vectors across the same seed/opponent/context matrix. Useful strategies should have different response strengths and weaknesses, not merely different paths.

## Visual repetition

Use deterministic canonical cameras and presentation settings. Cheap perceptual hashes can identify near-duplicates, but follow them with role-aware comparison of landmark placement/silhouette, road or room topology, skyline, biome/palette class, encounter silhouette and large-scale spatial rhythm.

Cosmetic noise should not trick the test into calling two structurally identical worlds diverse.

## Regression strategy

Run both fixed canonical seeds and large fresh cohorts. Compare descriptor and pacing-signature distributions between generator versions. Preserve worst-N failing seeds permanently.

A generator update can keep mean difficulty unchanged while silently making runs flatter, spikier or more exhausting; therefore compare peak spacing, pressure/recovery streaks, transition entropy and route-weighted hazard distributions.

## Human calibration

Automated metrics filter and diagnose; they do not replace playtests. Periodically compare metric predictions with blind human judgments of repetition, difficulty, pacing, fatigue, readability and memorability.

Version metric definitions and thresholds. Retire or reweight metrics that do not predict the intended experience.

## Recommended pipeline

Generate → invariant gates → multi-skill agent traces → decision/strategy clustering → pacing signatures → route-weighted heatmaps → junction/landmark analysis → descriptor distribution → canonical renders → visual similarity → worst-N/outlier review → human calibration.

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
- Are novel seeds valid rather than pathological?
- Does image similarity reflect memorable structure?
- Are rare catastrophic seeds hidden by good averages?
- Did the new generator version shift pacing or strategy distributions?
- Do automated scores correlate with blinded human judgments?
