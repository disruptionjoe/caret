# Domain Anchor

## Notation

```
^^^domain "purpose"
  ^voice "guide"
  ^goals
    ^active
    ^horizon
  ^log
  ^rules
```

## What it does

Defines a coherent unit of work that any agent can load and immediately understand. The domain has a purpose, a voice, active goals, long-term goals, a log of what has happened, and standing rules. An anchored agent — the domain anchor — is the persona that holds all of this together across sessions.

The anchor is not a worker. It is a context package. Any agent that enters this domain reads the anchor and inherits coherence: what this domain is for, how it sounds, what has been done, what is next, and what is not allowed.

## The anatomy of a domain

A domain has six components. All are mandatory except horizon goals, which are optional but recommended.

**Purpose.** One sentence. Why this domain exists. Not what it produces — why it matters. Every goal in the domain must trace back to this purpose. If it does not, it belongs in a different domain or it does not belong at all.

**Voice.** How this domain sounds. A pointer to the voice definition, not the definition itself. Voice is domain-locked: all output within this domain uses this voice, regardless of which agent produces it. The most common failure in multi-domain systems is voice bleed — an agent using Domain A's voice while working in Domain B. The anchor prevents this by making voice a first-class property of the domain, not the agent.

**Active goals.** What is being worked on now. Each goal has concrete projects with statuses, and each project has a clear next step. This is the queue. Agents entering the domain read active goals to know what to work on. Goals without next steps are stale. Goals with next steps but no `agent-ready` status are blocked. The anchor makes these states visible so agents do not waste runs figuring out what to do.

**Horizon goals.** Where this domain is heading. Not tasks — directions. These are the goals that active work builds toward but that no single run will complete. Horizon goals give the evaluator (or any agent deciding what to queue next) the context to make good auto-queuing decisions. Without them, auto-queuing degrades to "do the next obvious thing" without knowing whether that thing serves the larger direction.

**Log.** Append-only record of what has happened in this domain. Actions taken, decisions made, issues flagged, evaluator notes. The log is how agents across sessions maintain continuity without sharing context windows. An agent in session 47 reads the log and knows what sessions 1 through 46 produced. The log is the domain's memory.

**Standing rules.** Domain-specific constraints that override defaults. "Always use Caret^ voice, never Disruption Joe." "This is a collaboration — do not make unilateral decisions." "Income-generating work gets priority." Standing rules accumulate from human corrections. They are the lessons the system has learned about this specific domain.

## When to use it

You have work that spans multiple sessions, multiple agents, or both. The work has its own identity — a voice, a set of goals, constraints that do not apply elsewhere. Without a domain anchor, every agent that touches this work starts from zero: reads the files, infers the voice, guesses the context, and produces output that may or may not cohere with what came before.

Specific triggers:

- Multiple agents will work on the same body of work over time
- The work has a distinct voice or identity separate from other work
- You need evaluators or reviewers to check output against domain standards
- Queue-based systems (like the Overnight Factory) need to know what to work on and how
- You have caught voice bleed, scope confusion, or repeated context-gathering across sessions

## When not to use it

The work is a one-shot task. A single agent handles it in a single session and there is no future session that needs to pick up where it left off. Setting up a domain anchor for a one-shot task is overhead that buys nothing.

Also wrong when the work is genuinely cross-domain and resists classification. Some tasks serve multiple purposes and multiple voices. Forcing them into a single domain creates artificial constraints. Handle these at the orchestrator level, not the domain level.

If you have fewer than two goals in a domain, it might be a project, not a domain. Projects live inside domains. A domain with one project is a project that has been over-promoted.

## Design notes

The triple-caret (`^^^domain`) declares this as an anchored, persistent structure. It survives across sessions. It accumulates. This is the defining characteristic: domains remember.

The single-caret components (`^voice`, `^goals`, `^log`, `^rules`) are directives, not agents. They are structural declarations that the anchor carries. The notation makes the domain's anatomy visible in a glance. You can read the notation and know exactly what context an agent will load when it enters this domain.

**On purpose as a filter.** Purpose is not decorative. It is the filter that prevents scope creep. When an evaluator considers auto-queuing a task, it checks: does this serve the domain's purpose? When a human considers adding a new goal, the question is the same. A domain with a vague purpose ("do good work") filters nothing. A domain with a sharp purpose ("get Joe income") filters ruthlessly. The sharpness of the purpose determines the coherence of the domain.

**On voice as a property of the domain, not the agent.** This is a deliberate architectural choice. In naive multi-agent systems, voice is assigned per agent: "you are the writer, use this voice." This breaks when multiple agents work in the same domain, or when one agent works across domains. Voice follows domain, not agent. The anchor enforces this by making voice the first thing any entering agent reads. The agent's own personality is irrelevant. The domain's voice wins.

**On the log as shared memory.** Agent systems have a memory problem. Context windows are session-scoped. When a session ends, everything learned dies unless explicitly saved. The domain log solves this for domain-specific knowledge. It is not a general memory system — it is a domain's memory. What happened here. What was decided. What went wrong. An agent reading the log can reconstruct enough context to continue the work without re-deriving it from the files. The log is cheaper than full context and more reliable than agent recall.

**On standing rules as accumulated corrections.** Standing rules do not come from design documents. They come from mistakes. "Always use Caret^ voice" became a standing rule because an agent used the wrong voice and the human corrected it. "Do not make unilateral decisions in Pure" became a standing rule because the domain is a collaboration and solo action would damage trust. Standing rules are scar tissue. They are what the system learned the hard way. The notation gives them a home so the lessons persist.

**Relationship to Overnight Factory.** The factory pattern assumes domains exist. Each execution run walks the domains and works their queues. Each evaluation pass checks output against domain standards. Without domain anchors, the factory has nothing to evaluate against — no voice to check, no purpose to filter by, no log to reference. The Domain Anchor is the unit of coherence. The Overnight Factory is the cycle that operates on it.

**Relationship to Disposable Specialists.** Specialists are ephemeral agents that enter a domain, do one job, and leave. The domain anchor is what gives them coherence despite having no memory of their own. A writer entering the Caret^ domain reads the anchor, inherits the voice, and produces output that sounds like Caret^. Without the anchor, the specialist would need the voice guide, the goals, the context, and the rules passed explicitly every time — a brittle, error-prone handoff. The anchor standardizes what "entering a domain" means.
