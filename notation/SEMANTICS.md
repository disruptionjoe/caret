# Caret^ Semantics

## Core Model

Caret^ does not describe implementation steps. It marks intent boundaries.

To keep those boundaries clear, this repo uses these terms:

- `directive`: a Caret^ signal such as `^depth8` or `^review`
- `worker`: the acting agent, process, or responsibility holder
- `hat`: a lens, persona, stance, or loaded skill applied to the current worker
- `target`: the named or exact handle attached to `^^` or `^^^`
- `scope`: the block of text controlled by a directive
- `harness`: the runtime, prompt system, or execution layer that interprets Caret^

## What Each Form Means

### `^`

`^` adjusts instruction intent without introducing a new worker boundary.

Examples:

- `^depth8`
- `^review`
- `^skeptical7`

### `^^`

`^^` changes the hat, not the worker.

It keeps the current worker active and changes how that worker should approach the scoped material. That change may come from:

- a named persona
- an exact persona file
- a skill file
- another harness-resolved target

`^^` does not imply a fresh context. It is a perspective shift inside the current worker boundary.

### `^^^`

`^^^` changes the worker.

It requests a separate worker boundary with distinct responsibility. A harness may pass full context, selected context, or minimal context, but the result is still treated as a different worker scope rather than a new hat on the same worker.

### `^^^^`

`^^^^` marks a fresh-eyes boundary.

It tells the harness to clear, discard, or strongly deprioritize prior context for the scoped section and treat what follows as new. It does not, by itself, choose a hat or a worker. Those choices come from the surrounding scope or from additional directives inside the boundary.

## Scope Behavior

Caret^ is downward-scoped.

- broader directives establish ambient behavior
- narrower directives refine or override that behavior
- outdent closes `^^` and `^^^`
- `^^^^` may be closed explicitly with a second `^^^^`

If a directive has no child block, it applies to the next line.

Blank lines do not end a scope on their own. They only separate text inside the same containing block.

## Targets

Targets are references, not guaranteed resources.

The notation states what should be used. The harness decides whether a target can actually be resolved. A target may point to:

- a role label
- a persona file
- a skill file
- another identifier the harness knows how to load

Exact targets reduce ambiguity. Named targets trade exactness for convenience.

## Count Form

Count form means selection by quantity, not naming:

```text
^^3
^^^3
```

`^^3` asks for multiple relevant hats in the current worker.

`^^^3` asks for multiple relevant workers.

The harness decides how those are selected when it supports selection. If it does not, the count form remains an unresolved request rather than a reason to invent arbitrary targets.

## Markdown Relationship

Caret^ lives inside Markdown, but it is not defined by Markdown section markers.

Headings, lists, and blockquotes help structure a document for humans. They do not add hidden Caret^ operators. Caret^ scope is still driven by directive placement, indentation, and fresh-eyes boundaries.

## Non-Goals

Caret^ is not trying to be:

- a general programming language
- an execution scripting language
- a replacement for harness policy
- a full ontology of agent roles

It is a compact intent layer. The rest of the repo exists to keep that compact layer usable.
