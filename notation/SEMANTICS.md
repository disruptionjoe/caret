# Notation Semantics

What constructs mean, especially where ambiguity could arise.

---

## Caret depth vs parameter depth

`^^` (two carets) means "spawn ephemeral." `^depth7` (the depth knob) means "thoroughness level 7." These are different uses of the word "depth."

- Caret depth = structural lifecycle (`^`, `^^`, `^^^`, `^^^^`)
- `^depth` knob = behavioral thoroughness (0–9 scale)

They do not conflict. Caret depth is about *what kind of agent*. The depth knob is about *how thorough that agent should be*.

---

## `^temp` vs `^grip`

Temperature controls creative range — how far from convention the output wanders. Grip controls authority posture — how strongly the output commits to a specific answer.

These are orthogonal:

| | Low grip (exploratory) | High grip (directive) |
|---|---|---|
| **Low temp** (conservative) | Standard options, no recommendation | Do exactly this standard thing |
| **High temp** (creative) | Unconventional options, no recommendation | Do exactly this unconventional thing |

---

## Scope and indentation

<!-- TODO: formalize indentation semantics -->
<!-- Does indentation create strict scope? Or is it visual grouping? -->

---

## Context selection

<!-- TODO: define what follows ^context.selected -->
<!-- Is it freeform? Named references? File paths? -->

---

## Human gates

<!-- TODO: define → syntax formally -->
<!-- Is → reserved for human gates? Or general flow control? -->

---

## Default values

<!-- TODO: what happens when knobs are unspecified? -->
<!-- Is ^depth5 the default? Or is "unspecified" a valid state? -->
