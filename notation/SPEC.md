# Caret^ Notation Spec

The canonical syntax reference.

---

## Core Symbols

```
^    directive
^^   spawn ephemeral
^^^  spawn anchored
^^^^ clear context
```

Four symbols. That is the interaction model.

---

## Numbered Spawn

```
^^3   three ephemeral agents
^^^2  two anchored agents
```

Trailing number sets agent quantity. Orchestration is delegated to the runtime.

---

## Control Knobs

Ordinal parameters (0–9) that shape agent behavior without changing content.

| Knob | Controls | 0 | 9 |
|------|----------|---|---|
| `^depth` | Thoroughness | Shallow scan | Exhaustive analysis |
| `^temp` | Creative range | Conservative, conventional | Exploratory, unconventional |
| `^grip` | Prescriptiveness | Pure exploration, no recommendation | Exact spec, no hedging |

Knobs are orthogonal. They compose:

```
^depth7 ^temp2 ^grip9   thorough, conventional, tell me exactly what to do
^depth3 ^temp8 ^grip2   quick, creative, don't commit to anything
```

### `^grip` scale

```
^grip0  pure exploration — only questions and considerations
^grip1  landscape — maps the option space, no ranking
^grip2  gentle lean — "you might consider X," alternatives equal weight
^grip3  soft recommend — "X looks strongest, but here are others"
^grip5  balanced — clear recommendation with rationale, alternatives acknowledged
^grip7  directive — "do X," brief rationale, alternatives as context only
^grip8  imperative — "step 1, step 2, step 3" — execute this
^grip9  exact — precise spec, no interpretation, no hedging, no alternatives
```

---

## Parameters

Dot notation attaches conditions to any directive.

```
^model.sonnet
^retries.2
^timeout.30s
```

Parameters are hints. If the runtime adapter recognizes it, it applies it. If not, it ignores it. The notation does not enforce a parameter vocabulary — that is the adapter's job.

---

## Verbose Form

Short form and long form mean the same thing.

| Short | Long |
|-------|------|
| `^^` | `^spawn.ephemeral` |
| `^^^` | `^spawn.anchored` |
| `^^^^` | `^context.clear` |
| — | `^govern.readonly` |

Separator is always `.` — no parentheses, no hyphens. Compound words collapse: `readonly`, not `read-only`.

---

## Context Directives

```
^context.none       no prior context
^context.selected   named context items follow
^context.full       everything available
^context.clear      save state, wipe, start clean (same as ^^^^)
```

---

## Governance Directives

```
^govern.readonly           read only, no mutations
^govern.askbeforewrite     request approval before writes
^govern.askbeforenetwork   request approval before network calls
```

---

## Composition

Directives compose left-to-right on a line. Indentation implies scope.

```
^^^coordinator
  ^depth8
  ^^3
    ^context.selected topic constraints
    ^depth7 ^temp5
```

The coordinator is anchored, depth 8. It spawns three ephemeral agents, each scoped to selected context at depth 7, temp 5.

---

## Human Gates

```
→ human.approve
```

A workflow pause requiring human input before continuing.

---

## What the notation does NOT cover

Domain-specific instructions ("check for security issues," "maintain the author's voice") stay in prose. Caret handles the orchestration scaffold — who gets spawned, what context they see, what they're allowed to do, how deep they go. Domain expertise lives alongside the notation, not inside it.
