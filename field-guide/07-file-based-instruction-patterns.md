# File-Based Instruction Patterns

## Questions for Joe

- This cluster is where ACON's own EA system (skills as markdown files, index.json routing, ea-os SKILL.md) is a direct real-world example. Should the entry reference your system as a practitioner example, or keep it ecosystem-focused?
- "Markdown-native control" from your existing glossary is basically this concept. Should it stay as a separate design philosophy term, or get absorbed into this cluster?
- The DSL research positions ACON Directives as something that would "compile into" these file-based surfaces. Should this entry explicitly set up that connection? Or keep it clean and let the PDN plan reference back?
- How much should this entry go into the specific file conventions (.cursorrules, CLAUDE.md, .cursor/rules)? These are concrete and useful, but they'll become outdated as conventions change. Balance specificity vs durability?
- "Mount" from your existing glossary describes making files accessible to agents. Is mounting a sub-concept within this cluster, or a separate emerging pattern?

---

> The practice of instructing agents through persistent files — markdown docs, rules files, memory files — that get loaded into context at session start or on demand. A rapidly growing practice class that doesn't yet have a cross-tool name.

## Status

Fragmented (rapidly adopted across ecosystems, but each ecosystem names it differently)

## What problem this helps you think about

When you want an agent to behave consistently across sessions — follow the same coding style, apply the same review criteria, remember the same project conventions — you need persistent instructions that survive beyond a single conversation. The solution that's emerging across ecosystems is the same: write instructions in structured files, and have the agent load them into its context window automatically or on demand.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Rules / rules files | Cursor | Persistent instruction files stored in `.cursor/rules/`. Project-scoped, user-scoped, or auto-applied. Loaded into model context at session start. | Cursor rules documentation |
| CLAUDE.md / memory files | Anthropic (Claude Code) | Markdown files discovered at project root and subdirectories. Support recursive loading, `@` imports (with depth limits), and a `#` shortcut for quick additions. | Claude Code memory docs |
| .cursorrules | Cursor (legacy) | Earlier convention (now deprecated in favor of `.cursor/rules/`). A single file in the repo root with project-wide instructions. | Cursor docs (marked legacy) |
| Skills (as files) | Anthropic (Cowork) | Markdown files with frontmatter that define task-specific behavioral instructions. Loaded when triggered by message patterns. | Cowork skill system |
| System instructions | General | The initial prompt that configures an agent's behavior. In file-based systems, this gets externalized from code into editable documents. | General usage across ecosystems |
| Agent configuration | Various frameworks | Structured config (YAML, JSON, or markdown) that defines agent behavior, tools, and constraints. Less human-readable than markdown-native approaches. | Various framework docs |

## Key distinctions

**The core pattern is the same everywhere:** take instructions that would normally be in a system prompt and externalize them into files that can be version-controlled, edited by humans, and loaded automatically.

**What differs is the loading mechanics:**
- **Always loaded:** Some files are loaded into every session regardless (Cursor's "always apply" rules, root-level CLAUDE.md)
- **Conditionally loaded:** Some files are loaded only when relevant (Cursor's path-scoped rules, CLAUDE.md in subdirectories loaded only when files in that subtree are read)
- **Trigger-loaded:** Some files are loaded when a specific pattern matches (Cowork skills triggered by message content)
- **Manually loaded:** Some files are loaded on explicit request (user says "load the review instructions")

**What also differs is the composition model:**
- **Flat:** One file per scope level, no imports (simpler, more predictable)
- **Import-based:** Files can reference other files (`@` imports in CLAUDE.md, with depth limits for safety)
- **Hierarchical:** Files at different directory levels compose automatically (CLAUDE.md at root + CLAUDE.md in subdirectory)

**The key design trade-off is power vs predictability.** Import-based systems are more expressive but harder to debug ("why is my agent behaving this way? which file is it loading?"). Flat systems are limited but transparent.

**This cluster connects directly to the PDN opportunity.** The ACON Directive Language research positions its value proposition here: if every ecosystem has file-based instructions but with different formats, conventions, and loading mechanics, a portable notation that compiles into these different surfaces would solve the "write once, use everywhere" problem.

## How major ecosystems use this

### Cursor
Rich rules system: project rules in `.cursor/rules/`, user rules, memory files. Rules have metadata (description, glob patterns for auto-apply, tags). Contents are included at the start of model context. This is the most structured implementation — rules are typed, scoped, and discoverable.

### Anthropic (Claude Code)
CLAUDE.md files discovered recursively from the project root. Support `@file` imports with a maximum depth. A `#` shortcut adds content to memory from the conversation. The `/memory` command shows what's loaded. Less structured than Cursor's rules, but simpler and more Markdown-native.

### Anthropic (Cowork)
Skills are markdown files with YAML frontmatter (name, description, triggers). Loaded when message patterns match the trigger description. Skills can call other skills and tools. More dynamic than rules files — behavior changes based on what the user says.

### General practice
Many teams create a `AGENTS.md`, `CONVENTIONS.md`, or similar file at the repo root as a lightweight version of this pattern — human-readable instructions that agents can reference. Less formal than Cursor or Claude Code's system, but the same underlying concept.

## Why the distinction matters in practice

Without file-based instructions, you re-explain your preferences every session. With them, the agent starts each session already knowing your project's conventions, style, and constraints. The difference in productivity is significant — especially for teams where multiple people interact with the same agent.

The main risk: file-based instructions can rot. If conventions change but the instruction files don't get updated, the agent follows outdated rules. Maintenance is part of the practice.

## Examples

### Pattern in action
A development team uses: (1) A root-level CLAUDE.md with coding standards, testing conventions, and PR review criteria. (2) Subdirectory-specific CLAUDE.md files with module-specific context (e.g., the API directory's file explains the authentication approach). (3) A Cursor rules file that auto-applies when editing TypeScript files, enforcing type-checking preferences. The agent loads the relevant files based on what code the developer is working on.

### Anti-patterns / confusion traps
- Writing instruction files that are too long. If the file exceeds what fits comfortably in the context window alongside the actual work, it becomes counterproductive — the instructions crowd out the content.
- Not maintaining instruction files. Outdated instructions are worse than no instructions — the agent confidently follows wrong conventions.
- Duplicating instructions across files without a single source of truth. When conventions change, you need to update everywhere — imports/references solve this.

## Evidence level

- **Established terms:** "rules files" (Cursor-specific), "CLAUDE.md / memory files" (Anthropic-specific), "system instructions" (general)
- **Fragmented terms:** No cross-ecosystem name for the practice class itself. Each ecosystem has its own file conventions.
- **Inferred patterns:** "File-based instruction patterns" as a named practice class is an ACON framing. The underlying pattern is documented across ecosystems but not unified under a single label.

## ACON recommendation

No consensus term exists for this practice class. ACON uses **"file-based instruction patterns"** as a working label for the practice of externalizing agent behavioral instructions into persistent, editable files. When implementing, the key decisions are: loading mechanics (always vs conditional vs triggered), composition model (flat vs imports vs hierarchical), and maintenance cadence.

## Related entries

- Tool vs Skill vs Plugin — skills (Cowork sense) are a specific type of file-based instruction
- Memory vs Context Window vs Retrieval — file-based instructions are one way information enters the context window
- Model Context Protocol (MCP) — MCP resources can serve as another source of agent instructions

## Changelog

- 2026-03-22: Initial entry
