# Metamorphic Procedural QA

Use this guide when generated content has many valid outputs and a single golden answer is not meaningful.

## Core idea
Test a **relationship between controlled sibling cases**. Start from one known-valid parent and change one declared semantic factor. The QA oracle is the expected relationship, not a specific final layout.

## Relation types
| Relation | Expected result | Example |
|---|---|---|
| PRESERVE | selected gameplay semantics remain unchanged | decoration-only regeneration must not change collision/nav |
| MONOTONIC | selected margin moves in a declared direction | more encounter pressure must not improve intended pressure margin beyond tolerance |
| BOUNDED | result stays in an allowed envelope | small timing perturbation may change trajectory but not completion/damage bands excessively |
| ROUND_TRIP | semantic state survives conversion | save/export/reload preserves topology, IDs and critical progression |
| PERMUTATION | unordered input ordering is irrelevant | shuffling equivalent entity lists must not alter game truth |
| SYMMETRY | declared symmetric transformation preserves opportunity | mirrored arena should not create unintended side advantage |
| POLICY_ORDER | intended skill ordering remains intact | expert/baseline/novice/exploit ordering should not invert unexpectedly |

## Required test record
For every sibling test store:
- parent ID and generator/ruleset epoch
- relation type
- transformation ID and semantic delta
- protected semantic domains
- repair delta
- before/after margin vector
- before/after policy outcomes
- violation magnitude
- failure signature
- human confirmation status
- compute cost

## Hypothesis-footprint rule
A repair is admissible only when it restores sacred validity without substantially changing the tested hypothesis. If the test narrows a choke and repair widens that choke, the candidate is not strong evidence for that hypothesis.

Treat repair overlap as:
- **0**: unrelated repair; evidence remains strong.
- **small**: retain but lower confidence.
- **large**: reject or regenerate the sibling.

## Prefer sibling comparisons
Do not compare two unrelated random seeds when a same-parent counterfactual can be constructed. Common ancestry removes unrelated topology/content variance and makes failures easier to explain and shrink.

## Pair shrinking
Shrink parent and child together. Preserve:
1. both cases are valid,
2. the declared transformation remains meaningful,
3. the relation still fails.

The regression fixture should contain the smallest useful **difference**, not merely the smallest failing world.

## Policy-order testing
For generated encounters and traversal challenges, run multiple policies:
- novice
- baseline
- expert
- exploit/adversarial

A content sample can be technically solvable while rewarding the wrong policy. Record reversals separately from ordinary difficulty failures.

## CI promotion
Run cheap semantic relations broadly. Promote to expensive simulation/render/human review when:
- violation magnitude is high,
- signature is novel,
- machine policies disagree,
- repair overlap is uncertain,
- relation historically predicts human-confirmed failures.

Always retain an exploration floor for low-yield relation families so the scheduler does not become blind to new bug classes.

## Playtest review questions
- What exactly was transformed?
- Which gameplay properties were promised to stay the same?
- Which properties were expected to move, and in what direction?
- Did repair touch the hypothesis?
- Is the violation reproducible from the same parent?
- Does the result hold across player/agent policies?
- Can the pair be shrunk without losing the relation failure?
- Would a player perceive the changed outcome as a real rule/feel change?
