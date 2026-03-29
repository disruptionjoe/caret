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

## Full Process

The skill runs in three phases: Analyze, Rewrite, and Validate. All three happen in a single invocation.

### Phase 1: Analyze

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
7. Build a behavioral contract from the source (used in Phase 3):
   - required inputs or questions the skill must ask
   - required outputs, files, or report sections it must produce
   - required commands or side effects it must execute
   - required safety and approval boundaries it must enforce
   - required logging or completion behavior

### Phase 2: Rewrite

8. Rewrite the live instruction layer in Caret^ where it increases clarity or compression.
9. Keep supporting prose outside the notation when the prose carries real meaning.
10. Keep literal examples and templates inside fenced code blocks.
11. Preserve exact file references when precision matters.
12. Do not invent canonical syntax that the current Caret^ docs do not support.
13. If the user asked for an in-place rewrite, hold the update until Phase 3 passes.

### Phase 3: Validate

This phase replaces the need for any external parity skill. The validation is built in.

14. Generate a prompt suite from the source file. Build 3 to 5 concrete prompts:
    - one normal happy-path prompt
    - one edge or ambiguity prompt
    - one prompt that pressures safety, approval, or escalation
    - one prompt that pressures output format or artifact requirements
    - optional: one prompt that targets a known weak spot

    The prompts must be specific to the skill being rewritten, not generic. Derive them from the behavioral contract extracted in step 7.

15. Compare the original and rewrite against each prompt:
    - What does the original require for this prompt?
    - Does the rewrite preserve that requirement?
    - Is anything lost, changed, or ambiguous?

16. Build a parity matrix for each prompt:
    - preserved behaviors
    - changed behaviors
    - lost behaviors
    - unresolved behaviors

17. Classify overall parity:
    - `pass` — all required behaviors preserved
    - `partial` — some behaviors lost or ambiguous
    - `fail` — critical behaviors missing
    - `unverified` — comparison could not be completed

18. If parity is `partial`, patch the rewrite and re-compare. Iterate up to 2 additional times.

19. Stop iterating if:
    - parity reaches `pass`
    - the same behavior keeps getting dropped (the source may resist compression there)
    - gains are mostly token savings with no path to full parity

20. If no runnable harness is available, do a static contract comparison and mark parity as `inferred` rather than `executed`. Static comparison is still useful — it is just weaker evidence.

21. If the user asked for an in-place rewrite and parity is `pass`, apply the update now. If parity is `partial` or worse, present the rewrite as a proposal with the parity findings attached.

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

Finish with these sections:

### Findings

Call out:

- what changed
- what stayed prose
- any unresolved harness assumptions
- whether canon normalization was required
- whether shared contract extraction was a major factor
- whether any source references were generalized for public-safe reporting

### Prompt Suite

List the prompts generated for validation and why each one exists.

### Parity Matrix

For each prompt, show:

- original behavior
- rewrite behavior
- preserved / changed / lost / unresolved

### Iteration Log

If patches were needed, show:

- iteration number
- what was patched
- why the patch mattered
- parity status after patch

If the rewrite passed on first comparison, say so.

### Adoption Call

Choose one:

- `adopt`
- `hybrid`
- `keep mostly prose`

Explain the call in two or three sentences max.

### Behavioral Parity

Report:

- parity status (`pass`, `partial`, `fail`, `unverified`)
- whether parity was executed or inferred
- if inferred, what would need real execution to be sure
- number of iterations used
