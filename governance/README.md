# Governance

This directory records the rules that keep the repo from drifting.

Research can suggest.
Examples can illustrate.
Patterns can generalize.

Governance decides what must happen before canonical or workflow-critical assets change.

## Current Rules

1. Changes to `/caret-cheatsheet.md` trigger a repo-wide notation review.
2. Changes to `/Caret-it-skill.md` must follow the Caret-it evolution loop.
3. The live repo canon outranks archives, drafts, research, examples, patterns, and external source material.

## Repo Supremacy Rule

When source material conflicts, use this precedence:

1. `/caret-cheatsheet.md`
2. `/notation/`
3. other live repo docs governed by that canon
4. research and external evidence
5. archives and legacy material

Operational meaning:

- research may support a change, but it does not make the change by itself
- external repos may inspire a pattern, but they do not redefine Caret^
- examples and patterns may demonstrate the canon, but they do not set it
- archived or draft wording may help with structure, but not authority

If a contributor finds a conflict, the contributor should:

1. follow the live repo canon
2. mark the conflicting material as stale, downstream, or informational
3. update the repo only through the normal canonical change path

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
