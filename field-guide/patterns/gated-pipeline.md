# Gated Pipeline

## Notation

```
^^^pipeline
  ^^stage.1
  ^gate.review
  ^^stage.2
  ^gate.review
  ^^stage.3
```

## What it does

Sequential stages with explicit review gates between them. Each stage is ephemeral — fresh context, no carryover bias. The gates are directive-level checkpoints where the pipeline agent evaluates whether the output meets criteria before passing it forward.

## When to use it

Production workflows where quality at each stage matters more than speed. Document generation: research → outline → draft → edit → review. Code: design → implement → test → review. Any pipeline where a bad stage-2 input produces an unfixable stage-3 output.

The gates catch problems early. Rework at stage 2 is cheap. Rework at stage 5 is not.

## When not to use it

Exploratory or creative work. Gates impose linear progression. If the task benefits from iteration, backtracking, or non-sequential discovery, the pipeline model constrains more than it protects.

Also overkill for two-step tasks. A gate between "draft" and "review" is just a review. The pipeline pattern earns its overhead at three or more stages.

## Design notes

The single-caret gate (`^gate.review`) is a directive, not an agent. It does not spawn anything. It is an instruction to the pipeline coordinator to pause and evaluate. This is a deliberate notation choice: gates are control flow, not computation.

The ephemeral stages (`^^`) ensure that stage 2 cannot see stage 1's reasoning — only its output. This prevents contamination. The pipeline coordinator (`^^^`) holds the full picture and decides what to pass through each gate.

The pattern encodes a principle: in sequential work, the interfaces between stages matter more than the stages themselves. The notation makes those interfaces first-class objects.
