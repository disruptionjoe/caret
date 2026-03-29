# Live Registry

## Notation

```
^^^coordinator ^grip9
  ^registry
  ^audit
```

The coordinator maintains a registry of what exists. The audit verifies the registry matches reality.

## What it does

Keeps a single, authoritative list of what the system actually contains — domains, agents, skills, voices, queues — and ensures that list stays synchronized with reality.

Registries rot. A skill gets deleted but stays in the registry. A domain gets renamed but the registry still points to the old name. An agent gets created ad hoc but never registered. Over time, the registry becomes fiction. Agents consulting it make decisions based on a system that no longer exists.

The live registry pattern combats this by treating the registry as a living document that is verified, not just maintained.

## When to use it

When the system has enough moving parts that no single agent can hold the full inventory in context.

Specific triggers:

- An agent tried to route to a skill that no longer exists
- A coordinator made a delegation decision based on stale capability information
- Someone asked "what domains do we have?" and the answer required checking multiple files
- New components were created but never registered, leading to orphaned work
- The registry disagrees with the filesystem

## When not to use it

Small systems. If you have three skills and two domains, a registry is overhead. You can list them in a single file or hold them in your head. The pattern is for systems where the inventory exceeds easy recall.

Also wrong when the system is entirely static. If nothing gets added, removed, or renamed, the registry does not need to be live. A snapshot is fine. The live pattern exists because systems change.

## Design notes

The core trade-off is accuracy versus maintenance cost. A perfectly accurate registry requires verification on every change. A low-maintenance registry drifts. The pattern leans toward periodic verification rather than continuous synchronization.

**Registry scope.** Decide what gets registered. Not everything. Domains, yes. Active skills, yes. Every temporary file the night factory creates, no. The registry tracks components that other components need to discover. If nothing else needs to know about it, it does not need a registry entry.

**Verification cadence.** The registry should be audited on a regular cycle. The overnight factory evaluator is a natural place for this: once per cycle, compare the registry against the filesystem. Flag discrepancies. Do not auto-correct — flag. Auto-correction can mask structural problems.

**Discovery versus declaration.** Two approaches to keeping the registry current. Declaration: every time a component is created, it must register itself. Discovery: a periodic scan finds what exists and updates the registry. Declaration is more accurate but requires discipline. Discovery is more resilient but introduces lag. Most practical systems use both: declare on creation, discover on audit.

**The registry is not the source of truth for behavior.** The registry says what exists. The charter, rules, and configuration files say how it behaves. An agent reads the registry to know "there is a domain called Caret^." It reads the domain anchor to know what Caret^ is and how to work in it.

**Stale entries are worse than missing entries.** A missing entry means the system does not know about a component. It will be discovered. A stale entry means the system thinks something exists that does not. Agents will try to route to it, load it, or delegate to it — and fail. Aggressive pruning of stale entries is more important than aggressive registration of new ones.

Relationship to **Domain Anchor**: domains are the primary registrants. The registry lists them. The domain anchor defines them.

Relationship to **Overnight Factory**: the factory is the natural verification engine. Each run can include a registry audit step.

Relationship to **Voice Follows Domain**: voice routing depends on the registry. If the registry says "Caret^ domain uses Caret^ voice," a stale registry entry can cause voice mismatches.

Relationship to **Source of Truth Hierarchy**: the registry is an operational reference, not a governance document. It sits below the charter in authority. It describes what is, not what should be.
