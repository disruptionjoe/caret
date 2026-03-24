# Tool vs Skill vs Plugin

## Questions for Joe

- Should ACON recommend "tool" as the base-layer term (it has the strongest cross-ecosystem convergence) and treat "skill" and "plugin" as ecosystem-specific extensions? Or stay purely descriptive?
- The Cowork/Claude Code definition of "skill" (markdown instruction files with triggers) is architecturally different from LangChain's "skill" (dynamic bundles with tool registration). Should ACON explicitly call out that these share a name but are different concepts?
- Microsoft's rename from "skills" to "plugins" is well-documented. Should this be highlighted as a case study in the entry, or kept to a brief mention?
- Is MCP the resolution layer for this cluster? (i.e., "MCP may eventually standardize tool integration in a way that makes the tool/skill/plugin distinction less confusing") — or is that overclaiming?
- How much Cowork-specific detail should go in here? You use "skills" daily in a very specific way that differs from how most ecosystems use the word.

---

> A single capability that an agent can invoke — but the name for it changes by ecosystem, and the names carry different architectural assumptions.

## Status

Fragmented

## What problem this helps you think about

When you're deciding how to give an agent access to a new capability — say, web search, or a database query, or a formatting workflow — you'll encounter "tool," "skill," and "plugin" used almost interchangeably across different docs. But they aren't the same thing. Choosing the wrong abstraction affects how composable, portable, and maintainable your agent system is.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Tool | OpenAI, Anthropic, most frameworks | A discrete callable function — the agent sends structured input, gets structured output. Tools are the atomic unit. | OpenAI function calling docs; Anthropic tool-use docs |
| Function calling | OpenAI (historically) | The mechanism by which a model invokes a tool — essentially the protocol layer. Now converging with "tool calling" as the preferred term. | OpenAI function calling → tool calling rename |
| Skill | Anthropic (Cowork/Claude Code) | A markdown instruction file that defines a complete workflow or task approach. Skills are instructions, not callable functions. They shape behavior, not provide capabilities. | Cowork skill system documentation |
| Skill | LangChain | A dynamic bundle that can include tool registration, additional context, and behavioral configuration. Broader than a single tool; narrower than a full agent. | LangChain agent skills docs |
| Plugin | Microsoft (Semantic Kernel) | What was previously called a "skill" — renamed explicitly to align with OpenAI's plugin specification. Plugins package tools with metadata. | Microsoft Semantic Kernel docs; explicit "skills → plugins" rename |
| Plugin | Anthropic (Cowork) | An installable bundle of MCPs, skills, and tools. A distribution/packaging layer, not a capability layer. | Cowork plugin system |
| MCP Tool | Cross-ecosystem (via MCP spec) | A tool exposed through the Model Context Protocol — a standardized interface that makes tools portable across clients. | MCP specification |

## Key distinctions

The core confusion happens because "skill" and "plugin" operate at different levels of abstraction depending on the ecosystem, while "tool" is relatively stable.

**Tool is the base layer.** Across nearly all ecosystems, a "tool" means: a discrete callable function that takes structured input and returns structured output. The agent decides when to call it. The tool doesn't shape the agent's behavior — it extends the agent's capabilities. This is the most stable term in the cluster.

**"Skill" has two incompatible meanings.** In Cowork/Claude Code, a skill is a set of instructions — a markdown file that tells the agent *how to approach a task*, including triggers, constraints, and workflow steps. The agent doesn't "call" a skill the way it calls a tool; the skill reshapes the agent's behavior. In LangChain, a skill is a bundle — it can include tool registration, context injection, and behavioral defaults. Same word, different architecture.

**"Plugin" is a packaging concept.** In Semantic Kernel, plugin replaced skill as the name for packaged tools. In Cowork, a plugin is a distributable bundle that can contain multiple skills, tools, and MCP servers. In both cases, the plugin is a container, not a capability itself.

**MCP cuts across all three.** The Model Context Protocol standardizes how tools (and resources, and context) are exposed to agents regardless of what the host ecosystem calls them. MCP tools are tools in the "discrete callable function" sense, but they're accessed through a standard protocol rather than a framework-specific API.

The practical distinction that matters most for design:
- **Tools** answer "what can the agent do?"
- **Skills** (Cowork sense) answer "how should the agent behave?"
- **Plugins** answer "how is this capability packaged and distributed?"
- **MCP** answers "how do different systems expose and consume capabilities portably?"

## How major ecosystems use this

### OpenAI
Uses "tool" and "function calling" (converging on "tool calling"). No "skill" concept. Plugins existed briefly as a consumer product feature (ChatGPT plugins) but were deprecated. Tools are the primary abstraction.

### Anthropic
Uses "tool" for callable functions (via the API). Uses "skill" in Cowork/Claude Code for markdown-based behavioral instructions. Uses "plugin" for distributable bundles containing skills + tools + MCPs. These three layers are architecturally distinct and deliberately named differently.

### LangChain / LangGraph
Uses "tool" for callable functions. Uses "skill" for dynamic bundles that include tools plus context. The "agent harness" framing positions skills as one component of a larger agent runtime that also includes orchestration, hooks, and infrastructure.

### Microsoft (Semantic Kernel)
Uses "plugin" (formerly "skill" — explicitly renamed). Plugins contain functions that the agent can call. The rename was motivated by alignment with an OpenAI plugin specification, making this one of the few documented cases of an ecosystem deliberately choosing to converge on shared naming.

## Why the distinction matters in practice

If you build an agent system and call everything a "skill," you'll confuse yourself when you try to port it to another ecosystem. Your Cowork skills (behavioral instructions) won't map to LangChain skills (tool bundles) even though they share a name. Similarly, if you read Microsoft docs about "plugins" and assume it means the same as Cowork plugins, you'll expect packaging/distribution behavior that isn't there.

The practical impact: when designing a system, decide separately what tools the agent needs (capabilities), what skills it should follow (behavioral instructions), and how those are packaged (plugins/distribution). These are three different questions even though the terms blur them.

## Examples

### Pattern in action
You're building a research assistant. It needs: (1) web search capability → that's a **tool**. (2) Instructions for how to evaluate sources and structure findings → that's a **skill** (Cowork sense). (3) A way to share the whole research-agent setup with your team → that's a **plugin**. And (4) a standard interface so the web search tool works across Claude, Cursor, and a custom app → that's **MCP**.

### Anti-patterns / confusion traps
- Treating "skill" as universal. If someone says "I built a skill for X," you need to ask which ecosystem — the architecture is different.
- Assuming plugins are always about distribution. In Semantic Kernel, a plugin is just a tool container with metadata — it doesn't necessarily imply distribution or marketplace semantics.
- Confusing MCP with a replacement for tools/skills/plugins. MCP is a protocol for exposing capabilities, not a replacement for the concepts themselves. You still need to decide what's a tool vs a skill vs a plugin — MCP just standardizes how tools are accessed.

## Evidence level

- **Established terms:** "tool" / "function calling" / "tool calling" — high cross-ecosystem convergence
- **Fragmented terms:** "skill" (two incompatible meanings), "plugin" (two different scopes)
- **Inferred patterns:** The three-layer model (capability / behavior / packaging) is an ACON inference, not something any single ecosystem documents explicitly

## ACON recommendation

ACON uses **"tool"** as the primary label for discrete callable capabilities because it has the strongest cross-ecosystem convergence. "Skill" and "plugin" are documented as ecosystem-specific terms with meanings that differ by platform. When writing cross-ecosystem documentation, prefer "tool" for capabilities and specify the ecosystem when using "skill" or "plugin."

## Related entries

- Model Context Protocol (MCP) — the standardization layer for tool integration
- File-Based Instruction Patterns — closely related to the "skill as behavioral instructions" concept
- Agent Harness — the runtime layer that hosts tools, skills, and plugins

## Changelog

- 2026-03-22: Initial entry
