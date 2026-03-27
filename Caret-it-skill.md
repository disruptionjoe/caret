# Caret-it Skill

Take a working skill or any instruction-heavy `.md` file.
Strip the drag.
Keep the force.
Rewrite it in Caret^ where Caret^ actually helps.

## Purpose

This skill converts verbose operational prose into a tighter Caret^ form without dropping the constraints that make the original useful.

It is built to run alongside an existing skill, prompt file, workflow doc, or other Markdown instruction artifact.

## What Good Looks Like

The rewritten file should be:

- shorter
- clearer about scope and boundaries
- cleaner about worker vs hat changes
- tighter about safety and trust assumptions
- easier to reuse across sessions

Not everything belongs in Caret^.

Keep explanatory prose when prose is doing real work. Convert the live signal layer. Do not flatten nuance just to chase compression.

## Five-Lens Review

Run the target through five lenses before rewriting:

1. `notation architect`
   Find what should become Caret^, what should stay prose, and where the original is smuggling semantics that belong in explicit notation.

2. `harness implementer`
   Catch hidden execution assumptions, unresolved targets, weak defaults, and instructions that only work in one local environment.

3. `security reviewer`
   Catch trust-boundary problems, ambiguous literal-vs-live text, and any place the rewrite could imply unsafe execution.

4. `edge-case tester`
   Catch scope ambiguity, Markdown traps, nesting confusion, blank-line drift, and worker-vs-hat mistakes.

5. `compression editor`
   Remove repetition, collapse obvious prose, and preserve only the words that still earn their tokens.

If the harness can spawn or simulate multiple perspectives cleanly, use that. If not, perform the same five-lens pass inside one worker. The review still stands.

## Rewrite Process

1. Read the full target file before rewriting anything.
2. Separate live instructions from explanatory or historical prose.
3. Extract the non-negotiables:
   - required constraints
   - safety rules
   - target files or handles
   - approval boundaries
   - reporting requirements
4. Run the five-lens review.
5. Rewrite the live instruction layer in Caret^ where it increases clarity or compression.
6. Keep supporting prose outside the notation when the prose carries real meaning.
7. Preserve exact file references when precision matters.
8. Do not invent canonical syntax that the current Caret^ docs do not support.
9. If the user asked for an in-place rewrite, update the file. Otherwise, present a proposed rewrite.

## Rewrite Rules

- Do not force every sentence into Caret^.
- Do not invent targets that the source file never implied.
- Do not hide safety rules inside vague notation.
- Do not use named targets when the source clearly points to an exact file.
- Do not drop operational detail that a real harness or human still needs.
- Do compress duplicated setup, repeated tone instructions, and stacked prose knobs when Caret^ can carry them directly.

## Required Output

Finish with these sections:

### Findings

Call out what changed, what stayed prose, and any unresolved harness assumptions.

### Caret^ Rewrite

Provide the rewritten version or the patch summary if you updated the file directly.

### Compression Report

Report:

- original token count
- rewritten token count
- tokens saved
- percentage shorter
- projected savings over 1,000 runs

Use the local harness tokenizer if one exists.

If no tokenizer is available, estimate tokens as:

```text
estimated_tokens = ceiling(character_count / 4)
```

Use this math:

```text
tokens_saved = original_tokens - rewritten_tokens
percentage_shorter = (tokens_saved / original_tokens) * 100
projected_1000_run_savings = tokens_saved * 1000
```

Round percentages to one decimal place unless the local harness has a stronger reporting standard.

### Example Compression

Show one short before-and-after excerpt that makes the savings visible.

Format:

```text
Before:
...

After:
...

Why it compresses:
...
```

### Log Note

Finish by using whatever logging or completion mechanism the local harness expects.

If the harness exposes a real log, archive, intake, or queue action, use it.

If it does not, add a brief plain-language completion note and stop. Do not invent side effects.

## Closing Line

End with a plain-language statement of value in this form:

```text
This rewrite is X% shorter. At roughly Y tokens saved per run, using it 1,000 times saves about Z tokens.
```

Keep it concrete. Make the gain easy to feel.
