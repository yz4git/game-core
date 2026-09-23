# Procedural Pacing and Readability QA

## Goal

A procedural level can be valid, visually varied and still feel repetitive, exhausting or confusing. Production QA should therefore validate **experience shape** as well as geometry.

## 1. Pacing is a sequence

Represent a route as sampled values for:
- threat
- resource pressure
- execution density
- recovery opportunity
- navigation uncertainty

Measure more than averages:
- peaks and peak spacing
- longest pressure streak
- longest dead/low-demand streak
- recovery delay after a peak
- transition entropy
- encounter-type n-grams

Two seeds with identical mean difficulty can have radically different pacing.

## 2. Use multiple player models

Run at least novice-like, baseline and expert-like policies when feasible. Record hazard/death/success curves separately.

A seed is not simply "difficulty 0.7"; it is a challenge distribution conditional on a player policy.

## 3. Route-weight encounter pressure

Spatial enemy/threat heatmaps are useful, but weight them by traversal probability. A severe room that almost nobody reaches should not dominate the experienced-pacing estimate.

Maintain both:
- raw authored/generated threat field
- route-weighted experienced threat field

## 4. Explicit recovery budget

After a high-pressure segment, bound the time/distance until at least one meaningful recovery mechanism:
- safer geometry
- lower enemy pressure
- health/resource opportunity
- reduced input density
- planning pause

The exact budget is genre-specific and should be calibrated against human playtests.

## 5. Landmark usefulness

A landmark is useful when it is:

**visible × distinctive × stable × near a meaningful decision**

Asset uniqueness alone is insufficient.

At each important junction, collect:
- visible landmark IDs
- approximate screen size / visibility
- approach-angle silhouette descriptor
- angular separation
- branch identity

Flag important forks whose alternatives have weak perceptual separation.

## 6. Junction ambiguity

Compare branches using coarse features such as:
- heading
- width
- elevation
- lighting/biome class
- landmark signature
- destination role

Low separation across several features indicates a likely wayfinding problem even if the navigation graph is valid.

## 7. Cluster traces before heatmaps

An aggregate occupancy map can make two real strategies look like one fuzzy route.

Pipeline:
1. normalize traces into decision signatures
2. cluster signatures
3. render occupancy/transition heatmaps per cluster
4. compare cluster outcome profiles

## 8. Strategy diversity needs counterfactual tests

Trace distance alone can reward meaningless variation. For each strategy/policy, evaluate an outcome vector across the same seed/opponent/context matrix.

Useful strategies should have different strengths, weaknesses or responses—not merely different paths to the same result.

## 9. Generator regression

For fixed seeds and fresh cohorts compare distributions of:
- pacing peaks
- pressure/recovery streaks
- transition entropy
- junction ambiguity
- landmark separation
- route clusters
- strategy outcome vectors

Do not accept a release merely because validity and mean difficulty stayed constant.

## 10. Human calibration loop

Periodically ask blinded players to rate seed pairs for:
- repetition
- pacing quality
- fatigue
- readability
- memorability
- perceived difficulty

Measure whether automated metrics predict these labels. Version metric definitions and thresholds; retire proxies that stop correlating.

## Recommended CI pipeline

Generate cohort → validity gates → multi-skill agents → trace clustering → pacing signatures → route-weighted pressure → junction/landmark analysis → distribution regression → worst-N seed capture → periodic human calibration.

## Playtest checklist

- Are difficulty peaks spaced intentionally?
- Is recovery available after peaks?
- Does novice/expert experience diverge in expected ways?
- Are alternate routes actually distinct strategies?
- Can players distinguish branches before committing?
- Are landmarks visible from the decisions they are meant to support?
- Does aggregate telemetry hide multiple behavior clusters?
- Do automated repetition/readability scores correlate with humans?
- Did the latest generator change pacing shape even if mean difficulty is unchanged?
