# Automated Highlight & Spectator Information Safety

## Purpose

Replay/highlight systems should produce clips that are meaningful and understandable while never treating spectator delay as a substitute for information authorization.

## Highlight ranking

Use a vector rather than one excitement score:
- meaningful state delta
- rarity / novelty
- risk or comeback magnitude
- setup/payoff relation
- audiovisual/reaction confidence
- viewer comprehension
- duplication versus already selected clips

Large explosions, kills and scores are useful signals but not definitions of importance.

## Hard negatives

Maintain examples that look exciting but are strategically routine:
- cosmetic explosions
- repeated easy kills
- low-stakes overtakes
- standard finisher animations
- noisy crowd/audio without important state change

False-positive quality matters because top-k ranking otherwise fills reels with visually loud repetition.

## Clip boundaries

Extract three phases where possible:

**setup → tension/decision → resolution**

Backtrack from a detected peak to the earliest causal decision the viewer needs, then extend until the result stabilizes. Evaluate whether a first-time viewer can explain why the outcome mattered.

## Diversity selection

After candidate scoring, rerank with diversity penalties across:
- event signature
- actor/player
- location
- tactic
- emotional rhythm
- camera presentation

A reel should summarize multiple reasons the run/match was interesting.

## Audience-specific rankings

Do not force one ranking to serve every purpose.
- public recap: legibility and meaningful swing
- coaching: decision error / alternative opportunity
- personal memories: achievements, rivals, PBs, repeated-attempt payoff
- QA: rare state transitions and suspicious anomalies

Document what human labels were optimized for before using them as ground truth.

## Spectator authorization boundary

Never send hidden state to spectators merely because it will be delayed.

Create a spectator-specific state projection. Classify fields, for example:
- PUBLIC
- PARTICIPANT
- TEAM
- PRIVATE
- DEBUG

Public spectator/replay export should be allowlist-based. Test schema differences automatically.

## Choosing spectator delay

Delay is a competitive-policy parameter, not an access-control mechanism. Choose it from how long leaked information remains actionable:
- travel/action time
- strategic planning horizon
- communication latency
- round/phase duration
- respawn/re-entry timing

Run explicit collusion simulations. If delayed information still changes a live decision, increase delay or further reduce spectator information.

## Automation-friendly replay controls

Expose stable operations for tools as well as humans:
- seek by tick/time
- pause/step/speed
- follow entity
- camera preset/keyframes
- overlay toggles
- event jump
- deterministic clip render

A highlight candidate should be renderable consistently without manual camera repair.

## Comprehension evaluation

Measure interest and understanding separately. After a clip, ask:
- what changed?
- why did it matter?
- who/what caused it?

High engagement with low causal understanding is not automatically a good game highlight.

## Privacy-minimized learning

Prefer aggregate/derived signals when sufficient:
- event-jump count
- rewind rate
- anonymous clip rating
- aggregate watch completion
- state-delta features

Do not retain raw chat, voice, faces or identifiers merely to improve ranking. Richer signals require a separate justification and appropriate consent/policy.

## Game-design diagnostic

Aggregate highlight signatures by level/seed/session:
- meaningful-event density
- duplicate-signature ratio
- longest low-event interval
- event-type entropy
- actor/tactic coverage

Low diversity can reveal repetitive encounter design even when procedural geometry or visuals vary.

## QA checklist

- Does top-k contain hard-negative false positives?
- Can viewers explain each clip's causality?
- Does the reel contain multiple event signatures?
- Can a public spectator packet reveal hidden state?
- Is export controlled by an explicit field allowlist?
- Is spectator delay justified by actionable-information lifetime?
- Can collusion still exploit delayed data?
- Can tools render a candidate deterministically?
- Are ranking telemetry inputs privacy-minimized?
- Do low-highlight regions correspond to intentional pacing?