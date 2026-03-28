# Caret-it Optimization Workflow

This workflow exists to keep `Caret-it-skill.md` from getting trapped in a local minimum.

One pass can make it tighter.
Multiple rounds show where it breaks, where it over-converts, and where the best model is actually hybrid.

## Goal

Stress the conversion skill across different source shapes, extract repeatable patterns, and converge on a stronger rewrite model.

## Round Structure

Each round should mix files with different failure modes.

Use three file shapes per round:

- one file where Caret^ should compress aggressively
- one file where the right answer is hybrid
- one file that pressures a boundary: stale semantics, dense tables, literal templates, or heavy implementation detail

## Per-File Procedure

1. Read the full source file.
2. Classify each section:
   - live signal layer
   - explanatory prose
   - literal example or template
   - reference table or schema
3. Run the five-lens review from `Caret-it-skill.md`.
4. Draft the Caret^ rewrite.
5. Build a behavioral parity checklist or prompt set:
   - required inputs or questions
   - required outputs or artifacts
   - required commands or side effects
   - approval and safety boundaries
   - logging or completion behavior
6. Compare original and rewritten behavior:
   - execute both on the same prompt set when a real harness is available
   - otherwise do a static contract comparison and mark it as inferred
7. Record a parity status:
   - `pass`
   - `partial`
   - `fail`
   - `unverified`
8. Compute token counts:
   - use the local harness tokenizer if available
   - otherwise use `ceiling(character_count / 4)`
9. Make an adoption call:
   - `adopt`
   - `hybrid`
   - `keep mostly prose`
10. Record:
   - what compressed well
   - what stayed prose
   - what broke or resisted compression
   - what parity preserved
   - what parity lost
   - unresolved harness assumptions

## Between-Round Synthesis

After each round:

1. Identify the strongest positive pattern.
2. Identify the strongest failure mode.
3. Patch `Caret-it-skill.md` only if the lesson is general, not file-specific.
4. Keep patches small. One round should not cause a full rewrite of the skill itself.

## Suggested Round Mix

Round 1: baseline operational skills

- route-heavy
- rule-heavy
- closeout-heavy

Round 2: diagnostic and decision skills

- multi-lens reasoning
- scoring frameworks
- complex start-of-day flows

Round 3: boundary and adversarial files

- infrastructure sync logic
- stale semantics
- canonical mismatch

## Convergence Test

The workflow is converging when these conditions hold:

- adoption calls stop swinging wildly between rounds
- the skill gets better at spotting hybrid cases early
- literal templates stay literal
- stale semantics trigger normalization instead of blind conversion
- compression improves without hiding meaning
- parity failures become easier to predict before a rewrite is proposed

## Output Bundle

Each optimization run should produce:

- one workflow file
- one summary index
- one round summary per round
- per-file reports
- per-file rewrites when a rewrite is actually appropriate
- one parity matrix showing which rewrites are safe replacements versus compression-only evidence

The point is not just better rewrites.

The point is a better decision rule for when to rewrite at all.
