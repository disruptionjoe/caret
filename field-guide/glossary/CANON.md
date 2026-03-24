# ACON Glossary

A practical vocabulary for agentic systems. These terms cover what people encounter immediately when working with AI agents, plus new pattern language for concepts that exist in practice but haven't been clearly named.

---

## Foundational Terms

### Mount
When a folder, file, or data source is made accessible to an agent. A mounted folder means the agent can read and write to it. Unmounted = invisible to the agent.

### Context Window
The total amount of text (tokens) an agent can hold in working memory at one time. Everything the agent "knows" during a conversation lives here. When it fills up, older content gets pushed out or compressed.

### Spawn
Creating a new agent instance — either a sub-agent within a workflow or a fresh agent session. Spawning can be ephemeral (stateless) or anchored (with persistent context).

### Harness
The platform or environment that hosts and runs the agent. Examples: Claude Code, Cursor, a custom API wrapper. The harness provides the agent's capabilities, tool access, and execution environment.

### Skill
A reusable, self-contained set of instructions that an agent can load and follow for a specific task. Skills are typically Markdown files that define what the agent should do, how, and with what constraints.

### Agentic Loop
The core cycle an agent runs: receive input → reason → act (use tools, write files, call APIs) → observe results → reason again. The loop continues until the task is complete or a stopping condition is hit.

### Inference
A single pass through the model — one "thinking step." Each time the model generates a response, that's one inference. Workflows may involve many inferences chained together.

### Eval
Evaluating an agent's performance or outputs. Can be automated (test suites, scoring functions) or human (reviewing quality, accuracy, tone). Essential for knowing whether a system actually works.

### Temperature
A setting that controls how creative or conservative the model's outputs are. Low temperature = more predictable, focused, deterministic. High temperature = more exploratory, varied, creative. In Caret^ notation: `^temp0`–`^temp9`.

### Grip
How tightly the output commits to a specific recommendation. Controls authority posture — how directive vs. exploratory the response is. Orthogonal to temperature (creative range) and depth (thoroughness). Loose grip = open hand, options can move. Tight grip = locked in, nothing moves. In Caret^ notation: `^grip0` (pure exploration, only questions) through `^grip9` (exact spec, no hedging). Not the same as temperature: you can be creative and non-prescriptive (`^temp7 ^grip2`) or conservative and highly prescriptive (`^temp2 ^grip9`).

### Token
The basic unit of text that language models process. Roughly 3/4 of a word. Important because context windows, costs, and speed are all measured in tokens.

---

## Agent Workflow Terms

### Action
A discrete thing an agent does — running a command, calling an API, writing a file, searching the web. Actions are the "doing" part of the agentic loop.

### API Call
When an agent communicates with an external service. Could be a database query, a web request, a tool invocation, or a call to another model.

### Workflow
A structured sequence of steps an agent follows to accomplish a goal. Can be linear, branching, or looping. Workflows often involve multiple skills, tools, and decision points.

### Trigger
The event or condition that starts a workflow or activates a skill. Can be user input, a schedule, a file change, or another agent's output.

### Queue
A waiting line for tasks or messages. Agents may queue work when they can't process everything simultaneously, or when tasks need to run in a specific order.

### Validation
Checking that an agent's output meets defined criteria before proceeding. Can be structural (is the JSON valid?), semantic (does the answer make sense?), or procedural (did it follow the right steps?).

### Escalation
When an agent determines it cannot or should not handle something and passes it to a human or a more capable agent. Good escalation design prevents agents from failing silently.

### Fallback
A backup behavior when the primary approach fails. Example: if the API is down, use cached data. If the model can't answer, ask the user for clarification.

### Checkpoint
A saved state that allows a workflow to resume from a known point. Critical for long-running processes that might be interrupted, time out, or need human review mid-stream.

---

## Pattern Language — Spawning and Personas

### Ephemeral Spawning
Creating a sub-agent with no prior context — a completely fresh perspective. The spawned agent has no memory of previous interactions, decisions, or reasoning. Used when you want unbiased "fresh eyes."

### Anchored Spawning
Creating a sub-agent that inherits or loads specific context — memory, principles, prior decisions, history. The spawned agent has continuity with past work. Used when consistency and institutional memory matter.

### Perspective Matrix
Spawning multiple agents with different domain perspectives to review the same thing from different angles. Example: having a product manager, engineer, and end user persona each evaluate a feature design.

### Cognitive Forking
Splitting a reasoning process into parallel tracks, each exploring a different approach or assumption. Unlike a perspective matrix (which varies the reviewer), cognitive forking varies the reasoning path.

### Persona Panel
A structured set of personas that review or evaluate something in sequence or parallel. Similar to a perspective matrix but formalized — the panel has defined roles, each with specific evaluation criteria.

### Fresh-Eyes Loop
The practice of spawning a new persona of the same type to re-evaluate something without the accumulated context bias of the previous instance. Used to catch blind spots that develop when an agent has been working on something too long.

### Persona Refresh Cycle
A systematic pattern of periodically replacing an active persona with a fresh instance. Prevents context drift and confirmation bias in long-running workflows.

---

## Orchestration Hierarchy

### Primary Orchestrator
The top-level orchestrator built into the harness/platform. This is the system's native coordination layer — it manages the overall conversation, tool access, and execution flow. You don't build it; it comes with the platform.

### Chief of Staff
A reusable anchored agent role that sits between the primary orchestrator and specialized sub-agents. The chief of staff decides which personas to bring in, when, and in what order. Individual skills don't need to embed persona-selection logic — they delegate to the chief of staff.

### Meta-Orchestrator
An orchestrator that coordinates other orchestrators. Relevant in complex multi-system setups where different platforms or harnesses need to work together.

---

## Design Philosophy

### Context Budgeting
Intentionally managing what enters the context window. Not everything should be loaded — context is a finite resource. Good context budgeting means loading only what's relevant for the current step.

### Selective Loading
Loading only the specific skill, file, or data branch needed for the current step. The opposite of "load everything and let the model figure it out."

### Prompt Compression
Using shorter, denser prompts that preserve quality while reducing token usage. Achieved through better structure, clearer instructions, and eliminating redundancy.

### Decision Routing
Using decision trees or lightweight branching logic to choose the next skill, file, or path. The agent doesn't reason about what to do next from scratch — a routing structure tells it.

### File-Gated Context
Making information available to the agent only when specific files or folders are loaded. Information the agent doesn't need stays invisible until it's relevant.

### Scripted Determinism
Offloading repeatable, predictable logic to scripts, indexes, or programs rather than making the model reason it out every time. If the answer is always the same, don't make the model think about it.

### Index-Mediated Access
Using a registry, index, or manifest as the agent's first stop so it can discover what exists without reading everything. The index tells the agent where to look; the agent reads only what it needs.

### Markdown-Native Control
Building agent systems primarily in Markdown so humans can read, edit, and audit them without needing YAML fluency or specialized tooling. Markdown is the lingua franca of human-AI collaboration.

### Branch-First Architecture
Structuring workflows around explicit branches and exit conditions before writing detailed step instructions. Define the decision tree first; fill in the leaves second.

### Token Frugality
A general principle of minimizing unnecessary token usage across the system — in prompts, in context loading, in output generation. Every token costs time, money, and attention.

### Sparse Context Design
Designing systems where the agent operates with minimal context by default and loads additional context only when needed. The opposite of "give the agent everything upfront."

### Human-Readable Orchestration
Designing orchestration logic that a non-technical person can read and understand. If a human can't follow the decision tree, the system is too complex.

---

## Model Selection

### Model Provenance
Where a model comes from — open source, proprietary, fine-tuned, distilled. Provenance affects licensing, control, auditability, and trust.

### Model Alignment
How well a model's default behavior matches the task requirements. A highly aligned model needs less prompting and fewer guardrails. Misaligned models require more scaffolding.

### Fine-Tuning Depth
How much a model has been specialized for a particular task or domain. Deeper fine-tuning = better at that specific thing, potentially worse at general tasks.

### Inference Cost
The computational and financial cost of running the model. Varies by model size, provider, token count, and speed requirements. Critical for production systems.

---

## Broader Framework Labels

These describe the overall design philosophy that ACON embodies:

### Markdown-Native Agent Design
Building agent systems using Markdown as the primary control surface. Human-editable, version-controllable, auditable.

### Sparse Context Orchestration
An architectural approach where agents operate with minimal context and load additional information only as needed, using indexes and routing to find what's relevant.

### Deterministic Agent Architecture
Designing agent systems where the structural flow is predictable and repeatable, even though the model's reasoning within each step is generative. Determinism in the scaffold, creativity in the execution.
