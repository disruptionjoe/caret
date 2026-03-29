# Fragmented Terminology

Terms in active use across multiple ecosystems with competing or inconsistent definitions. Each entry documents what the term means in different contexts, where the fragmentation causes real problems, and the Caret^ position.

---

## Tool vs Skill vs Plugin

**Status:** Fragmented across ecosystems. "Tool" is converging; "skill" and "plugin" have conflicting meanings.

### The Problem

A single capability that an agent can invoke. But depending on which ecosystem you work in, you call it a "tool," "skill," or "plugin." They appear in major documentation and are used almost interchangeably. They are not the same thing architecturally.

### What It Means in Different Contexts

| Term | Ecosystem | Meaning | Architecture |
|------|-----------|---------|--------------|
| **Tool** | OpenAI, Anthropic, LangChain, Semantic Kernel | A discrete callable function. Agent sends structured input, gets structured output. Tools are atomic. | Function → Input → Output |
| **Function calling** | OpenAI (legacy), converging on "tool calling" | The protocol layer by which a model invokes a tool. Now standardizing as "tool calling." | Protocol mechanism, not the capability itself |
| **Skill** | Anthropic (Cowork/Claude Code) | A markdown instruction file that defines a complete workflow or task approach. Skills are instructions that shape behavior. They don't provide capabilities — they provide guidance. | Instruction set → Behavioral change |
| **Skill** | LangChain | A dynamic bundle that includes tool registration, context, and behavioral configuration. Broader than a tool, narrower than a full agent. | Tool aggregation + context injection |
| **Plugin** | Microsoft (Semantic Kernel) | What "skill" used to mean — a renamed concept aligning with OpenAI plugins. Packages tools with metadata. | Tools + metadata container |
| **Plugin** | Anthropic (Cowork) | An installable distribution bundle containing MCPs, skills, and tools. A packaging and distribution layer. | Distribution abstraction |

### Where Fragmentation Creates Problems

If you call everything a "skill," you'll confuse yourself moving between ecosystems. Cowork skills (behavioral instructions) don't map to LangChain skills (tool bundles) even with the same label. Reading Semantic Kernel docs about "plugins" and assuming it matches Cowork plugins will set wrong expectations about distribution and discovery.

When you're designing a system, you're making three decisions, not one:

1. **What capabilities does the agent need?** (tools)
2. **What behavioral guidance should it follow?** (skills)
3. **How is this packaged and distributed?** (plugins)

These are separate questions. Conflating them breaks composability.

### Design Consequence

Choosing the wrong abstraction affects:
- **Composability:** Can you reuse it in other agents or systems?
- **Portability:** Does it move to different frameworks intact?
- **Maintenance:** When something changes, how far does the change ripple?

Treating a behavioral instruction like a callable function breaks the abstraction. Treating a tool bundle like a distribution format hides real packaging questions.

### Caret^ Position

Use **"tool"** as the primary label for discrete callable capabilities. It has the strongest cross-ecosystem convergence. When using "skill" or "plugin," specify the ecosystem. In cross-ecosystem documentation, prefer "tool."

When building systems, distinguish these three questions explicitly:
- **Capabilities** (tools) — what the agent can do
- **Behavioral guidance** (skills) — how it should behave
- **Packaging** (plugins) — how it's distributed and installed

### Related Terms

- Model Context Protocol (MCP) — the standardization layer for tool integration
- Orchestrator vs Router vs Supervisor — roles that manage tools and skills

---

## Orchestrator vs Router vs Supervisor

**Status:** Fragmented. "Orchestrator" is common but overloaded; "router" is clearer but narrower.

### The Problem

The role responsible for deciding which agents work on what, when, and in what order — but the name and scope of that role differ significantly across ecosystems. The architecture implied by each name is different.

### What It Means in Different Contexts

| Term | Ecosystem | Meaning | State Management | Scope |
|------|-----------|---------|------------------|-------|
| **Orchestrator** | Semantic Kernel, general usage | A coordination layer managing multi-step, multi-agent workflows. Maintains state across interactions. Handles sequential, concurrent, and handoff patterns. | Full state persistence | Entire workflow |
| **Router** | LangChain, general usage | A dispatch mechanism. Selects the next agent or path based on current input. Often stateless — doesn't maintain multi-turn context. | Minimal or no state | Single decision point |
| **Supervisor** | LangGraph | A specific pattern where one agent coordinates others, deciding which sub-agent to invoke. Maintains conversation history and shared state. | Shared state graph | Multi-agent coordination |
| **Manager** | AutoGen, CrewAI | The coordinating agent in multi-agent conversation. Manages turn-taking and delegation. Functionally equivalent to "orchestrator." | Full state tracking | Entire workflow |

### The Critical Distinction: Routing vs Orchestration

A **router** is a dispatch point. It answers: "Which agent should handle this?" It looks at the current input and decides. Lightweight, often stateless. A router is a single decision.

An **orchestrator** is a coordination layer. It answers: "What's the plan? What's done? What's next? What if something fails?" It manages entire workflows across multiple steps, tracks progress, handles failures, maintains state across turns.

Most multi-agent systems need both. The router handles initial dispatch. The orchestrator manages the workflow after dispatch. Confusing the two leads to either over-engineering simple dispatch or under-engineering complex coordination.

### Supervisor Is a Pattern, Not a Competing Concept

A supervisor is a specific orchestration implementation: one agent coordinating others via shared state. In LangGraph, it's explicit. In Semantic Kernel, orchestration is the broader framework and supervisors are one pattern among several (sequential, concurrent, handoff, group chat). A supervisor is a type of orchestrator.

### Manager Is a Synonym

AutoGen's "manager" and CrewAI's "manager" both describe the coordinating agent in multi-agent setups. No meaningful architectural distinction from "orchestrator" — just different naming conventions.

### Where Fragmentation Creates Problems

If you call your dispatch logic an "orchestrator," you'll over-engineer it — adding state management and failure handling to something that should be simple routing. If you call your coordination layer a "router," you'll under-engineer it — expecting stateless dispatch when you actually need workflow management.

The most common mistake: building a "smart router" that gradually accumulates state, history tracking, error handling until it's actually an orchestrator — without the architectural design decisions (state persistence, checkpoint/resume, failure modes) that an orchestrator needs from the start.

### Caret^ Position

Distinguish **router** (stateless dispatch) from **orchestrator** (stateful coordination) as a primary design axis. This is the clearest case for recommending a distinction. "Supervisor" is a specific orchestration pattern. "Manager" is effectively a synonym for orchestrator.

When designing multi-agent systems, decide whether each coordination point routes or orchestrates. The answer drives architectural decisions about state, persistence, and failure handling.

### Related Terms

- Handoff / Delegation / Transfer — the mechanism by which orchestrators and routers pass work
- Agent Identity Persistence — affects whether orchestration requires state persistence (see `^^` change hat vs `^^^` change worker)

---

## Handoff / Delegation / Transfer

**Status:** Mostly established ("handoff" is converging), but mechanics are fragmented.

### The Problem

When one agent passes work to another, three critical questions arise:

1. **What context does the receiving agent get?**
2. **Who decides when it happens?**
3. **What happens if it fails?**

The answer to all three varies by ecosystem. Getting them wrong is a common source of agent system failures.

### What It Means in Different Contexts

| Term | Ecosystem | Meaning | Context Transfer | Trigger | Failure Handling |
|------|-----------|---------|-------------------|---------|-----------------|
| **Handoff** | OpenAI Agents SDK, Semantic Kernel, LangChain | When one agent delegates a task to another. | Varies: tool input/output, filtered messages, or full history | Agent-initiated (tool call) or orchestrator-initiated | Variable |
| **Transfer control** | Semantic Kernel | Specific term for the mechanism by which one agent passes execution authority to another. Part of handoff orchestration. | Explicit state transfer | Orchestrator-initiated | Explicit escalation |
| **Delegation** | General usage, LangChain | Broader concept: assigning work to a subordinate agent. Implies hierarchy. | Varies | Varies | Varies |
| **Subagents as tools** | OpenAI, LangChain | Agents registered as callable tools. One agent "calls" another the same way it calls web search or database query. | Tool input/output only | Agent-initiated (tool call) | Tool error propagation |

### The Term Is Converging; The Mechanics Aren't

"Handoff" appears across OpenAI, Semantic Kernel, and LangChain with similar meaning (one agent passes work to another). But implementation differs in three critical ways.

### Design Decision 1: What Gets Passed

The most consequential choice:

- **Full message history** — receiving agent sees everything the sending agent saw
- **Filtered messages** — only selected context transfers (LangChain emphasizes this as a key "context engineering" risk)
- **Structured state** — a state object rather than conversation history
- **Tool results only** — receiving agent gets output, not reasoning or intermediate steps

More context can help but fills the context window and creates bias. Less context can cause decision-making on incomplete information. There is no universal right answer — the choice depends on the task and the architecture.

### Design Decision 2: Who Decides

The handoff can be:

- **Agent-initiated** — the sending agent decides, often by invoking a handoff tool
- **Orchestrator-initiated** — an external coordinator decides when to switch agents
- **Condition-triggered** — a predefined rule determines when handoff occurs

Agent-initiated handoffs are flexible but less controlled. Orchestrator-initiated handoffs are predictable but less responsive. Condition-triggered handoffs are deterministic but rigid.

### Design Decision 3: What Happens on Failure

If the receiving agent can't complete the task:

- **Falls back to sending agent** — retry with the same or different approach
- **Escalates to human** — breaks the agent chain
- **Triggers a different agent** — tries an alternative specialist
- **Fails silently** — the most dangerous option

Failure handling must be explicit. The default (silent failure) is often the worst choice.

### Subagents as Tools Is an Implementation Pattern

Not a competing concept. When agents are registered as tools, handoffs happen through the same mechanism as any tool call. The orchestrating agent "calls" another agent. This is clean and composable but limits context passing (typically tool input/output, not full conversation history).

### Where Fragmentation Creates Problems

The most common handoff failure is context loss. Agent A has important context that Agent B needs, but the handoff only passes the final output. Agent B then decides without critical information. The second most common failure is unclear ownership. After handoff, who is responsible? If both agents think the other is handling it, the task falls through the cracks.

### Caret^ Position

Use **"handoff"** as the primary label — it has the strongest cross-ecosystem convergence. When designing handoffs, explicitly specify three things:

1. **What context transfers** — full history, filtered, structured state, or output only
2. **Who triggers the handoff** — agent, orchestrator, or condition
3. **What happens on failure** — fallback, escalation, retry, or alternative

Don't let these be accidents.

### Related Terms

- Orchestrator vs Router vs Supervisor — the roles that manage and decide on handoffs
- Memory vs Context Window vs Retrieval — what gets passed is a context engineering decision
- Agent Identity Persistence — affects whether receiving agent starts fresh or with accumulated context (see `^^` change hat vs `^^^` change worker)

---

## Foundational Pattern

These three fragmented concepts are tightly coupled:

- The **tools** you choose determine what capabilities exist.
- The **skills** you define determine how the agent behaves with those tools.
- The **plugins** you use determine how capabilities are distributed.

In multi-agent systems:

- **Routers and orchestrators** manage handoffs.
- **Handoffs** require explicit decisions about context, ownership, and failure.
- Getting these distinctions clear is the foundation for systems that don't accumulate confusion as they grow.

Treat fragmentation as a design signal. Each time you find yourself choosing between terms, you're making an architectural decision. Make that decision visible.
