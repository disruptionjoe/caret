# Immutable State

## Notation

```
^^^coordinator ^grip9
  ^rules
    ^read-only
  ^^worker ^autonomy7
    ^log
```

Protected files sit above. Agents work below. The coordinator enforces the boundary. Workers read protected state. Workers never modify it.

## What it does

Declares certain files as read-only to all agents. Not permission-based. Not soft. Hard walls. The files exist. Agents read them. Agents never change them.

Agents work around immutable state. They propose changes. They defer. They request human judgment. Or they create new files downstream. New data flows into new structures. Original structures stay clean.

## When to use it

When you need a stable reference layer that agents treat as law. Voice definitions. Persona files. Core configuration. Skill specifications. State representations. Anything where modification by an agent would corrupt the source of truth.

When you want agents creative within rails. Propose changes to you. Never sneak them in.

## When not to use it

When the file is genuinely mutable state: logs, caches, temp work, drafts. Those should live elsewhere and be managed normally.

When you want full agent autonomy in a subsystem. Don't protect it. Accept the risk.

## Design notes

This is a containment pattern. It forces separation: read layer and write layer. You read law. You write proposals. Law never gets corrupted by proposals.

Consider three layers:

1. **Law layer** (immutable). Personas, voice guides, skill specs. These define boundaries. Read-only.
2. **Working layer** (mutable). Drafts, proposals, observations, logs. Agents write here freely. Humans review.
3. **Archive layer** (immutable after closure). Completed work, decided items, historical record. Locked once done.

This three-layer structure prevents the working layer from accumulating junk and the law layer from drifting.

The trade-off is real. Immutable state costs agent speed. An agent cannot fix a broken index. Cannot update stale metadata. Must flag it, leave it, wait for the human. This friction is the feature, not the bug. You buy stability by accepting that agents move slower around protected boundaries.

The system that enforces immutability must resist social engineering. An agent cannot convince you to "temporarily" unlock a protected file for a "quick fix." Protected means protected. You unlock it with a separate, deliberate action.

The pattern scales because it is binary. A file is protected or it is not. No gradations. No "mostly protected." Agents understand walls. Agents don't understand "partially protected" — and neither do you after six months of context rot.

Relationship to **Safe Mutation**: opposite poles. Safe Mutation permits mutation with archive-and-draft safety nets. Immutable State forbids mutation entirely. Use Safe Mutation when some mutation is necessary but should be reversible. Use Immutable State when mutation should never happen.

Relationship to **Domain Anchor**: the anchor itself may be immutable — agents read the domain's purpose, voice, and rules, but only the human (or the evaluator within strict scope) modifies them.

Relationship to **Publication Gate**: the gate enforces a human checkpoint before anything goes external. Immutable State enforces a human checkpoint before anything gets modified internally. Both are containment, at different boundaries.
