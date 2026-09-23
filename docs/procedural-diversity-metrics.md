# Procedural Diversity Metrics

## Goal

A generator is not diverse merely because screenshots differ. Production QA should answer three separate questions:

1. **Validity** — can this seed function?
2. **Decision diversity** — does it ask the player to do something meaningfully different?
3. **Perceptual diversity** — will players remember it as different?

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

Aggregate normalized agent occupancy over many seeds. Use them to reveal:

- repeated practical corridors
- nominal branches that are almost never useful
- over-dominant spawn/goal relationships
- repeated choke points
- unused generated space

## Expressive-range dashboard

Choose a few descriptors tied to player decisions, for example:

- route alternatives
- traversal length
- branch entropy
- hazard density
- resource slack
- planning search cost
- execution tolerance

Track coverage, density, clusters and outliers rather than only averages or extrema.

## Difficulty decomposition

Do not collapse difficulty to one scalar when possible. Separate:

- solution/search burden
- precision/timing burden
- input density
- resource pressure
- recovery margin

This makes a hard seed diagnosable.

## Visual repetition

Use deterministic canonical cameras and presentation settings. Cheap perceptual hashes can identify near-duplicates, but follow them with role-aware comparison of:

- landmark placement/silhouette
- road or room topology
- skyline
- biome/palette class
- encounter silhouette
- large-scale spatial rhythm

Cosmetic noise should not trick the test into calling two structurally identical worlds diverse.

## Regression strategy

Run both:

- **fixed canonical seeds** — deterministic regression fixtures
- **large fresh cohorts** — population/distribution regression

Compare descriptor distributions between generator versions. Preserve worst-N failing seeds permanently.

## Human calibration

Automated metrics filter and diagnose; they do not replace playtests. Periodically compare metric predictions with blind human judgments of repetition, difficulty, readability and memorability.

Retire or reweight metrics that do not predict the intended experience.

## Recommended pipeline

Generate → invariant gates → agent traces → decision signatures → route heatmaps → descriptor distribution → canonical renders → visual similarity → worst-N/outlier review → human calibration.

## Playtest checklist

- Do visually different seeds require different decisions?
- Are most seeds clustered in one descriptor region?
- Are apparent alternate routes actually used?
- Is difficulty coming from planning or execution?
- Are novel seeds valid rather than pathological?
- Does image similarity reflect memorable structure?
- Are rare catastrophic seeds hidden by good averages?
- Did the new generator version shift the whole distribution?
- Can players transfer learned rules while still encountering novelty?
