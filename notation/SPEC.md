# Caret^ Spec

## Purpose

Caret^ is a semantic signal layer for agent workflows in Markdown.

It signals intent. The harness decides execution.

The canonical syntax is small:

- caret count
- word directive names
- optional scalar levels
- comma-separated target lists
- colon binding
- indentation for scope

## Core Forms

```text
^      directive
^^     change the hat, not the worker
^^^    change the worker
^^^^   fresh-eyes boundary
```

The meanings are stable:

- `^` signals an instruction or control dimension.
- `^^` applies a lens, persona, or skill to the current worker.
- `^^^` requests a separate worker boundary.
- `^^^^` opens a fresh-eyes boundary. A second `^^^^` closes it. If not closed explicitly, it continues to the end of the containing block.

More carets mean deeper separation.

## Directive Names And Levels

Most scalar directives use a `0-9` scale:

```text
0      suppress or minimize
1-4    below normal
5      normal / default
6-9    above normal
```

If a level is omitted, normal behavior is assumed.

Compact and spaced forms are equivalent:

```text
^depth8
^depth 8
```

One-letter aliases are reserved for scalars.

Aliases are case-insensitive:

```text
^t9
^T9
^temp9
^temperature9
```

Operational directives may also take levels:

```text
^review3
^review8
```

Caret^ uses open vocabulary. Any clear word may be used as a directive. The notation defines the shape of the signal, not a closed dictionary of allowed terms.

## Targets

Targets follow `^^` or `^^^`.

Comma separates multiple targets:

```text
^^critic,researcher
^^^planner,reviewer
```

Targets may be:

- labels
- persona names
- repo-relative file paths
- skill files
- other handles the harness understands

Exact targets are valid:

```text
^^personas/critic.md
^^^skills/research.md
```

After `^^` or `^^^`, a bare number means count:

```text
^^3
^^^3
```

Count form asks the harness to choose relevant targets when it has a supported selection mechanism.

## Binding

Colon binds a directive to a target list:

```text
^^review:critic,ux-designer
^^^plan:software-engineer,product-manager
```

Colon binds. Comma separates.

## Scope

A directive applies to the indented block beneath it. If nothing is indented beneath it, it applies to the next line.

`^^` and `^^^` create a new scope. That scope closes on outdent.

`^^^^` is the only explicit paired boundary in the core notation.

Directives flow downward into their block. They do not leak upward or sideways.

Use spaces in shared files. Two spaces per indentation level is the preferred style. Any consistent deeper indent counts as child scope. Avoid tabs.

Blank lines do not close a scope by themselves.

Markdown headings, lists, and blockquotes are useful containers for organization, but they are not special Caret^ syntax. The close rule for `^^` and `^^^` is still outdent.

## Composition

Directives compose left to right on a line.

More local scope overrides broader scope. Within the same scope and the same control dimension, the rightmost directive wins.

Example:

```text
^^^coordinator
  ^depth8
  ^^^3
    ^depth7 ^temp5
```

Here the coordinator block carries `^depth8`, while each nested spawned worker carries `^depth7 ^temp5`.

## Literal Text

Inside fenced code blocks, Caret^ is example text, not live instruction.

Use fenced code blocks when you want to show notation literally.

## Defaults

If a directive, target, or level is omitted, the harness falls back to its normal behavior unless a more specific local rule exists in the current scope.
