# Platform Starters

If you want Caret^ to stick, install it at the platform layer.

Not one chat.
Not one task.
The platform.

## Start Here

Use `/platform/caret-core-starter.md`.

That is the default path.

It gives you the smallest working install with the strongest odds of stable load order.

Start there unless you already know you need a platform-shaped variant.

## Then Use These As Variants

- `claude-skill-starter.md`: for markdown skill systems and Claude-style `SKILL.md` flows
- `codex-shared-instructions-starter.md`: for Codex or shared-agent instruction layers
- `generic-harness-module-starter.md`: for custom harness repos and internal instruction loaders
- `plugin-loader-starter.md`: for platforms that can mount local or remote docs through a plugin or connector layer

## Recommendation

Use the simplest thing that gives you stable load order.

Best practical order:

1. `/platform/caret-core-starter.md`
2. platform-level skill or shared instructions shaped from that starter
3. harness module
4. plugin loader only if your platform actually supports stable mounted docs

If you are choosing cold:

1. start with the core starter
2. move to a platform-specific variant only when the platform needs a different wrapper shape
3. keep plugins last

Plugin or connector setup is useful when:

- your platform can mount local repo files or raw URLs cleanly
- the mounted docs can be loaded before task-specific skills
- the mounts are stable and read-only enough to act like canon

If your platform cannot guarantee those things, skip the plugin layer and use a normal skill or shared instruction file instead.

## Core Rule

No matter which starter you use:

- load `/caret-cheatsheet.md` first
- treat `/notation/` as canonical support
- treat examples, patterns, and research as downstream
- keep fenced code blocks literal
- let live repo canon outrank drafts, archives, and external material
