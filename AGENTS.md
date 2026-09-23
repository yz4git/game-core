# AGENTS.md

## Repository purpose

`game-core` is a reusable game-design knowledge base.

Store transferable design knowledge, not copyrighted source material.

## Contribution rules

1. Convert source material into original analysis.
2. Do not paste magazine text, scans, screenshots, maps, tables, walkthroughs, or long quotations.
3. Do not create close paraphrases that preserve the source's structure.
4. Prefer mechanisms over examples:
   - weak: "Game X does Y."
   - strong: "Y creates a decision between A and B because..."
5. Separate:
   - observation
   - mechanism
   - generalized principle
   - transfer idea
   - playtest question
6. Record source title/year/URL when useful, but keep the knowledge entry independently understandable.
7. New single-source observations go under `research/`.
8. Promote an idea to `docs/core-principles.md` only when it appears broadly reusable or is supported by multiple observations.
9. When reviewing a game, prioritize:
   - control feel
   - readability
   - decision density
   - dominant strategies
   - learning curve
   - enemy roles
   - risk/reward
   - failure clarity
   - pacing
   - replay value
   before adding cosmetic polish.
10. Never imitate a living or specific creator's protected expression. Extract general design techniques instead.

## Preferred writing style

- concise
- implementation-oriented
- genre-agnostic where possible
- testable
- written in Japanese unless a project requires otherwise

## Key question

For every proposed mechanic or improvement, ask:

> What new decision, skill, prediction, or interaction does this create for the player?

If the answer is "none," treat the feature as content or presentation rather than game-depth improvement.


## Continuous research protocol

For recurring research runs:

1. Read `research/COVERAGE.md` before choosing sources.
2. Prefer sources, years, genres, or themes marked under "Next priorities".
3. Each substantial batch should normally use at least 3 distinct source items when accessible.
4. Do not create a new core principle when an existing principle already captures the mechanism.
5. If a source only reinforces an existing principle, record it under evidence/coverage rather than duplicating the principle.
6. Promote to `docs/core-principles.md` only when the idea is broadly transferable and materially distinct.
7. Update `research/COVERAGE.md` after each research batch:
   - sources/years touched
   - themes covered
   - new principles promoted
   - remaining gaps
8. Prefer expanding under-covered areas:
   - level design
   - enemy encounter composition
   - boss design
   - fighting-game neutral/pressure
   - racing line/vehicle feel
   - shooter spawn/rhythm
   - puzzle teaching
   - economy/progression
   - co-op/social design
   - AI/opponent design
   - UI/input/accessibility
   - production/playtesting
9. A recurring run should add value to the repository, not merely summarize reading.
10. If no genuinely new principle is found, improve an existing guide with stronger tests, examples expressed generically, or cross-genre transfer questions.
