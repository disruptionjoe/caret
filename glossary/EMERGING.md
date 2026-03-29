# Emerging Terminology

Concepts with real patterns observed in practice but unstable or absent terminology. Each entry describes what the pattern does, where it appears, what would be needed to graduate to canon.

---

## Fresh-Eyes Review Loop

**Status:** Working label. Real pattern, independently implemented, no consensus name yet.

### What It Describes

Spawning a new agent instance to review work produced by a previous agent — deliberately without giving the reviewer access to the working agent's reasoning, drafts, or intermediate steps. The reviewer sees only the output.

### Why It Matters

Agents that work on something for a long time accumulate context bias. They stop questioning assumptions made early. They develop blind spots around compromises accepted. A fresh reviewer with no knowledge of the creative process catches what the working agent can't see.

This is not the same as "have another agent review it." The distinction is in the isolation: the reviewer starts with a clean context, sees only what an external user would see, and evaluates on fresh grounds.

### Where It's Been Observed

- Practitioner implementations that explicitly strip prior iterations before review, creating "fresh eyes" on each pass
- Coding workflows where a separate subagent reviews code without access to the conversation that produced it
- Multi-agent systems where a "critic" agent operates independently of the "creator" agent
- Actor-critic patterns from reinforcement learning, adapted to LLM workflows
- The Three-Lens Review pattern in agent operations systems (technical review + user perspective + implementation perspective, each in isolation)

### How It Works

1. An agent produces work (draft, code, analysis, plan, research synthesis)
2. A new agent instance is spawned — fresh, with no inherited context from the working agent
3. The reviewer receives only the output and the evaluation criteria
4. The reviewer provides feedback
5. The original agent (or a new instance) incorporates feedback and revises
6. Optionally: the cycle repeats with fresh reviewers each time

### Key Design Decisions

**How many cycles?**
- One pass catches obvious issues
- Two catches deeper problems
- Beyond three: diminishing returns unless the task is very high-stakes

**Same expertise or different perspectives?**
- A reviewer with the same expertise catches technical errors and omissions
- A reviewer with a different perspective (user, critic, domain expert) catches different classes of issues (usability, missing context, tone, edge cases)
- Optimal: multiple reviewers with different mental models

**What does the reviewer see?**
- Just the output? Clean and unbiased, but may lack necessary context for useful critique
- The output plus original requirements? More relevant, but risks viewer assumptions
- The output plus requirements plus evaluation rubric? Focused critique, but most structure
- The output plus prior feedback? Tracks iteration, but reintroduces some original agent bias

The design choice depends on the task. A code review needs some context about requirements. A writing review might be better with just the output.

### Naming Variants Observed in Practice

- "Fresh eyes review" — most common informal usage
- "Fresh context review" — emphasizes the context reset
- "Independent review loop" — emphasizes isolation from the working agent
- "Clean-room review" — borrows from hardware testing terminology
- "Blind review" — sometimes used but conflicts with blind peer review meaning
- "Context-isolated review" — more technical
- No single term has achieved consensus

### Evidence Level

- Practitioner repos documenting the pattern of stripping iterations for review cycles
- "Fresh eyes" subagent reviewers appearing in multiple independent coding workflow implementations
- Actor-critic adaptation patterns in LLM-based multi-agent systems
- Observed in 2-3 independent practitioner codebases
- The pattern is real and implemented independently by multiple practitioners
- The pattern works and produces observable value
- But no consolidated community documentation or shared terminology yet

**Current Evidence:** Low-medium.

### What Would Promote It to Canon

- **Ecosystem adoption:** One or more major frameworks (LangGraph, LangChain, Semantic Kernel) implementing this as a named pattern
- **Convergence:** The field settles on a single term (likely "fresh-eyes review" because it's already the most common informal usage)
- **Research:** Published evidence showing measurable improvement from fresh-eyes review vs single-pass review in agent workflows
- **Integration:** Appears in official documentation and tutorials as a recommended pattern, not just practitioner workarounds

### Related Terms

- Ephemeral vs Persistent Agent Identity — fresh-eyes review depends on creating ephemeral agent instances with clean context
- Guardrails and Validation — fresh-eyes review is a specific implementation of a critique and validation loop
- Orchestrator vs Router vs Supervisor — the orchestrator decides when to trigger a review and manages the feedback cycle

---

## Context Mount

**Status:** Working label. Pattern is real in emerging architectures, niche adoption, will likely merge with MCP resources.

### What It Describes

Making a data source, folder, or context module available to an agent through a filesystem-like interface — "mounting" it the way an operating system mounts a drive. When a context source is mounted, the agent can read from it. When it's unmounted, the information is invisible.

### Why It Matters

As agent systems become more complex, "what can this agent see?" becomes a design decision, not an accident. Context mounts provide a clean metaphor for controlling agent visibility and information flow. Mount the project docs for a project-focused session, unmount them when switching tasks. Mount a user profile for personalized behavior, keep it unmounted for anonymous processing.

This distinction matters for:
- **Security:** What is this agent authorized to see?
- **Focus:** Reduce noise by mounting only relevant context
- **Isolation:** Prevent accidental data leakage across sessions

### Where It's Been Observed

- Agent filesystem work and tooling that uses mounting metaphors for context sources
- Model Context Protocol (MCP) resources as "mountable" external data sources
- Cowork's folder mounting system — users select a folder, agent gains read/write access to it
- Claude Code's recursive CLAUDE.md discovery — files become "mounted" when their directory tree is accessed
- Emerging agent operating systems that treat context sources like mounted volumes

### How It Works

1. A context source (folder, documentation set, data file, configuration) is defined
2. The user or system explicitly "mounts" it for an agent or session
3. The agent can now access the mounted context through a consistent interface
4. When unmounted, the information is no longer visible to the agent
5. Mounts can be added or removed dynamically during a session

### Key Design Decisions

**Explicit vs automatic mounting?**
- Explicit: the user or developer decides what's mounted. More control, more overhead, requires awareness
- Automatic: the system mounts based on context or detection. Less friction, less visibility, harder to audit

Most production systems use explicit mounting for security reasons. Automatic mounting is useful in development.

**Read-only vs read-write?**
- Read-only mounts: reference docs, stable resources, things that shouldn't change
- Read-write mounts: working files, configuration that the agent might modify
- Mixed: some paths read-only, some writable

The distinction prevents accidental corruption of reference materials.

**Mount scope?**
- Session-scoped: lost when the session ends. Simplest, ephemeral
- Project-scoped: persists across sessions within a project. More useful, more complex
- Global: available across all sessions. Powerful, requires careful access control

Session-scoped is safest. Project-scoped is most practical. Global is rarely needed.

### Naming Variants Observed

- "Mount" / "mounted folder" — most common in agent tooling (filesystem metaphor)
- "Context source" — more generic, no metaphor implied
- "Workspace" — sometimes used for similar concepts but overloaded
- "Attachable context" — describes the behavior, not the mechanism
- "Resource" — in MCP terminology
- "Available context" — less specific
- No standard term for the abstract pattern

### Evidence Level

- Agent filesystem tooling actively using "mount" metaphors for context organization
- Model Context Protocol (MCP) defining "resources" as a standardized mounting mechanism
- Cowork's production folder mounting system used in working agent workflows
- Claude Code's implicit mounting through recursive file discovery
- Observed in 3-4 production systems and emerging architectures

**Current Evidence:** Low-medium. The pattern is real and useful in practice. It appears in multiple independent systems. But it's niche — not yet mainstream in agent design. Terminology has not converged.

### What Would Promote It to Canon

- **MCP convergence:** If MCP resources become the standard abstraction and the ecosystem settles on "resource" as the term, context mount might merge with that
- **Standardization:** Official documentation in one or more major frameworks that positions mounting as a first-class pattern
- **Practical evidence:** Real-world use cases showing clear value in explicit mounting (security audits, session isolation, performance)
- **Terminology convergence:** The field settles on a single term and stops using "workspace" and "context source" for different things

The term might not survive as-is. It could become "MCP resources" if that path dominates, or "mounted resources" if the filesystem metaphor becomes standard.

### Related Terms

- Model Context Protocol (MCP) — MCP resources serve the same function through a standardized protocol
- File-Based Instruction Patterns — file-based instructions are one type of mountable context
- Memory vs Context Window vs Retrieval — mounts are one mechanism for getting information into the context window

---

## Agent Identity Persistence

**Status:** Emerging. Terminology exists (ephemeral vs persistent) but applied inconsistently across ecosystems.

### What It Describes

Whether an agent instance maintains state and continuity across multiple turns or interactions. An ephemeral agent is created for a single task and discarded. A persistent agent remembers prior interactions and accumulates context.

### Why It Matters

The choice between ephemeral and persistent agents affects:
- **Handoff behavior:** Can the receiving agent access the prior agent's thinking?
- **Memory overhead:** Persistent agents grow heavier over time
- **Isolation:** Ephemeral agents are clean; persistent agents carry baggage
- **Specialization:** Ephemeral agents do one thing well; persistent agents accumulate expertise and bias

Most multi-agent systems use both. The design decision is often implicit. Making it explicit prevents mismatches.

### Where It's Been Observed

- Fresh-eyes review explicitly spawning ephemeral agents to avoid inherited bias
- Long-running assistants (persistent) that maintain conversation history
- Coordinator agents (often persistent) paired with worker agents (often ephemeral)
- Context cleanup patterns that explicitly destroy and recreate agent instances
- Agent operating systems that treat ephemeral and persistent as different resource classes

### How It Works

**Ephemeral:**
1. Agent instance is created for a specific task
2. It receives only the context needed for that task
3. It produces output
4. The instance is terminated and all state is discarded
5. If the same task needs to run again, a new instance is created fresh

**Persistent:**
1. Agent instance is created and remains active across multiple interactions
2. It accumulates context, conversation history, learned patterns
3. State is preserved between turns
4. The instance terminates only when explicitly ended or when the session closes
5. Restarting the same persistent agent resumes from prior state

### Key Design Decisions

**Retention scope for persistent agents?**
- Single session: persists within one conversation, lost at session end
- User-lifetime: persists across sessions for the same user
- Project-lifetime: persists across users and sessions for a single project
- Global: persists indefinitely

The choice affects memory overhead, security boundaries, and complexity.

**When to spawn ephemeral vs persistent?**
- Ephemeral for specialized tasks, isolated operations, fresh-perspective work
- Persistent for coordination, continuity, relationship-building
- Hybrid systems pair persistent orchestrators with ephemeral workers

### Naming Variants Observed

- "Ephemeral" / "persistent" — most standard terminology but applied loosely
- "Stateless" / "stateful" — sometimes used but confuses protocol-level with architectural-level state
- "Session-scoped" / "long-lived" — describes scope, not agent property
- "Disposable" / "anchored" — used in some frameworks (Caret^ uses `^^` change hat / `^^^` change worker instead)
- "Fresh instance" / "reused instance" — descriptive but not standard

The terminology exists but is applied inconsistently. The same term means different things in different frameworks.

### Evidence Level

- Widely observed in production multi-agent systems
- Terminology exists but is applied inconsistently across ecosystems
- Design decisions are often implicit rather than explicit
- Patterns like fresh-eyes review depend on this distinction

**Current Evidence:** Medium. The pattern is ubiquitous but the terminology is fragmented.

### What Would Promote It to Canon

- **Consistent definition:** Ecosystem settles on single meaning for "ephemeral" and "persistent" across frameworks
- **First-class abstraction:** Major frameworks make this an explicit design choice in their APIs and documentation
- **Best-practice guidance:** Published guidance on when to use ephemeral vs persistent, tradeoffs and implications
- **Architecture patterns:** Documented patterns that combine ephemeral and persistent agents effectively

### Related Terms

- Fresh-Eyes Review Loop — depends on ephemeral agent instances with clean context
- Context Mount — affects what state is available to persistent agents
- Handoff / Delegation / Transfer — different behavior depending on agent persistence

---

## Scope and Iteration

These emerging concepts represent real solutions to real problems that the agent ecosystem is actively working on. They are not yet standardized, but they are not accidents either — they emerge because they solve something that matters.

**Fresh-eyes review** solves the problem of context bias in long-running agent work.
**Context mounts** solve the problem of managing information visibility and scope in complex agent systems.
**Agent identity persistence** solves the problem of balancing continuity with isolation.

Watch for these patterns to either converge on standard terminology, merge into existing frameworks (especially MCP), or remain niche solutions for specific architecture choices. Either way, they are worth understanding now.
