# Procedural Boundary Interaction QA

Practical guide for finding failures caused by interactions between otherwise-valid procedural constraints.

## Core model

Do not define coverage as “number of seeds.” Define a semantic margin vector over player-facing budgets, then inspect where two margins approach failure together.

Examples:
- shooter: reaction slack × escape-space
- racing: braking slack × road clearance
- puzzle: irreversible commitment × recovery/restart cost
- RPG: resource slack × recovery opportunity
- 3D navigation: cue visibility × decision deadline

## Pair-state model

Each semantic pair-region is one of:
- **UNREACHABLE** — supported by grammar/constraint evidence
- **UNKNOWN** — not yet generated or proven impossible
- **INTERIOR** — comfortably safe
- **NEAR_PASS** — passes with small positive margin
- **NEAR_FAIL** — fails with small negative margin
- **CONFIRMED** — human or high-confidence machine-confirmed boundary behavior
- **PROMOTE_T3** — pair needs a third factor to explain variance

Never silently convert UNKNOWN to UNREACHABLE.

## Choosing dimensions

Use dimensions that change player decisions. Avoid Cartesian products of raw implementation variables.

Good semantic dimensions:
- reaction-time slack
- clearance in avatar-widths
- stopping-distance slack
- reversible-move surplus
- resource slack before mandatory encounter
- stable cue visibility before commitment
- recovery distance/time
- unavoidable-damage estimate

Correlated implementation fields should be collapsed unless they create distinct player choices.

## Repair distance

Record a vector rather than `repaired=true`:

`repair = { topology, clearance, timing, resource, visibility, encounter_pressure }`

Normalize by gameplay scale:
- geometry / avatar width
- timing / expected reaction window
- braking / stopping distance
- resource / expected encounter spend
- visibility / decision deadline

Classify every repair:
1. **invariant-restoring** — restores legality while preserving the tested hypothesis.
2. **hypothesis-altering** — directly weakens or changes the pressure being tested.

Use a strict cap for hypothesis-altering repairs. If the repair changes the exact boundary under investigation, reject or archive the candidate rather than calling it evidence.

## Matched counterfactual fixtures

For severe or informative cases, save siblings:
- same parent/context
- one controlled semantic delta
- one near-pass
- one near-fail

Regression should preserve the intended ordering. This gives a much better debugging target than a single pathological seed.

## Pair to 3-way promotion

Start with semantic pairs. Promote only when evidence warrants it:
- severe human-confirmed failure
- repeated near-zero margins
- novice/expert or agent-policy disagreement
- unexplained outcome variance
- unstable repair distance
- a known contextual factor repeatedly flips outcome

Typical third factors: occupancy, speed tier, lighting, skill policy, prior resource state.

## Empirical calibration

Use real generator history where available.

1. Recompute semantic margins for historical candidates.
2. Sample human-confirmed pass/fail cases near zero.
3. Fit genre/cohort-specific near-boundary bands.
4. Measure repair-distance distributions by repair family.
5. Choose caps from false-accept / false-reject tradeoffs, not aesthetics.
6. Hold out later generator history to test whether the threshold would have missed severe failures.
7. Re-run after generator, physics, ruleset, agent, or descriptor changes.

## Coverage target

Do not stop at raw occupancy. Require:
- canonical regression complete
- unbiased-random floor complete
- important reachable pair regions represented
- near-pass and near-fail evidence around important boundaries
- UNKNOWN backlog challenged by targeted search
- severe-signature discovery saturated over multiple windows
- promoted 3-way regions either covered or explicitly deferred
- matched counterfactual fixtures retained for severe boundaries

## Production telemetry

Persist:
`generator_epoch, seed, parent, mutation, margin_before, repair_vector, repair_class, margin_after, pair_state, policy_results, human_label, failure_signature, compute_cost`.

Track:
- boundary discoveries / CPU-hour
- severe signatures / CPU-hour
- human-confirmed precision
- p50/p95 repair distance
- hypothesis-altering repair rate
- UNKNOWN→reachable conversion rate
- pair→3-way promotion yield
- counterfactual fixture survival across releases

## Review questions

- Are we covering player decisions or raw parameters?
- Which pair of tolerable pressures becomes unfair together?
- Is this empty cell truly impossible or merely unexplored?
- Did repair restore legality or erase the hypothesis?
- Can we produce a minimally different passing sibling?
- Does a third factor consistently explain pair-level variance?
- Are thresholds calibrated against real players and held-out generator history?
