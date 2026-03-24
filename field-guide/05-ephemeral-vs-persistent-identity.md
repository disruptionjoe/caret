# Ephemeral vs Persistent Agent Identity

## Questions for Joe

- This is core ACON territory — your existing glossary already has "ephemeral spawning" and "anchored spawning." The research confirms the pattern is real but the naming is fragmented. Should ACON lean into its own terms here (ephemeral/anchored) or align with the more common stateful/stateless framing?
- "Anchored" is your original term. The ecosystem uses "persistent," "stateful," "continuity-bearing," and "resume-capable." Is "anchored" distinct enough to justify as an ACON recommendation, or should we map it as one variant among many?
- Related: "Persona Refresh Cycle" and "Fresh-Eyes Loop" from your existing glossary are specific patterns within this space. Should they be referenced here or kept in the emerging patterns annex?
- The DSL research proposes context inheritance modes (none/summary/selected/full/fork) as the implementation layer for this concept. Should this entry reference those modes, or keep it at the concept level and let the PDN handle implementation?

---

> Whether an agent starts fresh with no prior context or inherits identity, memory, and state from previous invocations — a design axis that appears across many frameworks but lacks a consensus name.

## Status

Fragmented (the concept is universal; the terminology is not consolidated)

## What problem this helps you think about

Every time you spawn an agent — whether it's a sub-agent in a workflow, a reviewer, or a new session of a long-running assistant — you face a fundamental choice: should it start completely fresh, or should it carry forward context from previous work? This choice affects bias, quality, cost, and whether the agent can maintain consistency over time.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Ephemeral | General usage, agent tooling | An agent that exists for one invocation and is discarded. No memory, no identity persistence. Each run starts from zero. | Sub-agent tooling discussions; practitioner usage |
| Persistent | General usage, agent tooling | An agent that maintains state across invocations. It remembers past interactions, decisions, and context. | Sub-agent tooling; persistent vs ephemeral mode discussions |
| Stateful / Stateless | General computing, applied to agents | Borrowed from computing: stateful agents retain information between calls; stateless agents don't. Maps directly onto persistent/ephemeral. | General computing terminology applied to agents |
| Anchored | ACON (proposed) | An agent that inherits or loads specific context — memory, principles, prior decisions. Implies intentional continuity: the agent is "anchored" to accumulated knowledge. | ACON glossary (original) |
| Resume / New session | Practical usage | Whether an agent continues an existing session (with full history) or starts a new one (fresh). A concrete implementation of the persistent/ephemeral axis. | Agent tooling docs |
| Memory-bearing / Memory-light | Informal | Describes the amount of persistent context an agent carries. "Memory-bearing" agents load prior knowledge; "memory-light" agents operate with minimal or no history. | Informal practitioner usage |

## Key distinctions

**The axis is simple; the tradeoffs are not.** At its core, this is a binary choice: does the agent carry forward context, or start fresh? But the real design space is a spectrum:

1. **Fully ephemeral:** No prior context. Every invocation is independent. The agent has no memory of previous interactions, decisions, or mistakes.
2. **Summary-loaded:** The agent receives a compressed summary of prior context, not the full history. Cheaper than full persistence, but lossy.
3. **Selectively loaded:** The agent inherits specific pieces of prior context (e.g., a user profile, key decisions, constraints) but not everything. Intentional curation of what carries forward.
4. **Fully persistent:** The agent has access to complete history. Every prior interaction is available. Most expensive in tokens, but highest continuity.
5. **Fork:** The agent starts with full prior context but from that point forward operates independently — changes don't propagate back. A snapshot, not a live connection.

**Why ephemeral agents matter:** They provide unbiased "fresh eyes." When an agent has been working on something for a while, it accumulates context that can become bias — it stops questioning early assumptions. Spawning a fresh agent to review the same work catches blind spots that the persistent agent has developed.

**Why persistent agents matter:** They maintain consistency. A persistent project assistant that remembers past decisions, user preferences, and project context doesn't need to be re-briefed every session. It builds institutional knowledge.

**The naming problem:** Different ecosystems use different words for the same axis (ephemeral/persistent, stateful/stateless, new session/resume), and none has emerged as the standard. ACON's original "ephemeral/anchored" framing adds the nuance that "anchored" implies intentional context loading (not just "has state"), but this term doesn't appear in any major framework.

## How major ecosystems use this

### OpenAI
Agents in the Agents SDK are effectively ephemeral per API call — they don't persist state between calls unless the developer manages it. The Assistants API adds thread-based conversations with some persistence. No explicit ephemeral/persistent concept in the agent framework itself.

### Anthropic
Claude Code sessions are ephemeral by default (context resets between conversations) but supports persistent context through memory files (CLAUDE.md) that are loaded each session. The "fresh context" / "just-in-time" guidance is a strategy for managing what persists vs what starts fresh.

### LangChain / LangGraph
Explicit support for both modes. LangGraph checkpointers enable persistent state (resume a workflow from where it left off). Thread-based conversations maintain history within a thread. Cross-thread stores enable long-term memory across different conversation threads. The framework lets you choose your position on the ephemeral-persistent spectrum per workflow step.

### General agent tooling
Sub-agent tooling often explicitly discusses "persistent mode" vs "ephemeral mode" for invocation. The choice affects token usage, context window pressure, and whether the sub-agent can be meaningfully re-used.

## Why the distinction matters in practice

**Review quality depends on this choice.** If your review agent inherits the context of the agent that did the work, it will see the same assumptions and miss the same blind spots. A fresh review agent catches things the working agent stopped noticing.

**Cost scales with persistence.** Persistent agents that carry full history consume more tokens per invocation. For long-running projects, this becomes significant. Selective loading (only carry forward what matters) is the practical middle ground.

**Consistency vs freshness is a real tradeoff.** A persistent project assistant that "knows everything" is great for continuity but may calcify around early decisions. Periodic "fresh starts" with selective context transfer can combine the benefits of both.

## Examples

### Pattern in action
A writing assistant works on a document over multiple sessions. The **persistent mode**: it loads the user's profile, style preferences, and the current document state every session — continuity without re-briefing. After the draft is complete, a **fresh (ephemeral) reviewer** reads the document with no knowledge of the writing process, drafting decisions, or compromises. It evaluates the output on its own merits.

### Anti-patterns / confusion traps
- Assuming "persistent" means "better." For review tasks, fresh agents outperform persistent ones at catching blind spots.
- Loading full conversation history into a persistent agent without filtering. The accumulated context eventually exceeds the context window and degrades performance.
- Not choosing explicitly. If you don't decide whether an agent should be ephemeral or persistent, the default is usually ephemeral — which means losing valuable context by accident rather than by design.

## Evidence level

- **Established terms:** "stateful/stateless" (borrowed from computing, widely understood), "persistent/ephemeral" (common in agent tooling)
- **Fragmented terms:** "anchored" (ACON-proposed), "memory-bearing/memory-light" (informal), "resume/new session" (practical)
- **Inferred patterns:** The five-point spectrum (fully ephemeral → summary → selective → full → fork) is an ACON synthesis drawn from the combination of LangGraph's persistence primitives and Anthropic's context engineering strategies

## ACON recommendation

No single consensus term exists. ACON documents the axis using **"ephemeral" vs "persistent"** as the primary labels because they are the most widely understood. ACON also introduces the context inheritance spectrum (none → summary → selective → full → fork) as a practical framework for designing agent identity decisions. "Anchored" is retained as an ACON-proposed term for "persistent with intentional context curation" — a useful distinction not yet reflected in ecosystem terminology.

## Related entries

- Memory vs Context Window vs Retrieval — the mechanism layer for implementing persistence
- Handoff / Delegation / Transfer Control — handoffs involve decisions about identity persistence
- Fresh-Eyes Review Loop (emerging) — a specific pattern that depends on ephemeral spawning
- Guardrails and Validation — persistent agents may need periodic bias checks

## Changelog

- 2026-03-22: Initial entry
