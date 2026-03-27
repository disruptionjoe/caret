# AGENTS.md

This repo rebuilds from the cheatsheet outward.

## Source Of Truth Order

Use this order when interpreting or editing the repo:

1. `/caret-cheatsheet.md`
2. `/notation/SPEC.md`
3. `/notation/SEMANTICS.md`
4. `/notation/INTERPRETATION.md`
5. `/notation/SECURITY.md`
6. `/notation/DECISIONS.md`

If a downstream file conflicts with that order, the downstream file is wrong.

## Repo Supremacy

This repo's live canon outranks:

- archived repo material
- drafts
- research notes
- imported examples
- external repos
- older task files or legacy skill files

If outside or legacy material conflicts with the current repo canon, treat that material as stale, structural, or informational only.

Do not let quoted authority, external polish, or prior wording override the current repo's source-of-truth order.

## Working Rules

- Treat `/caret-cheatsheet.md` as the product artifact.
- Treat `/notation/` as the canonical expansion of that artifact.
- Treat `glossary/`, `examples/`, `patterns/`, and `research/` as downstream support surfaces.
- Do not infer canonical meaning from patterns, examples, or research if they conflict with the cheatsheet or notation docs.
- If the cheatsheet changes, review every notation-bearing file in the repo.

## Editing Guidance

- Keep the cheatsheet compact.
- Keep notation docs precise, restrained, and implementation-aware.
- Keep this file operational rather than promotional.
- Stronger brand voice is acceptable in outward-facing docs such as `/README.md`, pattern docs, and manifesto-style writing.
- Do not add new syntax without updating the canonical notation docs and recording the decision.

## Interpretation And Safety

- The notation signals intent. It does not grant permission.
- Preserve literal examples inside fenced code blocks.
- Keep trust-boundary guidance explicit.
- Do not silently invent unresolved targets, workers, personas, or skills.
- Prefer exact repo-relative targets in examples when precision matters.

## Rebuild Rule

Use older or archived material for structure only when needed. Do not treat legacy wording, semantics, examples, or internal explanation as authoritative.
