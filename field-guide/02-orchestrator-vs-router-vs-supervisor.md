# Orchestrator vs Router vs Supervisor vs Manager

## Questions for Joe

- Your existing glossary has "Primary Orchestrator," "Chief of Staff," and "Meta-Orchestrator" as a hierarchy. Should those ACON-specific terms stay as-is, or should they be reframed through the lens of the research (which positions them as one possible implementation of orchestration roles)?
- The research shows that "router" is architecturally distinct from "orchestrator" (routers dispatch without maintaining state; orchestrators coordinate across turns). Should ACON explicitly recommend this distinction? It's the clearest case for an ACON recommendation.
- "Manager" appears in AutoGen and Crew-style frameworks but is essentially a synonym for orchestrator. Include it, or note it briefly and move on?
- Should ACON's "Chief of Staff" concept be positioned as an emerging pattern that ACON is naming? It doesn't appear in any major framework's docs under that name.

---

> The role responsible for deciding which agents work on what, when, and in what order — but the name and scope of that role vary significantly by ecosystem.

## Status

Fragmented

## What problem this helps you think about

When you're designing a multi-agent system and need to decide how work gets distributed — who picks the next agent, who tracks progress, who handles failures — you'll encounter "orchestrator," "router," "supervisor," and "manager" used to describe overlapping but different roles. The choice isn't just naming; it implies different architectures.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Orchestrator | Semantic Kernel, general usage | A coordination layer that manages multi-step, multi-agent workflows. Maintains state across interactions. Can include sequential, concurrent, and handoff patterns. | Semantic Kernel "Agent Orchestration" framework |
| Supervisor | LangGraph | A specific multi-agent pattern where one agent coordinates others, deciding which sub-agent to invoke based on the current state. Maintains conversation history. | LangGraph "Multi-Agent Supervisor" docs |
| Router | LangChain | A dedicated dispatch step that selects the next agent or path. Often stateless — routes based on the current input without maintaining multi-turn conversation history. | LangChain router docs |
| Manager | AutoGen, CrewAI | The coordinating agent in a multi-agent conversation. Manages turn-taking and delegation. Essentially synonymous with "orchestrator" in these frameworks. | AutoGen multi-agent docs |
| Coordinator | General usage | Informal synonym for orchestrator. No ecosystem-specific definition. | Various |

## Key distinctions

**The critical distinction is between routing and orchestration.** A router is a dispatch mechanism — it looks at the current input and decides where to send it, often without maintaining state or multi-turn context. An orchestrator is a coordination layer — it manages an entire workflow across multiple steps, tracks progress, handles failures, and maintains state.

This matters because:
- A **router** is lightweight and composable. It answers "which agent should handle this?" It's a single decision point.
- An **orchestrator** is heavyweight and stateful. It answers "what's the plan, what's done, what's next, and what do we do if something fails?" It's a coordination role.

Most multi-agent systems need both. The router handles initial dispatch; the orchestrator manages the workflow after dispatch. Confusing the two leads to either over-engineering a simple dispatch step or under-engineering a complex coordination problem.

**Supervisor vs orchestrator** is a narrower distinction. In LangGraph, a supervisor is a specific implementation pattern: one agent that coordinates others via a shared state graph. In Semantic Kernel, "orchestration" is the broader framework that includes supervisors as one pattern among several (sequential, concurrent, handoff, group chat). A supervisor is a type of orchestrator, not a competing concept.

**Manager is essentially a synonym for orchestrator** in frameworks that use it. AutoGen's "manager" and CrewAI's "manager" both describe the coordinating agent in a multi-agent setup. No meaningful architectural distinction from "orchestrator."

## How major ecosystems use this

### OpenAI
Does not use a named "orchestrator" role. Multi-agent coordination happens through handoffs (agents delegate to other agents via tool calls). The orchestration is implicit — embedded in the handoff chain rather than managed by a dedicated coordinator.

### Anthropic
Uses "orchestrator" informally in documentation about agent patterns. The "orchestrator-workers" pattern appears in guidance about building effective agents. No named orchestrator framework or class.

### LangChain / LangGraph
Makes the router/orchestrator distinction explicit. LangChain docs define a "Router" as a dedicated dispatch step. LangGraph provides "Multi-Agent Supervisor" as a named pattern with shared state management, tool delegation, and conversation routing.

### Microsoft (Semantic Kernel / AutoGen)
Semantic Kernel has "Agent Orchestration" as a first-class framework with named patterns: sequential, concurrent, group chat, handoff. AutoGen uses "manager" for the coordinating agent in multi-agent conversations.

## Why the distinction matters in practice

If you call your dispatch logic an "orchestrator," you'll over-build it — adding state management and failure handling to what should be a simple routing decision. If you call your coordination layer a "router," you'll under-build it — expecting stateless dispatch when you actually need workflow management.

The most common mistake: building a "smart router" that gradually accumulates state, history tracking, and error handling until it's actually an orchestrator — but without the architectural decisions (state persistence, checkpoint/resume, failure modes) that an orchestrator needs from the start.

## Examples

### Pattern in action
A customer support system: a **router** reads the incoming message and dispatches it to the billing agent, the technical support agent, or the general inquiry agent based on intent classification. A **supervisor/orchestrator** manages a complex return process that requires coordinating between the refund agent, inventory agent, and shipping agent across multiple steps with state persistence.

### Anti-patterns / confusion traps
- Building a "router" that maintains conversation history across dispatches. That's an orchestrator; call it one and design it accordingly.
- Assuming every multi-agent system needs an orchestrator. Simple dispatch (one input → one handler) only needs a router.
- Using "manager" without specifying whether it routes or orchestrates. The word is ambiguous enough to cause real design confusion.

## Evidence level

- **Established terms:** "orchestrator" (high usage, fragmented scope), "router" (established with clearer boundaries), "supervisor" (LangGraph-specific but well-documented)
- **Fragmented terms:** "manager" (synonym for orchestrator in some frameworks, ambiguous elsewhere)
- **Inferred patterns:** The router-vs-orchestrator distinction as a primary architectural axis is an ACON emphasis, supported by LangChain's explicit separation but not universally documented

## ACON recommendation

ACON recommends distinguishing **router** (stateless dispatch) from **orchestrator** (stateful coordination) as a primary design axis. "Supervisor" is a specific orchestration pattern (one agent coordinating others); "manager" is effectively a synonym for orchestrator. When designing multi-agent systems, decide whether each coordination point is routing or orchestrating — the answer drives architectural decisions about state, persistence, and failure handling.

## Related entries

- Handoff / Delegation / Transfer Control — the mechanism by which orchestrators and routers pass work
- Ephemeral vs Persistent Agent Identity — affects whether orchestration requires state persistence
- Guardrails and Validation — orchestrators often manage validation checkpoints across workflow steps

## Changelog

- 2026-03-22: Initial entry
