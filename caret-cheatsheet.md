# Caret^ Cheatsheet

Copy this into any agent session. Start using the notation immediately.

---

## The four symbols

```
^    directive — a single instruction
^^   spawn ephemeral — fresh agent, no prior context
^^^  spawn anchored — agent with inherited context
^^^^ clear context — save state, wipe, start clean
```

## Control knobs (0–9)

```
^depth5   how thorough (0 = shallow, 9 = exhaustive)
^temp3    how creative (0 = conventional, 9 = exploratory)
^grip7    how prescriptive (0 = pure exploration, 9 = exact spec)
```

## Parameters

```
^model.sonnet       set model
^govern.readonly    read-only, no mutations
^context.none       no prior context
^context.selected   named items only
```

## Common patterns

**Spawn a specialist:**
```
^^reviewer ^context.none ^depth7 ^govern.readonly
```

**Parallel agents:**
```
^^3 ^context.selected topic ^depth7 ^temp5
```

**Context refresh:**
```
^^^writer ^depth8
  ...work...
  ^^^^
  ^^^writer
```

**Route by intent:**
```
^^^router ^govern.readonly
  greeting  → ^^priority ^context.selected state
  intake    → ^^capture ^context.selected message
```

## Composition

Directives go left-to-right. Indentation means scope.

```
^^^coordinator ^depth8
  ^^researcher ^context.selected ^depth7
  ^^writer ^temp6 ^grip7
  ^^reviewer ^context.none ^depth7 ^govern.readonly
```

## Rules

- `.` separates parameters: `^govern.readonly`
- No hyphens: `readonly` not `read-only`
- No parentheses: `^spawn.ephemeral` not `^spawn(ephemeral)`
- Knobs are numbers: `^depth7` not `^depth.high`

---

*Full spec: [notation/SPEC.md](notation/SPEC.md)*
