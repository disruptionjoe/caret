# Caret-it Parity Loop Workflow

This workflow is general.

It applies to any skill or instruction-heavy Markdown file, not just GStack.

## Goal

Run the original and the Caret^ rewrite against the same contract surface.
Patch the rewrite.
Repeat until parity passes or the rewrite clearly stops being worth it.

## Inputs

- one original skill or instruction file
- one Caret^ rewrite draft
- one prompt suite

## Prompt Suite Rules

Use 3 to 5 prompts.

The suite should cover:

- normal use
- edge or ambiguity
- safety or approval pressure
- output-format pressure
- optional: one known difficult case

## Per-Iteration Procedure

1. Read the original file.
2. Read the rewrite.
3. Build or refine the prompt suite.
4. Extract the behavioral contract:
   - inputs
   - questions
   - side effects
   - outputs
   - boundaries
   - logging
5. Compare original and rewrite on the same suite.
6. Mark each comparison:
   - preserved
   - changed
   - lost
   - unresolved
7. Assign parity status:
   - `pass`
   - `partial`
   - `fail`
   - `unverified`
8. Patch the rewrite if the lesson is general.
9. Repeat.

## Evidence Modes

### Executed parity

Use this when both versions can actually be run in a real harness.

### Inferred parity

Use this when the comparison is static and contract-based.

This is weaker evidence.
Say so plainly.

## Stop Rules

Stop when one of these is true:

- parity reaches `pass`
- the rewrite remains `partial` but is still useful as a hybrid
- the rewrite fails parity on critical behaviors
- repeated patches only recover literal contract by reintroducing prose
- iteration cap is reached

Default cap: 3 rewrite iterations after the first draft.

## Final Output

Produce:

- prompt suite
- parity matrix
- iteration log
- final call
- confidence note

## Final Call Meanings

`replacement-safe`
- the rewrite preserves the needed behavior closely enough to replace the original

`hybrid-only`
- the rewrite helps, but only if important literal surfaces remain intact

`compression-only evidence`
- the rewrite proves token drag exists, but not that the rewrite is safe to replace with

`keep mostly prose`
- the source resists safe compaction
