# Harness Layering

## Notation

No new operators required. Handle through file organization, not syntax.

## What it does

Separates agent instructions into three distinct layers based on scope and portability.

**Platform harness** — instructions that exist because of where the agent runs. Tool bindings, UI constraints, file path conventions, scheduling mechanisms. Change the platform, change this layer. Everything else stays.

**Personal harness** — instructions that define who the agent is and how it behaves, regardless of platform. Decision frameworks, voice definitions, memory, principles, skill logic. Portable. Works identically in desktop app, CLI, API call.

**Project harness** — instructions scoped to specific task, project, or domain. Context relevant now but not forever. Project plans, domain rules, temporary constraints. Should not leak across projects.

## When to use it

When agent instruction files accumulate and boundaries disappear. When you need platform changes without rewriting everything. When old project context should not contaminate new work. When you want to know which rules are universal, which are platform-specific, which expire.

When building portable agent systems. When moving agents between platforms. When running the same agent on multiple projects.

## When not to use it

When a single well-organized file suffices. Small systems can layer with comments and sections without three literal files. Harness layering is principle, not file count requirement.

When layers will remain indistinguishable in practice. Over-engineering kills the pattern.

## Design notes

Rules accumulate fast. A rule gets added for a platform limitation. A constraint gets added because the agent made a mistake. A project detail gets added for context. Weeks later, the instruction file contains platform workarounds, core behavioral principles, project-specific details — all mixed.

Nobody knows which rules are universal, which are platform-specific, which expire when the project ends.

Result: changing platforms requires rewriting everything. Old project context contaminates new work. Platform bugs get misdiagnosed as behavioral problems.

Harness layering prevents this by making boundaries explicit before accumulation starts.

**Routing, not competition.** Platform harness routes into personal harness. Does not replace it. Personal layer wins on behavioral questions. Platform layer wins on capability questions.

**Determinism across platforms.** Personal and project layers should produce identical agent behavior regardless of platform. If switching platforms changes how agent reasons about problems (not just how it accesses tools), personal layer has platform leakage.

**Scope flows inward, not outward.** Platform harness knows about personal harness. Personal harness knows about project harness. Project harness does not know about platform. Prevents project-level instructions from making platform-specific assumptions.

Close analog in traditional software: OS-level config vs user-level config vs project-level config. `~/.bashrc` vs `.env` vs `project.toml`. Developers solved this for code. Agent builders have not solved it for instructions.

Most platforms do not expose harness layers explicitly. Claude Code uses single-layer `CLAUDE.md`. Cursor uses single-layer `.cursorrules`. OpenAI Assistants separates system prompt from thread instructions — two layers, not three. Custom frameworks mix system and personal, mix project and per-task. Three-layer model is implicit in well-architected systems but rarely named or enforced.

**Failure mode: platform leakage.** Instruction file references tools, paths, or UI elements that exist only in one platform. Agent moves to new platform, references break or produce confusing behavior.

**Failure mode: project leakage.** Instructions accumulated for Project A remain active during Project B. Agent applies outdated constraints, uses wrong voice, references irrelevant context.

**Failure mode: personal layer too thin.** Everything pushed to platform or project. Agent has no stable identity. Behaves differently depending on where it runs because nothing defines consistent core.

**Failure mode: over-engineering.** Three separate config systems with formal interfaces when one organized file suffices. Harness layering is principle, not requirement.

Relates to **Scope Constraint** — scope controls what an agent can do on a run; harness layers control what an agent is across all runs.

Relates to **Context Refresh** — when refreshing across platform changes, preserve personal and project harnesses; reset only platform state to prevent leakage.

The pattern is real. The terminology is working. The principle is simple: know which layer you are editing. Do not let them bleed.
