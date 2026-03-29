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

1. Read the original skill in full.
2. Read the Caret^ rewrite in full.
3. Build the prompt suite.
4. Run the original skill on the prompt suite if a real harness is available.
5. If no harness is available, extract the contract statically:
   - what it asks
   - what it must do
   - what it must not do
   - what it must output
6. Run the rewrite on the same prompt suite, or compare it statically if execution is unavailable.
7. Build a parity matrix:
   - preserved
   - changed
   - lost
   - unresolved
8. Classify parity:
   - `pass`
   - `partial`
   - `fail`
   - `unverified`
9. If parity is not good enough, patch the rewrite.
10. Repeat until:
   - parity passes
   - improvements stop being general
   - or the iteration cap is reached

## Iteration Rules

Default cap: 3 rewrite iterations after the first draft.

Do not loop forever.

Stop early if:

- the rewrite keeps dropping the same required behavior
- the source depends on too much literal contract to compact safely
- the gains are mostly token savings with no path to parity

That is a valid result.
The right answer may be `keep mostly prose`.

## Static Comparison Rule

If no runnable harness exists, do not pretend the comparison was executed.

Call it:

- `executed parity` when both versions were actually run
- `inferred parity` when the comparison was static

Static comparison is still useful.
It is just weaker evidence.

## Required Output

Finish with these sections:

### Prompt Suite

List the prompts used and why each one exists.

### Parity Matrix

For each prompt, compare:

- original behavior
- rewrite behavior
- preserved behaviors
- lost behaviors
- unresolved behaviors

### Iteration Log

Show:

- iteration number
- parity status
- what was patched
- why the patch mattered

### Final Call

Choose one:

- `replacement-safe`
- `hybrid-only`
- `compression-only evidence`
- `keep mostly prose`

### Confidence Note

Say whether parity was executed or inferred.

If inferred, say what would still need real execution to be sure.
