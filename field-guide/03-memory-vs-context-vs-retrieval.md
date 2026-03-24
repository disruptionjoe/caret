# Memory vs Context Window vs Retrieval vs Just-in-Time Context

## Questions for Joe

- This is the fastest-moving area in the research. "Context engineering" as a term is gaining traction (Anthropic published formal guidance on it) but isn't universal yet. Should ACON treat it as established or emerging?
- RAG (Retrieval-Augmented Generation) is a huge concept that overlaps with this cluster. Include it as a related term, or keep it out of scope because it's well-documented elsewhere?
- Your EA system uses file-based memory (daily notes, profile, memory.md). Should this entry reference that pattern as a real-world example of "file-directory memory"? Or keep it ecosystem-focused?
- The research identifies "just-in-time context" as an Anthropic-specific framing. LangGraph uses "checkpointers + stores." CrewAI uses "fact extraction + injection." Should ACON try to unify these under one label, or map them as variants?
- How deep should this entry go on the "memory types" taxonomy (short-term vs long-term vs episodic vs semantic)? These categories exist in academic literature but practitioners mostly just say "memory."

---

> What the agent knows, when it knows it, and how it got there — but the mechanisms, scope, and terminology for all of this vary dramatically across ecosystems.

## Status

Fragmented

## What problem this helps you think about

When an agent "forgets" something important, or "knows" something it shouldn't, or runs out of room for information mid-task — the root cause is almost always a confusion between context, memory, and retrieval. These are three different layers that get collapsed into the single word "memory" in most conversations.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Context window | Universal | The total token capacity the model can hold at once — the agent's working memory. Everything the agent "sees" during a conversation lives here. When it fills, things get dropped. | All major ecosystem docs |
| Memory (persistent) | Anthropic, Semantic Kernel, CrewAI | Information that survives across sessions. Anthropic: file-directory storage read by a memory tool. Semantic Kernel: long-term vs short-term memory providers. CrewAI: fact extraction and injection before tasks. | Anthropic memory tool docs; Semantic Kernel agent memory docs; CrewAI memory docs |
| Memory (working) | General usage | What the agent currently holds in the context window. Ephemeral — lost when the session ends or the window fills. | Informal but widespread |
| Retrieval | RAG literature, most frameworks | The act of fetching relevant information from an external store (vector DB, file system, API) and injecting it into the context window. | RAG pattern documentation across ecosystems |
| Just-in-time context | Anthropic | A strategy: don't load everything upfront. Instead, use lightweight identifiers and tool-based retrieval to pull information into context only when it's needed. | Anthropic "effective context engineering" guidance |
| Context engineering | Anthropic, emerging general usage | The practice of intentionally designing what enters the context window, when, and how. Includes strategies like progressive disclosure, selective loading, and file-gated access. | Anthropic context engineering docs |
| Checkpoint | LangGraph | A saved snapshot of conversation/workflow state that enables resumption. Not "memory" in the human sense — more like a save point in a game. | LangGraph persistence docs |
| Store | LangGraph | A cross-thread memory abstraction — information that persists across different conversation threads, not just within one. | LangGraph memory store docs |
| Crew memory | CrewAI | A system that extracts facts from conversations and injects recalled context before each new task. Operates automatically rather than on-demand. | CrewAI memory documentation |

## Key distinctions

**Context window is a constraint, not a feature.** It's the physical limit on what the agent can see at any moment. Everything else in this cluster is a strategy for managing that constraint.

**"Memory" conflates at least three different things:**
1. **What's currently in the context window** (working memory — ephemeral, lost when the session ends)
2. **What persists across sessions** (persistent memory — stored in files, databases, or external systems)
3. **The act of recalling something from storage into the context window** (retrieval)

When someone says "my agent has memory," you need to ask: does it remember things within a single conversation (working memory / context window), does it remember things across conversations (persistent storage), or does it actively go find relevant information when it needs it (retrieval)?

**Retrieval is the mechanism, not the memory itself.** RAG, vector search, file reads, API calls — these are all retrieval strategies. They move information from persistent storage into the context window. The retrieval strategy you choose affects latency, relevance, and token cost, but the underlying problem is the same: the agent needs something that isn't currently in its context window.

**"Just-in-time context" and "context engineering" are strategy-level concepts.** They describe *how you design* the flow of information into the context window, not any specific piece of technology. The core principle: don't load everything upfront; pull in what's relevant when it becomes relevant. This is a response to the context window constraint — you can't fit everything, so you need to be intentional about what goes in and when.

**Checkpoints and stores are persistence primitives.** LangGraph's checkpoints (save/resume state within a workflow) and stores (cross-thread persistent data) are specific implementations of persistent memory. They matter because they answer: "if the agent crashes or the session ends, what survives?"

## How major ecosystems use this

### OpenAI
Conversation history is the primary "memory." No built-in persistent memory system. Long conversations exceed the context window; users manage this themselves. Thread-based conversation is available in the Assistants API with some state management.

### Anthropic
Explicit "memory tool" using file-directory storage. Formal guidance on "context engineering" as a practice: just-in-time loading, progressive disclosure, file-gated access. Memory files (`CLAUDE.md`) are discovered and loaded based on file system location. The strategy layer is well-documented.

### LangChain / LangGraph
Rich persistence infrastructure: checkpointers (save/resume), thread-based conversations, cross-thread memory stores. Documentation explicitly addresses the problem of long conversations exceeding context windows. Memory is treated as an architectural layer, not a bolt-on.

### CrewAI
Automatic memory system: extracts facts from conversations and injects recalled context before tasks. More opinionated than other frameworks — memory happens automatically rather than being explicitly managed.

## Why the distinction matters in practice

The most common failure: building an agent that "has memory" (persistent storage) but runs out of context window mid-conversation because too much was loaded upfront. The fix isn't more memory — it's better context engineering (load less, retrieve on demand).

The second most common failure: assuming the agent "remembers" something because it was discussed three turns ago, when in fact it was pushed out of the context window by subsequent tool outputs. Context window management is not intuitive — what the model "sees" changes dynamically.

## Examples

### Pattern in action
A project management agent needs to: (1) know the user's name and preferences (**persistent memory** — loaded at session start), (2) understand the current task (**working context** — the conversation so far), (3) find relevant project history when the user asks about a past decision (**retrieval** — search project docs on demand), and (4) not fill the context window with all project history upfront (**context engineering** — just-in-time loading).

### Anti-patterns / confusion traps
- Loading all persistent memory into context at session start. This fills the context window before the conversation even begins.
- Assuming "RAG" solves the memory problem. RAG is a retrieval strategy; you still need to decide what to retrieve, when, and how much context window to allocate to it.
- Treating "memory" as a single system. An agent needs working memory (context window management), persistent memory (what survives across sessions), and retrieval (how to find things). These are three separate design decisions.

## Evidence level

- **Established terms:** "context window" (universal), "retrieval" (universal), "checkpoint" (LangGraph-specific but well-defined)
- **Fragmented terms:** "memory" (at least 3 different meanings), "context engineering" (Anthropic-led, not universal), "just-in-time context" (Anthropic-specific)
- **Inferred patterns:** The three-layer model (context window constraint → persistence strategy → retrieval mechanism) is an ACON synthesis, not explicitly documented by any single ecosystem

## ACON recommendation

No consensus term exists for the full cluster. ACON documents the layers separately: **context window** (the constraint), **persistent memory** (what survives sessions), **retrieval** (how stored information enters context), and **context engineering** (the strategy for managing all three). When someone says "memory," ask which layer they mean.

## Related entries

- File-Based Instruction Patterns — one implementation of persistent memory and context loading
- Ephemeral vs Persistent Agent Identity — directly tied to whether agents carry memory across invocations
- Model Context Protocol (MCP) — provides standardized retrieval of external resources

## Changelog

- 2026-03-22: Initial entry
