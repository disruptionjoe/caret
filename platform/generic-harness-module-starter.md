# Generic Harness Module Starter

Use this when you control the harness repo and can define a dedicated module for Caret^.

Use `/platform/caret-core-starter.md` first.

This file is the harness-module wrapper around that core install.

## How To Use It

1. Create a module that loads before task routing.
2. Point it at `/caret-cheatsheet.md`.
3. Add `/notation/` as optional deep support.
4. Keep the rest of the repo outside the hot path unless needed.

## Starter Shape

Use this as a model, then adapt it to your harness:

```text
module: caret-core
stage: pre-task

primary_source:
  - caret-cheatsheet.md

support_sources:
  - notation/
  - glossary/

literal_surfaces:
  - fenced code blocks
  - quoted text
  - copied external snippets

conflict_rule:
  - live repo canon beats examples, patterns, research, drafts, archives, and external sources

core_meanings:
  - ^ = directive
  - ^^ = hat, same worker
  - ^^^ = worker boundary
  - ^^^^ = fresh-eyes boundary

loader_rule:
  - load caret-core before task-specific modules
  - if direct file loading is unavailable, inline caret-cheatsheet.md into the module
```

## Hot Path Rule

The module should load the smallest useful layer first:

1. `caret-cheatsheet.md`
2. `notation/` only when deeper semantics are needed

Do not make every task pay the cost of loading research and long support docs unless the task actually needs them.
