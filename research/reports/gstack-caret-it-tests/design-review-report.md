# Gstack Caret-it Test: design-review

## Source

- repo: `https://github.com/garrytan/gstack`
- source file: `https://raw.githubusercontent.com/garrytan/gstack/main/design-review/SKILL.md`
- local copy: `raw/design-review-SKILL.md`
- rewrite: `design-review-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- This file is really two files fused together: a shared gstack runtime contract and a design-audit workflow.
- The highest-yield conversion is not total inline Caret. It is extracting the shared contract once, then converting the audit and fix loop.
- Literal command blocks, scoring tables, AI-slop blacklist rules, and output schemas still earn their place as literal surfaces.

## Adoption Call

`hybrid`

The skill-specific flow compresses well, but a pure rewrite would hide too much operational detail. The best move is shared-contract extraction plus a Caret^ spine for the audit phases.

## Compression Report

- original tokens: `14710`
- rewritten tokens: `773`
- tokens saved: `13937`
- percentage shorter: `94.7%`
- projected savings over 1,000 runs: `13937000`

## Example Compression

Before:

```text
## Phase 7: Triage
Sort all discovered findings by impact, then decide which to fix:

- High Impact
- Medium Impact
- Polish
```

After:

```text
^triage
Sort findings by impact:
- high impact
- medium impact
- polish
- deferred
```

Why it compresses:

The phase heading and prose scaffold collapse into one operating signal while the actual decision categories stay visible.

## Log Note

This report file is the completion record for the run.

This rewrite is 94.7% shorter. At roughly 13937 tokens saved per run, using it 1,000 times saves about 13937000 tokens.
