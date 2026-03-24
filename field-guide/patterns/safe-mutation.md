# Safe Mutation

## Notation

```
work-item-draft -> [human review] -> work-item (final)
existing-file -> data/archive/{timestamp}-{name} -> [modify original]
```

Provisional or reversible. Never both dangerous and irreversible.

## What it does

Permits agent mutation of state through two mechanisms: (1) Draft-then-promote — new work gets a `-draft` suffix until human approval, making all agent output provisional until acceptance. (2) Archive-before-modify — existing files are copied to data/archive/ before any modification, making all changes reversible. Together they form a pattern: agents can mutate state freely because every mutation is either provisional or reversible.

## When to use it

Any system where agents generate or modify content at scale. Night factory work. Content generation. Configuration changes. Anything that will have human review later. Draft and archive together remove the need for pre-flight human approval. Work flows faster because humans review output, not input.

## When not to use it

Protected state. Immutable files. Append-only logs. Anything that must never be mutated. In those cases, mutation is not safe, so it is forbidden. Use Immutable State pattern instead. Do not force Safe Mutation onto systems that require safety-through-prohibition.

## Design notes

Draft suffix is a naming convention that encodes approval status. It is not metadata. It is not a database field. It is a filename property. The convention is scannable by humans and machines. A file named `pattern-proposal-draft.md` is understood instantly: proposal exists, not yet approved. A file named `pattern-proposal.md` is understood instantly: approved, final, part of the system.

The draft-to-final promotion is a human action, not automatic. The human reviews the draft and either approves (rename, remove `-draft` suffix) or rejects (delete). This is the gate. It is simple and unambiguous. No approval workflows. No state tables. Just: does the draft meet the standard for final? Yes, promote it. No, delete it.

The archive directory is append-only backup. When an existing file is modified, the previous version is copied to data/archive/{timestamp}-{name}. Timestamp format is ISO 8601 for sortability. The original file is then modified. If the modification was wrong, the archive has the previous version. If the modification was disastrous, all previous versions are in archive. No deletion, no overwrite. Archive captures the full lineage.

Together, draft-then-promote and archive-before-modify mean that agents can work without requesting permission for every mutation. They work. Humans review after. This is faster and scales. The tradeoff is that humans must review. If review is not happening, this pattern fails. If review is not happening, you have a different problem.

Risk: agents can accumulate draft files faster than humans can review them. The draft queue becomes a backlog. Set a promotion SLA. If a draft sits for N days, it gets auto-deleted or auto-promoted depending on policy. Document the SLA. Enforce it. Otherwise drafts fossilize and become invisible.

Risk: archive directory grows without bound. Implement retention policy. Archive entries older than N months get deleted. Quarterly archive purge is reasonable. Document it. Run it on schedule. Otherwise you are running a museum, not a system.

Risk: archive naming collision if two modifications happen in the same second. Unlikely but possible at scale. Use {timestamp}-{hash} format if collision risk is real. Hash the original file content or path. One collision per billion is acceptable. Document the collision handling.

Design consequence: this pattern treats humans as the approval layer, not the work layer. Agents work. Humans decide. This inverts the traditional approval-then-work flow. It is faster but requires human discipline. If the humans are not reviewing, the system corrupts.

Related: Disposition Gate is the entry point for new work. Immutable State is the inverse: when mutation is not safe, forbid it. Append-Only Log is the extreme case: mutation is forbidden entirely, logs only.
