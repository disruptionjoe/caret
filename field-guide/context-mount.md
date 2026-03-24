# Context Mount

## Questions for Joe

- "Mount" is already in your existing ACON glossary as a foundational term. This emerging pattern entry is about the more specific concept of "attachable context volumes" — making arbitrary data sources accessible to agents through a filesystem-like metaphor. Should the existing glossary term be updated, or is this a distinct concept?
- This is closely related to MCP resources (standardized external data access). Is "mount" just a friendlier metaphor for MCP resources, or is there a meaningful architectural distinction?
- The research says evidence is "low-medium" — real in emerging architectures but niche. Is it worth including now, or should it wait for more evidence?

---

> ⚠️ EMERGING PATTERN — This describes a real practice that does not yet have a stable community name. The label "Context Mount" is a working label that extends ACON's existing "mount" concept. Expect this entry to evolve.

## The pattern

Making a data source, folder, or context module available to an agent through a filesystem-like interface — "mounting" it the way an operating system mounts a drive. When a context source is mounted, the agent can read from it. When it's unmounted, the information is invisible.

## Why it matters

As agent systems become more complex, the question of "what can this agent see?" becomes a design decision, not an accident. Context mounts provide a clean metaphor for controlling agent visibility: mount the project docs for a project-focused session, unmount them when switching tasks. Mount a user profile for personalized behavior, keep it unmounted for anonymous processing.

## Where it appears

- Agent filesystem work and tooling that uses mounting metaphors for context sources
- MCP resources as "mountable" external data
- Cowork's folder mounting system (user selects a folder → agent can read/write it)
- Claude Code's recursive CLAUDE.md discovery (files become "mounted" when their subtree is accessed)

## Key design decisions

- **Explicit vs automatic mounting?** Should the user/developer decide what's mounted, or should the system auto-mount based on context?
- **Read-only vs read-write?** Some mounts should be read-only (reference docs). Others should be writable (working files).
- **Mount scope?** Is a mount session-scoped (lost when the session ends), project-scoped (persists across sessions within a project), or global?

## Naming variants observed

- "Mount" / "mounted folder" (most common in agent tooling)
- "Context source" (more generic)
- "Workspace" (sometimes used for the same concept but overloaded)
- No standard term for the abstract pattern of "attachable context volumes."

## Evidence

- Agent filesystem tooling using "mount" metaphors
- MCP resource model (external data exposed to agents)
- Cowork's folder mounting system
- Evidence level: Low-medium. The pattern is real but the specific framing as "context mounts" is niche.

## Status: Working label

"Context Mount" extends ACON's existing "mount" term into a more specific architectural pattern. It may be absorbed into the MCP ecosystem's vocabulary as "resources" or remain as a distinct concept for the agent filesystem metaphor. ACON will track adoption.

## Related entries

- Model Context Protocol (MCP) — MCP resources serve a similar function through a standardized protocol
- File-Based Instruction Patterns — file-based instructions are one type of mountable context
- Memory vs Context Window vs Retrieval — mounts are one way information enters the context window

## Changelog

- 2026-03-22: Initial entry as emerging pattern
