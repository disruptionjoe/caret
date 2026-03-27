# Claude-Style `SKILL.md` Starter

Use this when your platform reads Markdown skill files.

Use `/platform/caret-core-starter.md` first.

This file is the Claude-shaped wrapper around that core install.

## How To Use It

1. Create or update your platform-level `SKILL.md`.
2. Put this block near the top, before task-specific skill rules.
3. If your platform can read local files, point it at `/caret-cheatsheet.md`.
4. If not, paste the full cheatsheet directly under the starter block.

## Starter

```markdown
# Caret^ Core

Load `caret-cheatsheet.md` as the active semantic signal layer for Markdown instructions.

## Source Of Truth

1. `caret-cheatsheet.md`
2. local `notation/` docs when present
3. local glossary support when needed
4. examples, patterns, and research only if they agree with canon

## Core Meanings

- `^` = directive
- `^^` = hat, same worker
- `^^^` = worker boundary
- `^^^^` = fresh-eyes boundary

## Operating Rules

- indentation scopes downward
- fenced code blocks are literal
- if downstream or imported material conflicts with canon, canon wins
- prefer exact repo-relative targets when precision matters
- do not infer new syntax from examples

## Load Rule

Load Caret^ before task-specific skills.

If file loading is not available, inline the full contents of `caret-cheatsheet.md` below this section.
```

## Smoke Test

After installing, run:

```text
^^reviewer ^depth7
  Review this paragraph for weak claims.
```

```text
^^^planner ^depth8
  Give me a 3-step launch plan.
```
