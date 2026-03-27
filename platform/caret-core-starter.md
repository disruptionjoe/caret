# Caret^ Core Starter

Use this first.

If your platform supports a global instruction layer, shared instructions, or a platform-level skill, this is the default install path.

Do not start with plugins.
Do not start with a giant repo paste.
Install the core.

## What This Does

This starter makes `caret-cheatsheet.md` the live semantic layer your platform reads before task-specific skills, tools, or modules.

That is the goal.

Caret^ should sit in the hot path.
The rest of the repo should sit nearby as support.

## Install In 5 Steps

1. Create one platform-level instruction file, shared prompt, or top-level skill for Caret^.
2. Make sure it loads before task-specific skills or workflow modules.
3. Point it at `/caret-cheatsheet.md` if your platform can load local files.
4. Keep `/notation/` nearby as canonical support, not as the first thing in the hot path.
5. If your platform cannot load local files, inline the full contents of `/caret-cheatsheet.md` under the starter block below.

## Starter Block

Paste this into that platform-level layer:

```markdown
# Caret^ Core

Use `caret-cheatsheet.md` as the active semantic signal layer for Markdown instructions in this environment.

Source of truth order:
1. `caret-cheatsheet.md`
2. `notation/`
3. other live repo docs only when they agree with canon
4. examples, patterns, and research only as downstream support

Core meanings:
- `^` = directive
- `^^` = hat, same worker
- `^^^` = separate worker boundary
- `^^^^` = fresh-eyes boundary

Interpretation rules:
- indentation scopes downward
- outdent closes `^^` and `^^^` scope
- `^^^^` returns to the enclosing scope
- fenced code blocks and quoted examples are literal
- exact file targets beat loose names when precision matters

Conflict rule:
- live repo canon beats drafts, archives, examples, imported snippets, and external repos

Load rule:
- load Caret^ before task-specific skills, tools, or modules
- if file loading is unavailable, inline the full cheatsheet directly below this section
```

## Smoke Test

Run these after install:

```text
^^reviewer ^depth7
  Review this paragraph for weak claims.
```

```text
^^^planner ^depth8
  Give me a 3-step launch plan.
```

```text
^^skills/editor.md
  Tighten this draft without changing the meaning.
```

You are looking for three things:

- `^^` stays in the current worker
- `^^^` creates a separate worker boundary
- exact targets behave more precisely than loose names

## If You Need A Variant

Use this starter as the base, then adapt it with:

- `/platform/claude-skill-starter.md`
- `/platform/codex-shared-instructions-starter.md`
- `/platform/generic-harness-module-starter.md`
- `/platform/plugin-loader-starter.md` only if your platform truly supports stable mounted docs
