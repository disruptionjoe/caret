# Caret-it Parity Skill (Development Tool)

This is an internal development and contributor tool for deep parity validation.

**Most users do not need this file.** The `Caret-it-skill.md` includes a built-in validation phase that handles prompt suite generation, parity checking, and iteration automatically.

This skill exists for:

- contributors validating changes to the Caret-it skill itself
- researchers running controlled parity experiments across large skill sets
- edge cases where someone wants to re-test an existing rewrite with a custom prompt suite

## When to Use This Instead of Caret-it

Use this skill only when:

- you already have a rewrite and want to test it independently of the compression process
- you need to run a larger or custom prompt suite beyond the 3-5 built into Caret-it
- you are comparing multiple rewrite variants against the same original
- you are contributing to the Caret repo and need to validate that changes to the Caret-it skill did not degrade output quality

For normal use — compressing a skill into Caret^ — just use `Caret-it-skill.md`. It handles everything.

## Purpose

Compression is easy to over-credit.

This skill exists to stop a rewrite from looking elegant while quietly dropping required behavior.

Use it after a Caret^ rewrite draft exists and you want deeper or independent validation beyond what the built-in Caret-it validation provides.

## What Counts As "Same"

The exact wording can change.

The behavioral contract should not drift without being named.

Check for parity across:

- required inputs
- required questions
- required commands or side effects
- required outputs or artifacts
- required safety and approval boundaries
- required logging and completion behavior

## Prompt Suite

Build a small representative prompt suite for the target skill.

Use 3 to 5 prompts:

1. one normal happy-path prompt
2. one edge or ambiguity prompt
3. one prompt that pressures safety, approval, or escalation
4. one prompt that pressures output format or artifact requirements
5. optional: one prompt that pressures a known weak spot

Keep the prompts concrete.
Do not test only the easy path.

## Loop

^intake original, rewrite, prompt suite

^harness-available
  ^execute original on suite
  ^execute rewrite on suite
^harness-available: else
  ^extract-contract original (asks, must-do, must-not-do, output)
  ^extract-contract rewrite (same)

^build parity-matrix
  ^scope: per-prompt
  ^classify (preserved, changed, lost, unresolved)

^classify-parity (pass | partial | fail | unverified)

^iterate ^cap3
  Gate: parity == pass → stop
  Gate: improvements-stalled → stop
  Gate: loop-count >= 3 → stop
  ^patch rewrite, re-compare

## Iteration Rules

Before starting Loop: identify shared-contract vs local-workflow layers. If the source bundles shared contract, report separation explicitly. Do not count shared-contract extraction as part of local compression gains.

Stop early if:
- the rewrite keeps dropping the same required behavior
- the source depends on too much literal contract to compact safely
- the gains are mostly token savings with no path to parity

Default cap: 3 iterations. Do not loop forever. That is a valid result — the right answer may be `keep mostly prose`.

## Static Comparison Rule

If no runnable harness exists, do not pretend the comparison was executed.

Call it:

- `executed parity` when both versions were actually run
- `inferred parity` when the comparison was static

Static comparison is still useful.
It is just weaker evidence.

## Required Output

^report
  ^section Prompt Suite
    List prompts used and why each exists.
  ^section Parity Matrix
    Per-prompt compare: original behavior | rewrite behavior | preserved | lost | unresolved
  ^section Iteration Log
    Per-iteration show: number | status | patch | rationale
  ^section Final Call
    Choose: `replacement-safe` | `hybrid-only` | `compression-only evidence` | `keep mostly prose`
  ^section Confidence Note
    Executed or inferred parity? If inferred, what still needs real execution?
