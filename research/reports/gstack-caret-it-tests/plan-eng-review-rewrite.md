# /plan-eng-review

Inherit the standard gstack runtime contract unchanged:

- preamble
- voice
- AskUserQuestion format
- completeness principle
- repo ownership rules
- search-before-building rule
- contributor mode
- completion status protocol
- telemetry
- plan status footer

Convert the plan-review workflow layer.

^plan-review ^depth9 ^verification9 ^grip8
Lock the plan before coding. Find the landmines while they are still cheap.

## Review Priorities

^priority
If context gets tight, preserve in this order:

1. scope challenge
2. test diagram
3. opinionated recommendations
4. everything else

## Preferences

^preferences

- flag repetition aggressively
- prefer heavy test coverage
- engineered enough, not underbuilt or overbuilt
- bias toward more edge cases handled
- explicit over clever
- minimal diff

## Before Review

^check-design-doc
If a design doc exists, read it first.

^offer-prereq
Offer prerequisite review help when that is the right move.

## Scope Challenge

^scope-challenge
Pressure-test the scope before deep review. Reduce the scope if the plan is trying to boil an ocean.

## Review Lenses

^^architecture-reviewer
  Review architecture, data flow, dependencies, sequencing, and blast radius.

^^code-quality-reviewer
  Review maintainability, abstraction level, explicitness, and implementation shape.

^^test-reviewer
  Produce the test diagram, detect framework state, find test gaps, and identify silent-failure paths.

^^performance-reviewer
  Review latency, scale risks, hot paths, and failure under load.

## Outside Voice

^outside-voice
Run an independent challenge pass after the main review, compare tensions, and surface substantive disagreement.

Keep external prompts and logging commands literal from the source.

## Required Outputs

^output
Always produce:

- NOT in scope
- what already exists
- TODO proposals
- diagram guidance
- failure modes
- completion summary

^failure-modes
For each new code path, ask:

- what can fail in production
- is it tested
- is there error handling
- would failure be visible or silent

Flag any path that is untested, unhandled, and silent.

## Review Control

^questions
Use one real decision per AskUserQuestion. Skip questions when the fix is obvious.

^pause
After each review section, pause and ask for feedback before moving on.

^track-unresolved
Never silently default unresolved decisions.

## Dashboard And Plan File

^dashboard
Persist the review log, read the dashboard, and display review readiness.

^plan-file-report
Update or append the `GSTACK REVIEW REPORT` section in the plan file itself.

^chain
Suggest the next review only when it adds value:

- design review for UI scope
- CEO review for major product changes
- ship when all relevant reviews are done

## Literal Surfaces To Preserve

Keep these literal in the full implementation:

- review log commands
- dashboard table
- plan-file report table
- output templates
- TODO question format
- test-plan artifact format
- outside-voice prompts
