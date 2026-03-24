# Agent Harness

## Questions for Joe

- "Harness" is already in your ACON glossary as a foundational term, defined as "the platform or environment that hosts and runs the agent." LangChain recently published a more specific anatomy (system prompt + tools/skills + orchestration + hooks + infrastructure). Should the existing term be upgraded to a cluster entry, or is it stable enough as a foundational term?
- The research classifies this as "medium (emerging)" — LangChain is leading the terminology but it hasn't been widely adopted by other ecosystems yet. Is it ready for the main field guide, or should it stay emerging?
- "Runtime," "environment," "platform," and "harness" all describe overlapping concepts. Is "harness" the best term to center on, or is it too LangChain-specific?

---

> ⚠️ EMERGING PATTERN — The term "harness" has gained a concrete meaning in recent LangChain documentation but is not yet widely adopted across ecosystems. This entry tracks its evolution.

## The pattern

The complete runtime environment that hosts an agent — including not just the model, but the system prompt, registered tools and skills, orchestration logic, hooks/middleware, and infrastructure. The "harness" frames the agent as one component within a larger engineering layer.

## Why it matters

When people say "agent," they often mean just the model + prompt. But in practice, an agent's behavior is shaped by everything around it: what tools it can access, what hooks intercept its actions, what orchestration logic manages its workflow, and what infrastructure runs it. "Harness" gives a name to this surrounding layer and makes it a first-class design concern.

## Where it appears

- LangChain "agent harness" anatomy (March 2026): explicitly documents the harness as system prompts + tools/skills/MCPs + orchestration logic + hooks/middleware + infrastructure
- Cursor's rules + tools + extensions system (implicitly a harness)
- Claude Code's permission modes + hooks + memory system + tool access (implicitly a harness)
- General usage: "runtime harness" appears in agent engineering discussions

## Key components (per LangChain's framing)

1. **System prompt / instructions** — the behavioral baseline
2. **Tools, skills, MCPs** — the capabilities available to the agent
3. **Orchestration logic** — how the agent's workflow is managed (routing, handoffs, state)
4. **Hooks / middleware** — interception points that can inspect, modify, or block agent actions
5. **Infrastructure** — execution environment, monitoring, persistence, deployment

## Naming variants observed

- "Harness" (LangChain-led)
- "Runtime" (general engineering)
- "Agent environment" (informal)
- "Platform" (used loosely but overloaded)
- "Scaffold" / "scaffolding" (sometimes used for the same concept)

## Evidence

- LangChain's published "agent harness" anatomy (2026)
- Implicit harness implementations in Cursor and Claude Code
- Evidence level: Medium. The term is gaining traction but is not yet adopted beyond LangChain. The concept is universal; the specific "harness" label is not.

## Status: Working label

"Harness" is emerging as a useful term for the agent runtime layer. It may consolidate as LangChain's influence spreads, or competing terms ("runtime," "scaffold") may win. ACON tracks this as an important concept regardless of which name stabilizes, because the architectural insight — "the agent is shaped by its harness more than its model" — is broadly true and useful.

## Related entries

- Tool vs Skill vs Plugin — tools and skills are components of the harness
- File-Based Instruction Patterns — system instructions are part of the harness
- Guardrails and Validation — hooks/middleware in the harness implement guardrails
- Orchestrator vs Router vs Supervisor — orchestration logic is a harness component

## Changelog

- 2026-03-22: Initial entry as emerging pattern
