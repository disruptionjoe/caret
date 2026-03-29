# Caret-it Parity Loop

This bundle turns Caret-it into a repeatable equivalence loop.

The question is no longer only:

- how much shorter did the rewrite get

It is also:

- did the rewrite keep the skill's job intact
- what was preserved
- what drifted
- how many iterations did it take to find out

## Start Here

1. `WORKFLOW.md`
2. `PROMPT-SUITE-TEMPLATE.md`
3. `PARITY-MATRIX-TEMPLATE.md`

## What This Is For

Use this bundle when you want to:

- test whether a compacted skill is replacement-safe
- compare original and rewritten behavior on the same prompt set
- rerun the rewrite after each patch
- stop when parity passes or the rewrite clearly plateaus

## Output Modes

The loop can end in one of four states:

- `replacement-safe`
- `hybrid-only`
- `compression-only evidence`
- `keep mostly prose`

That is the point.

The loop is supposed to tell you when not to overclaim.
