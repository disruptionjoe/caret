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

## Where Caret^ Usually Wins

Caret^ tends to pay off when the source file repeats operating mode over and over.

High-yield zones:

- repeated route logic
- repeated rule blocks
- repeated update or closeout steps
- handoff points
- gate decisions
- stance or pressure knobs that are currently described in prose
- repeated step framing inside complex orchestration files
- recurring analytic lenses that can cleanly map to hats

This is where the notation earns its keep.

## Where Prose Should Usually Stay

Some material should stay plain.

Keep prose when the source is carrying:

- nuanced explanation
- exceptions that need human judgment
- trust-boundary warnings
- example templates meant to stay literal
- concrete schemas, metadata fields, or destination tables that are already compact

Do not turn a good decision table into decorative notation.

## Shared Contract Gate

Some files bundle two layers together:

- a shared runtime contract
- a local workflow

Examples of shared contract material:

- standard preambles
- shared voice rules
- common telemetry or logging blocks
- universal AskUserQuestion formatting
- repeated contributor or escalation policy

If that shared layer appears to be repo-wide or tool-wide boilerplate:

- name it explicitly as shared contract
- do not pretend all of its removal is a local notation win
- evaluate the workflow layer separately from the contract layer

In many cases, the right rewrite is hybrid:

- inherit or reference the shared contract
- convert the local workflow spine

## Canon Alignment Gate

Some source files are not just verbose. They are stale.

If a file already contains Caret-like semantics, examples, or notation guidance that conflicts with current canon:

- stop treating it as a pure compression task
- normalize the semantics first
- then evaluate the rewrite

Examples:

- old meanings for `^^` and `^^^`
- deprecated dot-based forms
- examples that encode now-invalid worker behavior

If normalization is required, say so explicitly in the output. Do not count semantic repair as if it were only a notation win.

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
2. Check for canon conflicts or stale notation semantics.
3. Separate live instructions from explanatory or historical prose.
4. Mark each section as one of these before rewriting:
   - live signal layer
   - literal example or template
   - reference table or schema
   - explanatory prose
5. Extract the non-negotiables:
   - required constraints
   - safety rules
   - target files or handles
   - approval boundaries
   - reporting requirements
6. Run the five-lens review.
7. Rewrite the live instruction layer in Caret^ where it increases clarity or compression.
8. Keep supporting prose outside the notation when the prose carries real meaning.
9. Keep literal examples and templates inside fenced code blocks.
10. Preserve exact file references when precision matters.
11. Do not invent canonical syntax that the current Caret^ docs do not support.
12. If the user asked for an in-place rewrite, update the file. Otherwise, present a proposed rewrite.

## Rewrite Rules

- Do not force every sentence into Caret^.
- Do not force a full-file conversion if the right answer is hybrid.
- Do not invent targets that the source file never implied.
- Do not hide safety rules inside vague notation.
- Do not use named targets when the source clearly points to an exact file.
- Do not drop operational detail that a real harness or human still needs.
- Do not convert literal templates, example payloads, or sample headers into live notation.
- Do not mint one-off directives just because a heading exists. Use directives when they carry real operational signal.
- Do not treat semantic normalization as a pure compression win.
- Do not treat shared-contract extraction as if it were entirely local workflow compression.
- Do compress duplicated setup, repeated tone instructions, and stacked prose knobs when Caret^ can carry them directly.
- Do expect lower compression when the source is already dense with concrete file paths, metadata fields, and decision tables.
- Do expect strong compression in complex flow files if the rewrite keeps schemas and example payloads literal.
- Do use repo-relative paths, source URLs, or generic labels in public-facing reports instead of absolute local machine paths.
- Do avoid leaking local usernames, home directories, private workspace names, or machine-specific folder structure unless the task explicitly requires them.

## Directive Quality Bar

When you mint open-vocabulary directives in a rewrite, they should do at least one of these:

- collapse repeated operating language
- mark a reusable boundary or mode
- make sequence or precedence easier to see
- reduce repeated prose without hiding meaning

If a proposed directive does none of that, keep the heading or sentence in prose.

## Adoption Heuristic

Use compression as evidence, not as the only judge.

Working bands:

- `35%+` shorter and clearer: strong candidate for adoption
- `15-35%` shorter: usually a hybrid candidate
- under `15%` shorter: keep mostly prose unless clarity improves materially

These are heuristics, not law. Clarity still beats raw shrinkage.

## Required Output

Finish with these sections:

### Findings

Call out:

- what changed
- what stayed prose
- any unresolved harness assumptions
- whether canon normalization was required
- whether shared contract extraction was a major factor
- whether any source references were generalized for public-safe reporting

### Adoption Call

Choose one:

- `adopt`
- `hybrid`
- `keep mostly prose`

Explain the call in two or three sentences max.

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

## What The First Test Runs Showed

Early live runs showed the strongest gains in skills with repeated route logic, update rules, and closeout scaffolding.

They showed weaker gains in skills that were already operating as compact decision tables.

Use that pattern. Chase the live signal layer first.

Later rounds added two more lessons:

- complex orchestration files can still compress hard if schemas stay literal
- stale Caret semantics are a separate normalization problem, not just a rewrite opportunity

## Closing Line

End with a plain-language statement of value in this form:

```text
This rewrite is X% shorter. At roughly Y tokens saved per run, using it 1,000 times saves about Z tokens.
```

Keep it concrete. Make the gain easy to feel.
