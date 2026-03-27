# Improve Skill

^improve ^depth8 ^verification8 ^grip8
When Joe reports friction, run the smallest-fix loop. Better over time. No bloat.

## Trigger

^when Joe says:

- something went wrong
- this did not work
- fix this
- the system felt wrong
- the router detects a friction report

## Three-Lens Review

^^software-engineer
  Diagnose data-model issues, logic bugs, broken scripts, and misconfigured skill wiring.
  Propose the smallest code or schema change that fixes the root cause.
  Avoid rewrites. Prefer patches and guards.

^^systems-engineer
  Diagnose broken flow, bad routing, missing feedback loops, unreachable states, or unnecessary work.
  Propose the smallest structural change: remove a step, add a route, tighten a handoff.
  Avoid adding complexity.

^^ux-designer
  Diagnose confusion, too many questions, weak defaults, bad wording, and visible friction.
  Propose the smallest interface change: clearer phrasing, fewer steps, cleaner output.
  Avoid rearranging everything.

## Synthesis

^synthesize

- find the overlap
- if two or three lenses point at the same root cause, treat that as the real issue
- produce one improvement plan that names:
  - what changes
  - why it fixes the problem
  - what files are affected
  - whether it is safe now or should be queued

## Re-Review

^review
Run the synthesized plan back past each lens:

- software engineer -> bugs or debt
- systems engineer -> bottlenecks or state inconsistencies
- ux designer -> new confusion or friction

Incorporate valid refinements.

## Final Plan

^report
Present the result in plain language:

- what went wrong
- the fix
- the files affected
- whether it is safe to do now

## Implementation

^route

- if safe and local -> ask Joe whether to apply now, then make the change and log it
- if broader -> save the plan to `data/plans/` with `type: improvement`, `executor: agent`, `status: queued`

## Logging

^log
Record every applied or queued improvement in `data/state.json` -> `improvement_log` with:

- date
- Joe's friction report, brief
- one-line diagnosis
- what changed or was queued
- status: applied or queued

## Rules

^rules

- never apply broad changes without queuing first
- never skip re-review
- prefer the smallest fix, not the cleverest
- if the friction is about Joe's workflow rather than the system, say so and offer coaching instead
- if the same friction appears twice, escalate because the previous fix did not hold
