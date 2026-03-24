# Model Context Protocol (MCP)

## Questions for Joe

- MCP is the most "settled" entry in the field guide — it's a formal spec, not a fragmented concept. The value here is explaining how MCP relates to all the other clusters (tools, skills, plugins, memory, file-based instructions). Is that the right angle, or should this entry focus more on MCP itself?
- The research suggests ACON should decide whether MCP is (a) just a glossary entry, (b) a cross-cutting organizing axis, or (c) background context. I've drafted it as (b) — the entry that ties the other clusters together. Agree?
- How deep into MCP's technical details (resources, prompts, tools as MCP primitives) should this go? The audience ranges from "what is MCP?" to "I know MCP but don't understand how it relates to these other concepts."
- MCP is evolving fast. Should this entry include a "current state" section that acknowledges how quickly things are changing, or just document the stable parts?
- OpenAI's framing of MCP as "USB-C port for AI" is catchy and accurate. Use it, or avoid amplifying one company's marketing framing?

---

> An open protocol that standardizes how AI applications connect to external tools, resources, and context — increasingly the shared infrastructure layer that cuts across ecosystem-specific naming.

## Status

Established (new) — formal specification with rapid cross-ecosystem adoption

## What problem this helps you think about

When you're connecting an agent to external capabilities — databases, APIs, file systems, services — each framework has historically had its own way of doing it. MCP standardizes the interface: one protocol that lets any AI client connect to any tool/resource provider. If you're deciding how to expose capabilities to agents, MCP is the question of "should I build a framework-specific integration, or an MCP server that works everywhere?"

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Model Context Protocol (MCP) | Anthropic (origin), cross-ecosystem | An open protocol defining how LLM clients connect to external tools, resources, and context. Specifies a standard interface for servers (capability providers) and clients (AI applications). | MCP specification; Anthropic announcement |
| MCP Server | MCP spec | A service that exposes tools, resources, and/or prompts through the MCP protocol. Any external capability can be wrapped as an MCP server. | MCP specification |
| MCP Client | MCP spec | An AI application that connects to MCP servers to use their capabilities. Claude, Cursor, and other tools are MCP clients. | MCP specification |
| MCP Tool | MCP spec | A callable function exposed through MCP — equivalent to a "tool" in other ecosystems but accessed through a standardized protocol. | MCP specification |
| MCP Resource | MCP spec | Data or context exposed through MCP — documents, files, database records, or other information the agent can read but doesn't "call" like a tool. | MCP specification |
| MCP Prompt | MCP spec | A reusable prompt template exposed through MCP — pre-built instructions that can be invoked by the client. | MCP specification |

## Key distinctions

**MCP is a protocol, not a framework.** It doesn't replace tools, skills, plugins, or orchestration frameworks. It standardizes how capabilities are exposed and consumed across all of them. Think of it as the interface layer that sits between the agent and its capabilities.

**MCP has three primitive types:**
1. **Tools** — callable functions (the agent sends input, gets output back). This is what most people mean when they say "MCP."
2. **Resources** — readable data (documents, files, records). The agent can read them for context but doesn't "call" them.
3. **Prompts** — reusable instruction templates. Less commonly discussed but relevant for standardizing behavioral instructions across clients.

**MCP's relationship to this field guide's other clusters:**
- **Tool vs Skill vs Plugin:** MCP standardizes the "tool" layer. MCP tools are the portable version of ecosystem-specific function calling. Skills and plugins are higher-level abstractions that may use MCP tools underneath.
- **Memory vs Context vs Retrieval:** MCP resources provide a standardized way to expose persistent data that agents can retrieve. This is one implementation of "just-in-time context" — the agent retrieves MCP resources when it needs them rather than loading everything upfront.
- **File-Based Instruction Patterns:** MCP prompts could potentially standardize how behavioral instructions are exposed across tools, though this is early.
- **Handoff / Delegation:** When agents hand off to each other, MCP provides the shared tool layer that both agents can access — tools don't need to be re-registered for each agent.

**The "USB-C port" analogy** (widely used, originally from OpenAI's framing): just as USB-C standardizes the physical connection between devices and peripherals, MCP standardizes the connection between AI applications and capability providers. You build your capability as an MCP server once, and any MCP client can use it.

## How major ecosystems use this

### Anthropic
MCP originator. Claude Code, Claude Desktop, and Cowork are MCP clients. Deep integration — MCP is the primary way to extend Claude's capabilities beyond its built-in tools. The ecosystem includes an MCP registry for discovering available servers.

### OpenAI
Has adopted MCP compatibility. Framed as the "USB-C port for AI applications." Integration is newer than Anthropic's but signals cross-ecosystem convergence.

### Cursor
MCP client support. Users can connect MCP servers to extend Cursor's capabilities. Combined with Cursor's existing rules/tools system.

### LangChain / LangGraph
Support for MCP as a tool source. MCP tools can be integrated into LangChain chains and LangGraph workflows alongside framework-native tools.

### Community
Growing ecosystem of community-built MCP servers for common services (databases, APIs, SaaS tools). The standardization means a server built for one client works with all of them.

## Why the distinction matters in practice

If you're building a capability that agents should use, building an MCP server makes it available to every MCP client — Claude, Cursor, and any other tool that supports the protocol. Building a framework-specific integration (only for LangChain, only for Claude) limits your reach.

If you're choosing how to connect tools to your agent, MCP servers give you portability — switch from one AI client to another without rebuilding integrations.

The main limitation: MCP is still early. Not all clients support all MCP features equally. Server quality varies. The protocol is evolving. But the trajectory is toward MCP as the standard integration layer.

## Examples

### Pattern in action
You build a company knowledge base MCP server that exposes: (1) a search **tool** (agents can search the knowledge base), (2) document **resources** (agents can read specific documents), and (3) a "research" **prompt** template (a pre-built instruction for how to research topics using the knowledge base). This server works with Claude Code, Cursor, and any other MCP-compatible client without modification.

### Anti-patterns / confusion traps
- Treating MCP as a replacement for skills/plugins. MCP standardizes capability access, not behavioral instructions or packaging. You still need skills for behavior and plugins for distribution.
- Assuming all MCP servers are equal quality. Community MCP servers vary widely in reliability, security, and completeness. Evaluate before trusting with production data.
- Over-investing in framework-specific integrations when MCP could provide portable coverage. Before building a custom LangChain tool, check if an MCP server already exists.

## Evidence level

- **Established terms:** "Model Context Protocol" / "MCP" (formal spec, cross-ecosystem adoption), "MCP Server" / "MCP Client" / "MCP Tool" (spec-defined)
- **Established relationship:** MCP as a standardization layer for tool integration is documented and adopted
- **Inferred patterns:** MCP's role as a "terminology stabilizer" (the research's framing) and its positioning as the cross-cutting layer connecting other field guide clusters is an ACON interpretation

## ACON recommendation

ACON treats MCP as a **cross-cutting reference point** — the one emerging standard that is actively reducing naming fragmentation for tool/context integration. When discussing tools, skills, plugins, or capability integration, MCP provides a useful anchor: "is this capability exposed through MCP (portable), or through a framework-specific interface (locked in)?"

## Related entries

- Tool vs Skill vs Plugin — MCP standardizes the tool layer
- Memory vs Context Window vs Retrieval — MCP resources enable standardized retrieval
- File-Based Instruction Patterns — MCP prompts could extend to standardized instructions
- Handoff / Delegation — MCP provides shared tool access across agents

## Changelog

- 2026-03-22: Initial entry
