# Safe Mutation

## Notation

```
^^^worker ^autonomy7
  ^archive
  ^log
```

New work gets a `-draft` suffix. Existing files get archived before modification. Provisional or reversible. Never both dangerous and irreversible. The notation shows archival and logging; the draft-naming convention, archive format, and promotion workflow are implementation contracts defined in the prose below.

## What it does

Permits agent mutation of state without pre-flight approval. Two mechanisms:

1. **Draft-then-promote**: New work gets a `-draft` suffix. It is provisional, not live. The human reviews it. Approves (rename, remove `-draft`) or rejects (delete). Only approved work is final.

2. **Archive-before-modify**: Before modifying an existing file, copy it to `archive/ {timestamp}-{name}`. The original is then modified. All previous versions are in archive, immutable, sortable by timestamp. Rollback is one copy command.

Together: agents can mutate state freely. Every mutation is either provisional (not yet approved) or reversible (previous version archived).

## When to use it

Any system where agents generate or modify content at scale. Night factories. Skill generation. Configuration changes. Anything that will be human-reviewed later. Draft and archive remove the need for pre-flight approval. Work flows faster. Humans review output, not input.

This pattern trades ceremony for speed. You get faster iteration. You pay for mandatory review.

## When not to use it

Protected state. Immutable files. Append-only logs. Anything that must never be mutated. In those cases, mutation is not safe, so it is forbidden. Use Immutable State pattern instead.

Do not force Safe Mutation onto systems that require safety-through-prohibition. It will fail.

## Design notes

The draft suffix is a naming convention, not metadata. It is not a database field. It is not a flag. It is a filename property. Scannable by humans and machines. `pattern-draft.md` is instantly understood: proposal, not approved. `pattern.md` is instantly understood: approved, final, canonical.

The promotion from `-draft` to final is a human action. Not automatic. Not time-based. The human reviews and decides: does this meet the standard? Yes, promote. No, delete. Simple. Unambiguous. No approval workflows. No state tables.

The archive directory is append-only backup. When an existing file is modified, its previous version is copied to `archive/{timestamp}-{name}`. Timestamp is ISO 8601 for sortability. The original is then modified. If the modification was wrong, the archive has it. If the modification was catastrophic, all previous versions are in archive. No deletion. No overwrite. Archive captures full lineage.

Together, draft-then-promote and archive-before-modify mean agents work without requesting permission for every mutation. They work. Humans review after. This is faster and scales better than pre-approval loops. The trade-off: humans must review. If review is not happening, this pattern fails. If review is not happening, you have a different problem.

Risk: agents accumulate drafts faster than humans can review. The draft queue becomes invisible and fossilizes. Set a promotion SLA. If a draft sits N days, it gets auto-deleted or auto-promoted by policy. Document the SLA. Enforce it. Otherwise drafts become debt.

Risk: archive grows without bound. Implement retention policy. Archive entries older than N months get deleted. Quarterly archive purge is reasonable. Document it. Run it on schedule. Otherwise you are running a museum.

Risk: archive naming collision if two modifications happen in the same second. Unlikely at normal scale. Use `{timestamp}-{content-hash}` format if collision risk is real. Hash the original file content or path. Acceptable collision rate: one per billion.

Design consequence: this pattern treats humans as the approval layer, not the work layer. Agents work. Humans decide. This inverts the traditional pre-approval flow. It is faster but demands human discipline. If humans are not reviewing, the system corrupts.

Relationship to **Gated Pipeline**: the pipeline gates are quality checkpoints within a single artifact's journey. Safe Mutation is the approval mechanism for independent work artifacts. The pipeline controls sequence. Safe Mutation controls provisioning and reversibility.

Relationship to **Async Handoff**: the handoff compiles work into a summary and waits for human decision. Safe Mutation allows agents to work without waiting. The human reviews drafts asynchronously. Handoff is synchronous (compile → human decides → resume). Safe Mutation is asynchronous (work → draft → human reviews whenever).

Relationship to **Append-Only Log**: this pattern permits mutation. Append-Only forbids it entirely. Use Safe Mutation when some mutation is necessary but should be reversible. Use Append-Only when mutation should never happen.
