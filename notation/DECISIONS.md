# Notation Decisions

## 2026-03-26

### D001: Portable Artifact First

`/caret-cheatsheet.md` is the product artifact. The notation directory exists to clarify and support it.

### D002: Four-Form Core

The canonical core stays:

- `^` directive
- `^^` change the hat, not the worker
- `^^^` change the worker
- `^^^^` fresh-eyes boundary

### D003: Open Vocabulary, Fixed Structure

Caret^ keeps a fixed structural model and an open directive vocabulary.

### D004: Scalar Convention

The canonical scalar convention is `0-9`, with omitted level meaning normal behavior.

### D005: Scalar Alias Rule

One-letter aliases are reserved for scalars. Operational directives spell out.

### D006: Target Syntax

Canonical target syntax uses:

- commas for multiple targets
- colon for binding
- bare numbers after `^^` or `^^^` for count form
- exact repo-relative handles when precision matters

### D007: Scope Rule

`^^` and `^^^` close by outdent. `^^^^` is the only explicit paired boundary in the core notation.

### D008: Markdown Relationship

Markdown containers help organize documents, but they are not hidden Caret^ delimiters.

### D009: Literal Example Rule

Inside fenced code blocks, Caret^ is example text, not live instruction.

### D010: Contract And Security Placement

Interpretation behavior and trust boundaries belong in canonical notation docs, not in patterns or scattered examples.

### D011: Repo-Wide Review Trigger

When the cheatsheet changes, every notation-bearing doc, example, and pattern in the repo must be re-reviewed.

### D012: Repo Supremacy

The live repo canon outranks external repos, research artifacts, examples, patterns, drafts, and archived material.

Those sources may inform changes. They do not override current canon unless canon is deliberately updated.
