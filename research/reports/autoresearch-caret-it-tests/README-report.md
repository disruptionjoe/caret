# `README.md` Caret-it Report

## Findings

- This file is not a true skill. It is a public explainer with one operator-facing section embedded inside it.
- The strongest Caret^ target is the "Running the agent" handoff. The rest of the file mostly earns its prose.
- The README carries repository story, quick-start setup, design rationale, and platform notes. Those are public-facing narrative surfaces, not live signal layers.
- No canon normalization was required. The file does not encode stale Caret semantics.
- Shared-contract extraction was not the main issue. The boundary is audience and function, not a repeated repo-wide preamble.

## Adoption Call

`keep mostly prose`

The README should stay public and readable first. The right move is a small hybrid tightening around the operator handoff, not a full Caret^ conversion.

## Caret^ Rewrite

See `README-rewrite.md` for the suggested hybrid excerpt.

## Compression Report

- Original token count: `2033`
- Rewritten token count: `241`
- Tokens saved: `1792`
- Percentage shorter: `88.1%`
- Projected savings over 1,000 runs: `1792000`

Token counts use the fallback estimator `ceiling(character_count / 4)`.

Important caveat:

That raw shrinkage is not a real adoption signal for this file. It mostly reflects that the rewrite keeps only the operator-facing section and deliberately drops the public explanatory work the README is supposed to do.

## Example Compression

```text
Before:
Simply spin up your Claude/Codex or whatever you want in this repo (and disable all permissions), then you can prompt something like:

Hi have a look at program.md and let's kick off a new experiment! let's do the setup first.

After:
Load `program.md` as the live operator surface.
Baseline first.
Then iterate autonomously until interrupted.

Why it compresses:
The operator handoff is a real signal layer, so Caret-style tightening helps there. The broader README still needs prose around it.
```

## Log Note

Completed as a boundary-case research report.

No README in the source repo was modified.
