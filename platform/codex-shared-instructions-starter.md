# Codex Shared Instructions Starter

Use this when you have a shared instruction layer for Codex or another agent system with a common bootstrap prompt.

Use `/platform/caret-core-starter.md` first.

This file is the Codex-shaped wrapper around that core install.

## How To Use It

1. Add this to the shared instructions that load before task-specific work.
2. Keep the cheatsheet reachable in the workspace.
3. Do not bury this under later task modules.

## Starter

```markdown
# Caret^ Core Instructions

Use Caret^ as the active semantic signal layer for Markdown instructions in this workspace.

Source precedence:
1. `caret-cheatsheet.md`
2. `notation/`
3. other live repo docs governed by that canon
4. examples, patterns, and research only when they agree with canon

Interpretation rules:
- `^` signals a directive or control dimension
- `^^` applies a hat to the current worker
- `^^^` requests a separate worker boundary
- `^^^^` marks a fresh-eyes boundary
- indentation scopes downward
- fenced code blocks and quoted examples are literal

Operational rules:
- prefer exact targets over loose names when precision matters
- do not let archived, draft, or external material override local canon
- use support docs to clarify the cheatsheet, not replace it

Load order:
- load Caret^ before task-specific instructions or skills
- if direct file loading is unavailable, inline the full cheatsheet
```

## Smoke Test

```text
^^skills/editor.md
  Tighten this draft without changing the meaning.
```

```text
^^^^
Treat the next block as fresh context.
^^^^
```
