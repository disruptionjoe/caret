# Governance

This directory records the rules that keep the repo from drifting.

Research can suggest.
Examples can illustrate.
Patterns can generalize.

Governance decides what must happen before canonical or workflow-critical assets change.

## Current Rules

1. Changes to `/caret-cheatsheet.md` trigger a repo-wide notation review.
2. Changes to `/Caret-it-skill.md` must follow the Caret-it evolution loop.

## Caret-it Evolution Rule

`/Caret-it-skill.md` is not allowed to drift by vibe.

Any meaningful update to that skill should:

1. run the optimization workflow in `/research/reports/caret-it-optimization/WORKFLOW.md`
2. produce or extend an evidence bundle under `/research/reports/`
3. state whether the change came from:
   - local-skill evidence
   - external-repo evidence
   - canon alignment
   - shared-contract extraction
4. update the skill only when the lesson is general, not just file-specific

## Research Boundary

The workflow itself, the rounds, the external trials, and the report bundles belong in `research/`.

The rule that says future Caret-it changes must use that workflow belongs here.
