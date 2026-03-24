# Handoff / Delegation / Transfer Control

## Questions for Joe

- "Handoff" is converging as the consensus term. This is one of the strongest cases for an ACON recommendation. Comfortable with ACON endorsing "handoff" as preferred?
- LangChain explicitly flags "what context gets passed during a handoff" as a key risk. Should this entry include a mini-framework for handoff design decisions (what gets passed, who decides, failure modes)? Or is that too prescriptive for v1?
- "Subagents as tools" (OpenAI/LangChain pattern) is a specific handoff implementation. Should it be a sub-section here or its own entry?
- The research shows handoff mechanics differ significantly (OpenAI: handoffs are tools; Semantic Kernel: explicit control transfer; LangChain: message filtering decisions). How deep into implementation should this go vs staying at the concept level?

---

> When one agent passes work to another — but the mechanics of what gets passed, who decides, and what happens on failure differ significantly across ecosystems.

## Status

Established (the term "handoff" is converging), but mechanics are fragmented

## What problem this helps you think about

When you're building a multi-agent system and Agent A needs to pass work to Agent B, three questions arise immediately: What context does Agent B receive? Who decides when the handoff happens? What happens if Agent B fails? The answer to all three varies by ecosystem, and getting them wrong is a common source of agent system failures.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Handoff | OpenAI Agents SDK, Semantic Kernel, LangChain | When one agent delegates a task to another. OpenAI: handoffs are represented as tools that the agent can invoke. Semantic Kernel: explicit "transfer control" with handoff orchestration. LangChain: message passing with explicit decisions about what context transfers. | OpenAI Agents SDK docs; Semantic Kernel handoff orchestration; LangChain handoff docs |
| Transfer control | Semantic Kernel | Specific term for the mechanism by which one agent passes execution authority to another within handoff orchestration. | Semantic Kernel docs |
| Delegation | General usage, LangChain | The broader concept of assigning work to a subordinate agent. "Delegation" implies hierarchy; "handoff" implies peer transfer. In practice, used interchangeably. | LangChain multi-agent docs |
| Subagents as tools | OpenAI, LangChain | A specific implementation where agents are registered as callable tools — one agent "calls" another the same way it would call a web search or database query. | OpenAI "Agents as tools" docs; LangChain "A main agent coordinates subagents as tools" |

## Key distinctions

**The term is converging; the mechanics are not.** "Handoff" appears across OpenAI, Semantic Kernel, and LangChain with similar meaning (one agent passes work to another). But the implementation differs in three ways that matter:

**1. What gets passed.** This is the most consequential design decision. Options:
- Full message history (the receiving agent sees everything the sending agent saw)
- Filtered messages (only selected context transfers — LangChain highlights this as a key "context engineering" risk)
- Structured state (a state object rather than conversation history)
- Tool results only (the receiving agent gets the output of the previous agent, not its reasoning)

**2. Who decides.** The handoff can be:
- Agent-initiated (the sending agent decides to hand off, often by invoking a handoff tool)
- Orchestrator-initiated (an external coordinator decides when to switch agents)
- Condition-triggered (a predefined rule determines when handoff occurs)

**3. What happens on failure.** If the receiving agent can't complete the task:
- Falls back to the sending agent
- Escalates to a human
- Triggers a different agent
- Fails silently (the most dangerous option)

**"Subagents as tools" is a specific handoff implementation,** not a competing concept. When agents are registered as tools, handoffs happen through the same mechanism as any tool call — the orchestrating agent "calls" another agent. This is clean and composable but limits what context can be passed (typically just the tool input/output, not full conversation history).

## How major ecosystems use this

### OpenAI
Handoffs are first-class in the Agents SDK. They are represented as tools — "Handoffs allow an agent to delegate tasks to another agent" and they appear in the agent's tool list. This means the agent autonomously decides when to hand off, and the handoff mechanism is the same as a tool call.

### Anthropic
No named "handoff" primitive in the API. Multi-agent patterns are documented as design guidance (orchestrator-workers pattern). Handoffs are implemented through tool calls or explicit workflow logic rather than a framework-level abstraction.

### LangChain / LangGraph
Explicit handoff support with emphasis on context management. The docs specifically call out the risk of passing too much or too little context during handoffs. LangGraph's state management provides fine-grained control over what persists across agent boundaries.

### Microsoft (Semantic Kernel)
"Handoff orchestration" is a named orchestration pattern where agents can "transfer control" to other agents. The framework provides explicit handoff mechanics as part of its orchestration layer.

## Why the distinction matters in practice

The most common handoff failure is context loss. Agent A has important context that Agent B needs, but the handoff mechanism only passes the final output, not the reasoning or intermediate state. Agent B then makes decisions without critical information.

The second most common failure is unclear ownership. After a handoff, who is responsible for the task? If both agents think the other is handling it, the task falls through the cracks. If both agents try to handle it, you get conflicting outputs.

## Examples

### Pattern in action
A customer inquiry arrives. A triage agent classifies it and hands off to a specialist agent. The **handoff decision:** the triage agent decides based on intent classification (agent-initiated). The **context passed:** the customer's message plus the classification result, but NOT the triage agent's internal reasoning (filtered). The **failure mode:** if the specialist agent can't resolve it, escalate to a human with the full conversation history.

### Anti-patterns / confusion traps
- Passing full conversation history through every handoff. This fills the receiving agent's context window and dilutes the relevant information.
- Not specifying failure behavior. "What if the handoff target fails?" should be answered before building, not after.
- Assuming handoffs are symmetric. In most implementations, Agent A handing off to Agent B is not the same as Agent B handing off to Agent A — the context passing rules may differ.

## Evidence level

- **Established terms:** "handoff" (converging across 3+ ecosystems), "delegation" (general usage synonym)
- **Fragmented terms:** "transfer control" (Semantic Kernel-specific), "subagents as tools" (implementation pattern, not a term)
- **Inferred patterns:** The three-axis framework (what gets passed / who decides / failure behavior) is an ACON synthesis of observations across ecosystems, most directly supported by LangChain's context engineering warnings

## ACON recommendation

ACON uses **"handoff"** as the primary label for this concept because it has the strongest cross-ecosystem convergence. When designing handoffs, ACON recommends explicitly specifying three things: what context transfers, who triggers the handoff, and what happens on failure.

## Related entries

- Orchestrator vs Router vs Supervisor — the roles that manage handoffs
- Memory vs Context Window vs Retrieval — what gets passed during a handoff is a context engineering decision
- Ephemeral vs Persistent Agent Identity — affects whether the receiving agent starts fresh or with accumulated context

## Changelog

- 2026-03-22: Initial entry
