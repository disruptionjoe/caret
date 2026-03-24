# ACON Field Guide — Draft Index

A practitioner-facing concept map for agent systems. Organized around clusters of related terms and the design-relevant distinctions between them.

## Cluster Entries (Main Field Guide)

1. [Tool vs Skill vs Plugin](clusters/01-tool-vs-skill-vs-plugin.md) — Status: Fragmented
2. [Orchestrator vs Router vs Supervisor vs Manager](clusters/02-orchestrator-vs-router-vs-supervisor.md) — Status: Fragmented
3. [Memory vs Context Window vs Retrieval vs Just-in-Time Context](clusters/03-memory-vs-context-vs-retrieval.md) — Status: Fragmented
4. [Handoff / Delegation / Transfer Control](clusters/04-handoff-delegation-transfer.md) — Status: Established (mechanics fragmented)
5. [Ephemeral vs Persistent Agent Identity](clusters/05-ephemeral-vs-persistent-identity.md) — Status: Fragmented
6. [Guardrails and Validation](clusters/06-guardrails-and-validation.md) — Status: Established (scope fragmented)
7. [File-Based Instruction Patterns](clusters/07-file-based-instruction-patterns.md) — Status: Fragmented
8. [Model Context Protocol (MCP)](clusters/08-model-context-protocol.md) — Status: Established (new)

## Emerging Patterns Annex

- [Fresh-Eyes Review Loop](emerging/fresh-eyes-review-loop.md) — Working label
- [Context Mount](emerging/context-mount.md) — Working label
- [Agent Harness](emerging/agent-harness.md) — Emerging

## How to read an entry

Each cluster entry follows a consistent schema:

- **Questions for Joe** — feedback needed before finalizing
- **Status** — Stable, Fragmented, Emerging, or Working Label
- **What problem this helps you think about** — the design decision this cluster addresses
- **Terms in this cluster** — the competing/overlapping terms mapped with sources
- **Key distinctions** — the boundaries that matter for design (highest-value section)
- **How major ecosystems use this** — OpenAI, Anthropic, LangChain, Microsoft where relevant
- **Why the distinction matters in practice** — concrete impact of getting this wrong
- **Examples** — pattern in action + anti-patterns
- **Evidence level** — established vs fragmented vs inferred
- **ACON recommendation** — when ACON has one

## Total feedback questions across all entries: ~35

Each entry has 3-5 questions at the top. Review them in order of priority — entries 1-4 are the highest-value clusters.
