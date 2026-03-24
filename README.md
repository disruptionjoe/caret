# Caret^

**Portable directive notation for agent orchestration.**

Every agent tool has its own config format. Its own rules files. Its own way of saying "spawn a sub-agent with no context." None of them talk to each other. The patterns are identical. The syntax never is.

This is not a tooling problem. It is a notation problem. There is no shared language for what you want agents to do.

Caret^ is that language. You write orchestration intent once, in Markdown, and adapters translate it to whatever runtime your agents use.

```
^    directive
^^   spawn ephemeral
^^^  spawn anchored
^^^^ clear context
```

That is the entire interaction model.

Not a framework. Not a runtime. Not another orchestration tool competing for your stack. A notation that sits inside your `.md` files and stays out of the way.

---

## Quick Start

### Depth

More carets, deeper level.

| Syntax | Meaning |
|--------|---------|
| `^` | Directive — a single instruction to the runtime |
| `^^` | Spawn ephemeral — a fresh agent with no prior context |
| `^^^` | Spawn anchored — an agent that inherits designated context |
| `^^^^` | Clear context — save state, wipe the window, start clean |

### Numbered Spawn

```
^^3   three ephemeral agents
^^^2  two anchored agents
```

The notation says *what*. The runtime decides *how*.

### Parameters

Dot notation attaches conditions to any directive.

```
^model.sonnet
^retries.2
^timeout.30s
```

Parameters are hints. If the runtime adapter recognizes a parameter, it applies it. If not, it ignores it. The notation does not enforce a parameter vocabulary — that is the adapter's job.

```
^model.sonnet ^retries.2
^^researcher
```

Set the model, set retries, spawn a researcher. One line.

### Verbose Form

Short form and long form mean the same thing.

| Short | Long |
|-------|------|
| `^^` | `^spawn.ephemeral` |
| `^^^` | `^spawn.anchored` |
| `^^^^` | `^context.clear` |
| — | `^govern.readonly` |

The separator is always `.` — no parentheses, no hyphens. Compound words collapse: `readonly`, not `read-only`.

### Principles

1. `^` for depth
2. `.` for separation
3. Markdown-native — lives in `.md` files
4. Declarative — intent, not wiring
5. Portable — adapters handle the runtime

---

## Field Guide

The [Caret^ Field Guide](field-guide/) is a practitioner's reference for agent terminology.

"Tool." "Skill." "Plugin." "Chain." "Workflow." Every platform uses these words differently. The Field Guide maps where they overlap, where they diverge, and where the distinctions actually matter.

Each entry: tool-neutral definition, competing terms across platforms, design distinctions, ecosystem notes, and common failure modes.

Browse it: [field-guide/](field-guide/)

---

## Patterns

### Disposable Specialists

```
^^^chief.of.staff
  ^^researcher
  ^^writer
  ^^reviewer
```

The Chief of Staff is anchored — it holds continuity across the task. The specialists are ephemeral. Each starts clean, does one job, returns results. The CoS synthesizes. The specialists hold nothing.

### Perspective Matrix

```
^^^chief.of.staff
  ^^3
```

Three ephemeral reviewers. Different lenses. No cross-contamination. The CoS synthesizes. Context stays clean.

### Context Refresh

```
^^^work.agent
  ...
  ^^^^
  ^^^work.agent
```

Work until the context window gets heavy. Save state. Clear. Reload. Resume clean. Long sessions degrade without this. Most people learn that the hard way.

---

## Who This Is For

People who build agent systems and are tired of rewriting the same orchestration logic in every tool's proprietary format.

People who care about clean context, precise directives, and not wasting tokens on ambiguity.

If you need a sales pitch, this is not for you.

---

## Current State

Caret^ is a notation spec. The symbol set, the Field Guide structure, and the initial patterns are defined. Adapter implementations that compile the notation into specific runtimes are next.

## Structure

```
README.md               you are here
MANIFESTO.md            why this exists
CONTRIBUTING.md         how to propose changes
field-guide/
  ├── glossary/         the vocabulary
  ├── patterns/         architecture patterns
  ├── examples/         real-world usage
  └── *.md              concept clusters + emerging terms
research/               evidence that the notation works
governance/             how contributions are reviewed
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). The bar is practical utility. If it does not help someone build a better agent system, it does not belong here.

## License

MIT.

## Author

[Disruption Joe](https://disruptionjoe.com)

---

*Context is not a bucket. It is a weapon. Use only what improves the shot.*
