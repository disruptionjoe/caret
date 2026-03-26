# Caret^ Cheatsheet

Copy this into any agent session. Start using the notation immediately.

---

## Core idea

Caret^ is a semantic signal layer for agent workflows in Markdown. Small core. Clear intent. No wasted motion.

The notation signals intent. The local harness, skill system, or runtime decides execution. That is the point. Caret^ does not tell the system how to work. It tells the system what you want.

Structure is fixed. Vocabulary is expandable.

---

## The four caret forms

```
^      directive
^^     change the hat, not the worker
^^^    change the worker
^^^^   fresh-eyes boundary
```

`^` is an instruction.
`^^` applies a persona or lens to the current agent. Same worker, same context, different perspective.
`^^^` spawns a separate agent. Different worker, different responsibility boundary.
`^^^^` signals a fresh start. Clear or strongly deprioritize prior context and treat what follows as new. A second `^^^^` closes the fresh-eyes section and returns to the enclosing scope.

More carets, deeper separation.

---

## Scalar directives (0-9)

Most scalar directives use a 0-9 scale.

```
0      suppress or minimize
1-4    below normal
5      normal / default
6-9    above normal
```

If omitted, assume normal behavior.

Compact form preferred:

```
^temp3
^depth8
^grip5
```

Spaced form also valid:

```
^temp 3
^depth 8
```

Both resolve to the same meaning.

---

## Core scalars

Eight knobs ship with the cheatsheet. This is a starter set. Add your own once the pattern clicks.

```
^temp         (^t)  creativity / divergence
^length       (^l)  output length
^depth        (^d)  reasoning effort
^grip         (^g)  prescriptiveness
^precision    (^p)  strictness / exactness
^scope        (^s)  breadth of surface considered
^autonomy     (^a)  how much to decide without asking
^verification (^v)  how much to check before concluding
```

One-letter aliases are reserved for scalars. Operational directives spell out.

Scalars compose. They are orthogonal. Each one controls a separate dimension:

```
^d7 ^t2 ^g9   thorough, conventional, exact
^d3 ^t8 ^g2   quick, creative, uncommitted
```

---

## Aliases

Aliases are case-insensitive. `^t9`, `^T9`, `^temp9`, and `^temperature9` all resolve to the same meaning.

A scalar may have a one-letter, short, and long form. Use whichever is clearest for your context. One-letter saves tokens. Full words help readability in shared files.

---

## Operational directives

These tell the system what kind of work you want done. Not how to do it.

```
^intake
^triage
^queue
^log
^extract
^summarize
^synthesize
^plan
^review
^audit
^report
^rank
^route
^archive
```

The notation defines intent. The harness defines execution.

Operational directives take scalar levels too:

```
^review3     lighter pass
^review8     deeper pass
^audit2      quick scan
^audit9      exhaustive
```

---

## Open vocabulary

The cheatsheet defines a starter set. Any word can become a directive.

```
^humor7
^skeptical8
^formal2
^urgency9
```

This is not a bug. It is the core design. Caret^ is a semantic signal layer, not a language. If the word is clear in context, the system interprets it. Different systems may interpret it differently. That is expected. The 0-9 rule applies to anything scalar. Add what your workflow needs.

---

## Multi-target syntax

Commas separate multiple targets.

```
^^software-engineer,ux-designer
^^^critic,researcher,planner
```

Targets can be persona names, persona files, skill files, or whatever handles the harness understands.

---

## Exact targets

Names are fine when the harness can resolve them cleanly. Use exact files when you want no ambiguity about what should be loaded.

```text
^^personas/critic.md
^^review:personas/critic.md,personas/researcher.md
^^^skills/research.md
```

Prefer repo-relative paths in shared files. Keep path naming simple and consistent.

---

## Count form

After `^^` or `^^^`, a bare number means count.

```
^^3     apply 3 relevant personas here
^^^3    spawn 3 relevant sub-agents
```

How the system selects those personas or agents is up to the harness. Systems with routing logic or chief-of-staff behavior will handle this well. If your system does not have selection logic, name targets directly.

---

## Binding

Colon binds a directive to a target list.

```
^^review:critic,ux-designer
^^^plan:software-engineer,product-manager
```

Colon binds. Comma separates.

---

## Scope

A directive applies to the indented block beneath it. If nothing is indented, it applies to the next line.

`^^` and `^^^` create a new scope. That scope closes when indentation returns to the parent level.

`^^^^` may be used as an explicit fresh-eyes boundary. A second `^^^^` closes it. If it is not closed explicitly, it continues to the end of the containing block.

Directives do not leak upward or sideways. They flow down into their block.

Use spaces in examples and shared files. Two spaces per level is the preferred style. Any consistent deeper indent counts as child scope. Avoid tabs.

Caret lives inside normal Markdown structure. Headings, lists, and blockquotes are useful containers for sections, but they are not special Caret syntax. The actual close rule for `^^` and `^^^` is outdent.

```
^^^coordinator
  ^depth8
  ^^researcher
  ^^writer ^temp6
```

`^depth8` applies to everything inside the coordinator block. `^temp6` applies only to writer.

---

## Common patterns

**Apply a specialist lens:**
```
^^reviewer ^depth7
```

**Multiple perspectives:**
```
^^3 ^depth7 ^temp5
```

**Spawn a team:**
```
^^^critic,researcher,planner
```

**Use an exact persona file:**
```
^^personas/critic.md ^depth7
```

**Run a skill in the current worker:**
```
^^skills/editor.md
```

**Spawn a worker from a skill file:**
```
^^^skills/research.md ^depth8
```

**Context refresh:**
```
^^^writer ^depth8
  ...work...
  ^^^^
  ^^^writer
```

**Sequenced workflow:**
```
^^^coordinator ^depth8
  ^review
  ^synthesize
  ^rank
  ^report
```

**Coordinated team:**
```
^^^coordinator ^depth8
  ^^researcher ^depth7
  ^^writer ^temp6 ^grip7
  ^^reviewer ^depth7
```

---

## Composition

Directives go left-to-right on a line. Indentation means scope.

```
^^^coordinator
  ^depth8
  ^^^3
    ^depth7 ^temp5
```

The coordinator spawns three sub-agents, each scoped to depth 7, temp 5.

---

## Rules

- `,` separates targets: `^^critic,researcher`
- `:` binds directives to targets: `^^review:critic`
- Knobs are numbers: `^depth7` not `^depth high`
- Aliases are case-insensitive: `^t9` and `^T9` are the same
- Inside fenced code blocks, Caret is example text, not live instruction
- If omitted, assume default behavior
