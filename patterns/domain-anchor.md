# Domain Anchor

## Notation

```
^^^domain ^grip9
  ^voice
  ^goals
  ^log
  ^rules
```

## What it does

Defines a persistent unit of coherence that agents enter, inherit, and leave unchanged. A domain has a purpose, a voice, active goals, a log, and standing rules. Any agent working in this domain reads the anchor first and inherits all of it — perspective, constraints, history — without negotiation.

The anchor is not a worker. It is a context package. Agents come and go. The anchor stays. Purpose filters what belongs. Voice constrains how it sounds. Goals define what to work on. The log is memory. Rules are scar tissue from past mistakes.

## When to use it

Multiple agents will touch the same body of work over time. The work has its own identity — a distinct voice, a set of goals, constraints that don't apply elsewhere. Without an anchor, every entering agent re-derives context from files, guesses the voice, and produces output that may not cohere with what came before.

Specific triggers:

- Cross-session work that needs continuity without shared context windows
- Distinct voice requirements that agents routinely violate
- Queue-based systems (like the Overnight Factory) that need to know what to work on and how
- You've caught voice bleed, scope confusion, or repeated context-gathering across sessions

## When not to use it

One-shot tasks. A single agent handles it in one session and nothing picks up afterward. Setting up an anchor for that is overhead that buys nothing.

Also wrong for genuinely cross-domain work that resists classification. Some tasks serve multiple purposes and multiple voices. Forcing them into one domain creates artificial constraints. Handle those at the orchestrator level.

If the domain has fewer than two goals, it might be a project, not a domain. Projects live inside domains. A domain with one project is a project that got over-promoted.

## Design notes

The triple-caret (`^^^domain`) declares a persistent, anchored structure. It survives across sessions. It accumulates. Domains remember.

The single-caret components (`^voice`, `^goals`, `^log`, `^rules`) are structural declarations the anchor carries. The notation makes the domain's anatomy scannable at a glance. You read the block and know exactly what context an agent will load when it enters.

**Purpose as a filter.** Purpose is not decorative. It is the filter that prevents scope creep. An evaluator checking whether to queue a task asks: does this serve the domain's purpose? A domain with a vague purpose ("do good work") filters nothing. A domain with a sharp purpose ("get Joe income") filters ruthlessly. Sharpness of purpose determines coherence of the domain.

**Voice as a property of the domain, not the agent.** In naive multi-agent systems, voice is assigned per agent. This breaks when multiple agents work the same domain, or one agent works across domains. Voice follows domain, not agent. The anchor enforces this by making voice the first thing any entering agent reads. The agent's own personality is irrelevant. The domain's voice wins. See **Voice Follows Domain** for the full routing pattern.

**The log as shared memory.** Context windows are session-scoped. When a session ends, everything learned dies unless saved. The domain log solves this for domain-specific knowledge. An agent in session 47 reads the log and knows what sessions 1 through 46 produced. The log is cheaper than full context and more reliable than agent recall. See **Append-Only Log** for the structural pattern behind it.

**Standing rules as accumulated corrections.** Rules don't come from design documents. They come from mistakes. "Always use Caret^ voice" became a rule because an agent used the wrong voice and a human corrected it. Rules are scar tissue — what the system learned the hard way. The notation gives them a home so lessons persist. See **Accumulated Corrections** for the learning mechanism.

Relationship to **Overnight Factory**: the factory assumes domains exist. Each run walks the domains, works their queues, checks output against domain standards. Without domain anchors, the factory has nothing to evaluate against.

Relationship to **Disposable Specialists**: specialists are ephemeral agents that enter a domain, do one job, and leave. The domain anchor gives them coherence despite having no memory of their own.
