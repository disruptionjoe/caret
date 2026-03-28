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
- Under the new parity gate, the current rewrite is not a drop-in replacement. It preserves the workflow spine, but it only references the shared contract and the exact audit surfaces instead of carrying them forward as executable skill content.

## Adoption Call

`hybrid`

The skill-specific flow still looks like a strong Caret^ candidate, but this exact rewrite is not behaviorally equivalent yet. Treat it as evidence for a future hybrid extraction, not as a replacement skill.

## Behavioral Parity

- parity status: `partial`
- parity basis: `inferred via static contract comparison`
- comparison scope:
  - shared gstack runtime contract
  - setup and bootstrap behavior
  - audit phases
  - fix loop
  - required outputs
  - logging and completion behavior
- preserved:
  - the main audit sequence
  - triage and fix-loop structure
  - the need to keep literal scoring and report surfaces
- lost or unresolved:
  - exact gstack preamble behavior
  - one-time proactive and telemetry prompts
  - exact bootstrap commands and install flow
  - output JSON schema and output path contract
  - hard-rule corpus and scoring tables
  - completion protocol details

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
