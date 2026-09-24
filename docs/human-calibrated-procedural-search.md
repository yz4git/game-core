# Human-Calibrated Procedural Search

Batch 43 production guidance.

Human review should improve where valid procedural search spends budget, not redefine the legality contract. Learned scheduling runs only after invariant and validity checks.

## Contextual scheduling
Measure mutation usefulness by genre, generator/ruleset version, behavior region, topology family, decision phase and margin region. Keep parent/region selection telemetry separate from mutation-method selection telemetry.

## Evidence value
Prefer new actionable failure families, severity, reproducibility and information gain over raw failure count. Repeated instances of an already-understood signature receive diminishing search credit. Human-rejected cases remain useful calibration evidence.

## Exploration floor
Reserve minimum coverage for every supported mutation family plus canonical and unbiased random samples. Adaptive scheduling only reallocates the remaining budget.

## Version drift
Discount old evidence when generator rules, physics, agents, descriptors or validity rules change. Record the version that produced each learned weight.

## Human-review allocation
Prioritize high-severity, uncertain, novel and disagreement cases. Record skill cohort separately so novice and expert boundaries are not averaged into a misleading single label.

## Compound boundaries
After individual mutation families show useful evidence, selectively test promising pairs and track pair-specific yield instead of enumerating every combination.

## Scheduler regression test
Before adopting a scheduling change, replay a fixed corpus of known reachable failure families. Compare time-to-first finding, severe-family recall, human-confirmed yield, invalid rate, diversity and compute cost. Do not accept higher average yield if a rare severe family disappears.

## Audit record
Store: context, parent, mutation method, semantic delta, repair delta, margins, failure signature, automated severity, human label/cohort, compute cost and scheduler version.

## Pipeline
VALIDITY CONTRACT → CONTEXT/PARENT SELECTION → MUTATION SELECTION → SEMANTIC MUTATION → VALIDITY/REPAIR → MARGIN + SIGNATURE → SELECTIVE HUMAN REVIEW → COHORT LABEL → CONTEXTUAL CREDIT UPDATE → SCHEDULER REGRESSION CORPUS

## Review questions
- Is one common failure dominating learned weights?
- Which contexts reverse mutation-method rankings?
- Does every mutation family still receive exploration budget?
- Are stale weights retained after a generator/ruleset change?
- Did better results come from parent selection or mutation selection?
- Which automated severity rules repeatedly overestimate human severity?
- Are novice-only and expert-only failures both retained?
- Which mutation pairs reveal compound failures?
- Can surprising scheduler weights be traced to reviewed evidence?
