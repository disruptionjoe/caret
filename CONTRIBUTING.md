# Contributing to Caret^

Caret^ is a working project. The notation is stable. The Field Guide is growing. Patterns are being discovered. The architecture is evolving. Contributions are welcome.

---

## What We Accept

### Field Guide Terms

New terms for the glossary. Every term must earn its place.

- **Tool-neutral definition.** The term should work across ecosystems, not assume a particular framework.
- **Clear distinction from related terms.** If it's a synonym for something already documented, it doesn't belong.
- **Real-world scenario where this term matters.** Vague concepts don't help. Show us when someone would actually encounter this.
- **Not a synonym for something already documented.** Check CANON.md and FRAGMENTED.md first.

Submit via issue with title `[Field Guide] Term Name`.

### Definition Refinements

Improvements to existing glossary entries.

- Current definition and why it is incomplete or unclear
- Proposed revision
- Real-world example that illustrates the improvement

Submit via PR.

### Notation Changes

Changes to the symbol set, syntax rules, or parameter vocabulary. These go through review.

- What you are proposing
- Why existing notation does not cover it
- How it would look
- What problem it solves

High-stakes changes go to `notation/DECISIONS.md` for structured discussion before implementation. No surprises.

Submit via issue with title `[Notation] Description`.

### Architecture Patterns

New patterns for the patterns/ directory.

- Clear name
- Caret^ directive example (notation only)
- Plain-language explanation
- When to use it and when not to
- Real-world context (what problem does it solve?)

Submit via PR.

### Documentation & Examples

Clarity improvements, new examples, better explanations. Typos, broken links, confusing sections.

Submit via PR or issue.

---

## How to Contribute

1. **Check existing issues and PRs to avoid duplicates.**
2. **Open an issue for anything high-stakes** (notation, new terminology, major docs changes).
3. **Open a PR for additions, refinements, examples, corrections.**
4. **Follow the voice and style of the document you are editing.**
5. **Test examples.** Verify links. Run notation samples through SPEC.md rules.

---

## Standards

### Clarity > Cleverness

If it is clever but unclear, remove the cleverness. Precision matters more than wit.

### Simplicity > Completeness

A simple explanation that covers 80% of the problem is better than a complete explanation that few people understand.

### Practical > Theoretical

Terms, symbols, and patterns must connect to real situations. Abstract concepts need grounding in agent system work.

### Tool-Neutral

Definitions should not assume a specific platform or framework. If a concept is platform-specific, document it as such.

---

## The Project Is Still Evolving

The notation is stable. The Field Guide is incomplete. Patterns are being discovered. Architecture profiles (file-first vs. chat-safe vs. minimal) are still being defined.

If you find something that does not fit yet, open an issue. That is how we discover missing categories.

---

## Voice & Style

Match the document you are editing. Three tiers:

- **Notation/Reference docs:** low temperature. Exact, restrained, minimal attitude. Precision over performance.
- **README / Field Guide:** mid temperature. Opinionated, stylized, grounded. More personality, still technically exact.
- **Examples:** plain language alongside notation. Show both. Make the translation visible.

Avoid:

- Exclamation marks (except rare emphasis)
- Corporate reassurance or fake friendliness
- Startup fluff or hype language
- Jargon without explanation
- "We," "our community," "exciting"

---

## Questions?

Open an issue. If your contribution is constructive and practical, you are in the right place.
