# Procedural 3D Visibility and Road QA

## Purpose

Automate the failures that make a generated 3D world feel broken even when it renders: roads that disconnect at seams, junctions that cannot be read in time, landmarks hidden from actual routes, unstable occlusion, districts whose silhouettes repeat despite cosmetic variation, moving occluders that hide cues at the wrong moment, and interiors whose floors/portals destroy orientation.

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

Drive canonical routes using a deterministic baseline controller. Record completion, steering/braking intervention peaks, off-road time, collision count, reverse/recovery events, minimum lane margin and speed loss around seams. A connected graph that forces emergency corrections is a dynamics failure.

## Gameplay visibility contracts

Rendering systems answer whether geometry is occluded. Game design also needs to answer **when a cue must become visible and remain identifiable**.

For each critical landmark/objective/exit define relevant approach routes, gameplay camera profile, expected first-visible range, minimum continuous visible duration/distance, required visibility before a decision point, optional reveal/occlusion zones, navigation scope, and supported lighting/portal states.

Measure along route trajectories rather than only from hand-picked screenshots.

Recommended cue contract:

`cueId, scope, routeSegments, decisionId, revealStart, requiredStableWindow, minScreenArea, minIdentificationMargin, allowedOccluderClasses, portalStateMask, lightingProfileMask`

## Landmark metrics

At fixed route intervals capture visible/not visible, screen-space area, angular position/separation, depth, occluding semantic ID and distance to next consequential junction. Aggregate first-visible distance, route-visible fraction, longest occluded interval, last sighting before junction and visibility transition rate.

Short rapid visible/hidden bursts are **occlusion chatter**. A cue can be technically visible often yet remain unreadable because each exposure is too short.

## Dynamic occlusion is temporal QA

A moving bus, crowd, door, enemy or foreground prop can invalidate a cue only during the decision window. Treat visibility as a time series.

For each consequential decision record:

- stable-visible time immediately before commitment
- longest hidden interval
- probability of deadline occlusion across traffic/crowd seeds
- p5 visibility margin, not only mean visibility
- occluder semantic class
- camera angular velocity at visibility transitions

Separate design occlusion from renderer-query latency. A one-frame pop during rapid camera motion is a different defect from a landmark being hidden for the whole braking window.

Do not assume engine culling roles equal gameplay roles. Maintain semantic tags such as `canOccludeCriticalCue` and `mayBeOccluded` independently of static/dynamic renderer flags.

## Occluder severity

Duration alone is insufficient. Classify major occluders as static, periodic, player-controlled, stateful or stochastic. Weight a blockage by predictability, duration, player agency and consequence. A predictable train that briefly blocks a sign is different from arbitrary facade clutter that hides it permanently.

## Stochastic occupancy testing

Traffic and crowds turn visibility into a distribution. Replay canonical routes over occupancy seeds and report probability of a required cue being blocked at its deadline. Preserve the seeds that minimize visibility margin as regression fixtures.

## Junction preview test

At each consequential fork, sample backward along the approach until the safe braking/steering deadline. Compare branches using heading, width/lane count, elevation, road marking/sign identity, biome/lighting semantic class, visible destination landmark and screen-space angular separation.

Flag forks whose branch-separation score stays below threshold until after commitment.

## Indoor and multi-floor cue hierarchy

Interiors should not depend on a distant global landmark that walls inevitably remove. Use overlapping navigation scopes:

1. global/world anchor
2. district/building anchor
3. floor/zone anchor
4. junction-local discriminator
5. destination/door cue

Test **cue handoff** rather than each landmark in isolation. Along a route, compute intervals in which each cue is usable and flag decision-relevant gaps where the previous cue has disappeared before the next becomes understandable.

More raw visibility is not automatically better. A cue is valuable when it reduces branch ambiguity. Extra visible geometry can create noise or false affordance.

## Vertical-transition contract

For stairs, ramps, lifts, shafts and teleporters, verify both ends:

- floor/zone identity is distinguishable
- arrival facing direction is intentional
- an orientation anchor survives or is immediately replaced
- immediate route choices are readable
- stacked floors do not expose false destinations
- player can recover orientation without opening the map

Treat visually similar adjacent floors as an adversarial case.

## Stateful portals

Doors, shutters, destroyed walls, lift gates and scripted blockers mutate topology and visibility together. Every meaningful portal state must participate in both navigation-graph and visibility-graph regression.

For `closed/open/locked/destroyed` or equivalent states, rerun reachability, cue visibility, branch readability and semantic-buffer comparisons. Opening a shortcut must not silently erase the cue hierarchy or expose a misleading destination.

## Lighting and identification robustness

Line-of-sight is not recognition. Day/night, weather, fog, auto-exposure, bloom, headlights and tunnel transitions can leave a landmark geometrically visible while destroying its identifying features.

For critical cues evaluate:

- screen-space area
- local luminance/contrast proxy
- silhouette separation from background
- semantic-ID visibility
- human recognition rate on worst-N captures
- stable identification interval before commitment

Avoid mandatory visual decisions inside unstable exposure/adaptation windows unless another modality carries the information.

## Occlusion-boundary fixtures

Coarse cells, portals and simplified occluders are vulnerable around small apertures and boundaries. Permanently retain adversarial camera positions at doorframes, windows, corners, stair mouths, atria, thin walls and narrow gaps. Compare engine visibility against ground-truth rays/depth/semantic buffers.

## Skyline signature

RGB diversity is not skyline diversity. For canonical viewpoints, sample horizon elevation around azimuth and store height-band occupancy, dominant peaks, peak spacing, dominant landmark IDs, silhouette self-similarity and district-to-district signature distance.

Use this to find generators that change facade noise while repeating the same massing rhythm.

## Reveal scheduling

Do not maximize landmark visibility everywhere. Useful landmarks can disappear and reappear. Define far/mid/near envelopes so global orientation cues do not erase local discovery or overwhelm neighborhood cues. Review whether reappearance coincides with decisions where the cue matters.

## Canonical camera matrix

Visibility tests must use shipped camera semantics. At minimum include relevant combinations of walk/drive/drone, camera height/pitch, FOV, portrait/landscape if supported, representative phone/tablet aspect ratios, and camera follow/offset state. Editor free-camera screenshots do not substitute for these.

## Semantic visual regression

Capture deterministic buffers where feasible: RGB, normalized depth, semantic object/class ID, road/lane mask, collision/walkability/drivability, landmark ID and major occluder ID.

Use RGB for presentation regressions and semantic buffers for gameplay regressions. This reduces false alarms from lighting/particles while exposing geometry or affordance changes hidden by similar colors.

## Adversarial search

Search route/camera/world-state parameter space for minimum landmark visibility margin, longest pre-junction cue occlusion, maximum branch ambiguity, maximum road-mask seam discontinuity, maximum depth/semantic disagreement, highest occlusion-chatter rate, largest cue-handoff gap, worst floor ambiguity and lowest night-time identification margin.

The full matrix of camera × route × portal state × traffic seed × time-of-day × weather × device is too expensive to render exhaustively. Run cheap graph/ray/contrast predicates broadly, then fully render and human-review worst-N, boundary cases and newly discovered failure clusters.

## CI tiers

### Fast / per change
- graph connectivity
- lane seam matching
- collision/drivable continuity
- curvature/grade/width bounds
- canonical landmark rays
- portal-state reachability
- cue-handoff coverage

### Standard
- baseline-agent routes
- gameplay-camera captures
- junction preview metrics
- skyline signatures
- semantic-buffer regression
- vertical-transition fixtures
- day/night identification proxy

### Scheduled stress
- large fresh seed cohort
- adversarial seed/camera/world-state search
- stochastic traffic/crowd occupancy
- worst-N retention
- multi-device camera matrix
- portal × lighting × occupancy boundary combinations

## Human calibration

Automated tests should select cases for humans, not declare aesthetic truth. Periodically ask blinded reviewers:

- could you identify the correct branch before commitment?
- which landmark did you use to orient?
- did any road seam feel surprising or unfair?
- could you distinguish districts from silhouette alone?
- did a landmark flicker or disappear at the wrong moment?
- when the global cue disappeared indoors, what cue replaced it?
- after changing floors, could you state your floor/zone and facing direction?
- at night or after an exposure transition, could you identify the cue rather than merely see it?

Feed repeated human failures back into measurable predicates and threshold calibration.

## Minimum production dashboard

Per generator build show: hard road failures, bridge/articulation distribution, baseline route completion, seam intervention p95, landmark visibility p5, deadline-occlusion probability, pre-junction preview p5, occlusion-chatter worst-N, cue-handoff gap worst-N, vertical-transition ambiguity, portal-state regressions, lighting identification p5, skyline cluster occupancy, semantic-buffer regressions, and new severe failures per 1,000 seeds.