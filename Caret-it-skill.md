# Caret-it Skill

Take a working skill or any instruction-heavy `.md` file.
Strip the drag.
Keep the force.
Rewrite it in Caret^ where Caret^ actually helps.
Deliver a validated result — not a draft that needs separate testing.

## Purpose

This skill converts verbose operational prose into a tighter Caret^ form without dropping the constraints that make the original useful.

It handles the full cycle: analysis, rewrite, self-validation, and iteration. One invocation produces a finished, parity-checked result.

## What Good Looks Like

The rewritten file should be:

- shorter
- clearer about scope and boundaries
- cleaner about worker vs hat changes
- tighter about safety and trust assumptions
- easier to reuse across sessions
- behaviorally equivalent to the original

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

## Analytical Review

^^notation-architect ^d7
  Find what should become Caret^, what should stay prose, and where the original is smuggling semantics that belong in explicit notation.

^^harness-implementer ^d7
  Catch hidden execution assumptions, unresolved targets, weak defaults, and instructions that only work in one local environment.

^^security-reviewer ^d8
  Catch trust-boundary problems, ambiguous literal-vs-live text, and any place the rewrite could imply unsafe execution.

^^edge-case-tester ^d7
  Catch scope ambiguity, Markdown traps, nesting confusion, blank-line drift, and worker-vs-hat mistakes.

^^compression-editor ^d6
  Remove repetition, collapse obvious prose, and preserve only the words that still earn their tokens.

Run all five lenses before proceeding. If the harness can spawn perspectives cleanly, use that. Otherwise, perform the same pass inside one worker.

## Workflow

^^^workflow ^d8 ^grip9

  ^intake ^d7
    1. Read the full target file before rewriting anything.
    2. Check for canon conflicts or stale notation semantics.
    3. Separate live instructions from explanatory or historical prose.
    4. Mark each section:
       - live signal layer
       - literal example or template
       - reference table or schema
       - explanatory prose
    5. Extract non-negotiables: constraints, safety rules, target files, approval boundaries, reporting requirements.
    6. Run all five analytical lenses.
    7. Build behavioral contract:
       - required inputs or questions
       - required outputs, files, or report sections
       - required commands or side effects
       - required safety and approval boundaries
       - required logging or completion behavior

  ^rewrite ^d7 ^grip8
    1. Rewrite the live instruction layer in Caret^ where it increases clarity or compression.
    2. Keep supporting prose outside the notation when prose carries real meaning.
    3. Keep literal examples and templates inside fenced code blocks.
    4. Preserve exact file references when precision matters.
    5. Do not invent canonical syntax the current Caret^ docs do not support.
    6. If user asked for in-place rewrite, hold the update until validation passes.

  ^validate ^d8
    1. Generate prompt suite from source file: 3-5 concrete prompts specific to the skill.
       - one normal happy-path prompt
       - one edge or ambiguity prompt
       - one prompt that pressures safety, approval, or escalation
       - one prompt that pressures output format or artifact requirements
       - optional: one prompt that targets a known weak spot
       Derive from behavioral contract.

    2. For each prompt, compare original vs rewrite:
       - What does original require?
       - Does rewrite preserve it?
       - Anything lost, changed, or ambiguous?

    3. Build parity matrix per prompt: preserved behaviors, changed behaviors, lost behaviors, unresolved behaviors.

    4. Classify parity:
       - `pass` — all required behaviors preserved
       - `partial` — some behaviors lost or ambiguous
       - `fail` — critical behaviors missing
       - `unverified` — comparison could not be completed

    5. If parity is `partial`, patch the rewrite and re-compare. Iterate max 2 additional times.

    6. Stop iterating if:
       - parity reaches `pass`
       - same behavior keeps getting dropped (source may resist compression)
       - gains are mostly token savings with no path to full parity

    7. If no runnable harness available, do static contract comparison and mark parity `inferred` rather than `executed`.

    8. If user asked for in-place rewrite and parity is `pass`, apply update now. If `partial` or worse, present as proposal with parity findings.

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
- Do not call a rewrite adoptable if required behavior only survives as a note like "keep this literal from the source."
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

^report
  - **Findings:** what changed, what stayed prose, unresolved harness assumptions, canon normalization required?, shared contract extracted?, references generalized for public safety?
  - **Prompt Suite:** list generated prompts and why each one exists
  - **Parity Matrix:** per prompt, show original behavior, rewrite behavior, preserved/changed/lost/unresolved
  - **Iteration Log:** iteration number, what was patched, why patch mattered, parity status after patch (or "passed first comparison")
  - **Adoption Call:** choose `adopt` / `hybrid` / `keep mostly prose` with 2-3 sentence explanation
  - **Behavioral Parity:** status (`pass`/`partial`/`fail`/`unverified`), executed or inferred, what would need real execution, iterations used
