# Procedural 3D Visibility and Road QA

## Purpose

Automate the failures that make a generated 3D world feel broken even when it renders: roads that disconnect at seams, junctions that cannot be read in time, landmarks hidden from actual routes, unstable occlusion, and districts whose silhouettes repeat despite cosmetic variation.

## Four validity layers for roads

Do not call a road valid until it passes all four:

1. **Topology** — graph edges really connect; directionality and destination reachability are valid.
2. **Geometry** — lane/centerline endpoints, surface, collision and elevation join continuously.
3. **Dynamics** — intended vehicles can traverse curvature, grade and width transitions at intended speed.
4. **Semantics** — markings, signs, branch identity and navigation metadata agree with the route graph.

Track connected components, articulation points, graph bridges/cut-edges, alternate-route ratio, detour factor, lane-endpoint mismatch, curvature jump, grade jump and width jump.

## Seam contract

For every chunk/tile boundary with a road crossing:

- centerline endpoints pair within tolerance
- lane count and direction map intentionally
- surface and collision overlap without a gap/step
- nav edges connect both representations
- elevation and tangent continuity stay inside traversal limits
- semantic road ID / route role is preserved or explicitly transitioned

A screenshot is insufficient evidence because visually touching surfaces can still have disconnected navigation or collision.

## Baseline-agent traversal

Drive canonical routes using a deterministic baseline controller. Record:

- completion
- steering/braking intervention peaks
- off-road time
- collision count
- reverse/recovery events
- minimum lane margin
- speed loss around seams

A connected graph that forces emergency corrections is a dynamics failure.

## Gameplay visibility contracts

Rendering systems answer whether geometry is occluded. Game design also needs to answer **when a cue must become visible**.

For each critical landmark/objective/exit define:

- relevant approach routes
- gameplay camera profile
- expected first-visible range
- minimum continuous visible duration/distance
- required visibility before a decision point
- optional reveal/occlusion zones

Measure along route trajectories rather than only from hand-picked screenshots.

## Landmark metrics

At fixed route intervals capture:

- visible/not visible
- screen-space area
- angular position and separation
- depth
- occluding semantic ID
- distance to next consequential junction

Aggregate first-visible distance, route-visible fraction, longest occluded interval, last sighting before junction and visibility transition rate.

Short rapid visible/hidden bursts are **occlusion chatter**. A cue can be technically visible often yet remain unreadable because each exposure is too short.

## Junction preview test

At each consequential fork, sample backward along the approach until the safe braking/steering deadline. Compare branches using:

- heading
- width / lane count
- elevation
- road marking/sign identity
- biome/lighting semantic class
- visible destination landmark
- screen-space angular separation

Flag forks whose branch-separation score stays below threshold until after commitment.

## Skyline signature

RGB diversity is not skyline diversity. For canonical viewpoints, sample horizon elevation around azimuth and store:

- height-band occupancy
- dominant peaks
- peak spacing
- dominant landmark IDs
- silhouette self-similarity
- district-to-district signature distance

Use this to find generators that change facade noise while repeating the same massing rhythm.

## Reveal scheduling

Do not maximize landmark visibility everywhere. Useful landmarks can disappear and reappear. Define far/mid/near envelopes so global orientation cues do not erase local discovery or overwhelm neighborhood cues.

Review whether reappearance coincides with decisions where the cue matters.

## Canonical camera matrix

Visibility tests must use shipped camera semantics. At minimum include relevant combinations of:

- walk / drive / drone
- camera height and pitch
- FOV
- portrait/landscape if supported
- representative phone/tablet aspect ratios
- camera follow/offset state

Editor free-camera screenshots do not substitute for these.

## Semantic visual regression

Capture deterministic buffers where feasible:

- RGB
- normalized depth
- semantic object/class ID
- road/lane mask
- collision/walkability/drivability
- landmark ID
- major occluder ID

Use RGB for presentation regressions and semantic buffers for gameplay regressions. This reduces false alarms from lighting/particles while exposing geometry or affordance changes hidden by similar colors.

## Adversarial camera search

Random screenshots are poor at finding narrow alignment failures. Search route/camera parameter space for:

- minimum landmark visibility margin
- longest pre-junction cue occlusion
- maximum branch ambiguity
- maximum road-mask seam discontinuity
- maximum depth/semantic disagreement
- highest occlusion-chatter rate

Keep worst-N and near-threshold camera positions as permanent fixtures.

## CI tiers

### Fast / per change
- graph connectivity
- lane seam matching
- collision/drivable continuity
- curvature/grade/width bounds
- canonical landmark rays

### Standard
- baseline-agent routes
- gameplay-camera captures
- junction preview metrics
- skyline signatures
- semantic-buffer regression

### Scheduled stress
- large fresh seed cohort
- adversarial seed search
- adversarial camera search
- worst-N retention
- multi-device camera matrix

## Human calibration

Automated tests should select cases for humans, not declare aesthetic truth. Periodically ask blinded reviewers:

- could you identify the correct branch before commitment?
- which landmark did you use to orient?
- did any road seam feel surprising or unfair?
- could you distinguish districts from silhouette alone?
- did a landmark flicker or disappear at the wrong moment?

Feed repeated human failures back into measurable predicates and threshold calibration.

## Minimum production dashboard

Per generator build show: hard road failures, bridge/articulation distribution, baseline route completion, seam intervention p95, landmark visibility p5, pre-junction preview p5, occlusion-chatter worst-N, skyline cluster occupancy, semantic-buffer regressions, and new severe failures per 1,000 seeds.
