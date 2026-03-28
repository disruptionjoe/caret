# Gated Pipeline

## Notation

```
^^^pipeline
  ^^^stage-1
  ^gate ^verification ^depth8
  ^^^stage-2
  ^gate ^verification ^depth8
  ^^^stage-3
```

Each stage is fresh. Each gate is a hard stop.

## What it does

Sequential work with explicit verification gates between stages. A stage executes, produces output, halts. The gate examines the output against criteria. Pass: feed to the next stage. Fail: reject, revise, or reroute. No leakage between stages. No contamination from prior reasoning.

The pipeline is not a workflow description. It is a control structure. The notation makes gates first-class, not hidden in prose.

## When to use it

Production workflows where bad input at stage N cascades into unfixable output at stage N+1. Document pipelines: research → outline → draft → edit → review. Code: design → implement → test → review. Any sequence where early errors compound.

Gates catch problems cheap. Rework at stage 2 costs less than rework at stage 5.

Three or more stages. Fewer than that is just linear work, not a pipeline.

## When not to use it

Exploratory work. Discovery. Anything that benefits from backtracking or non-linear iteration. The pipeline enforces sequence. If the task needs to loop backward, gates become constraints, not safeguards.

Also wrong when each stage is independent. If stage 2 does not need stage 1's output to be correct, there is no pipeline. Just run them in parallel.

## Design notes

The gate (`^gate ^verification`) is a directive, not an agent. It is an instruction to pause, evaluate, decide. It does not compute. It judges.

The notation separates three concepts: the executor (`^^^stage`), the output, and the judgment. This separation prevents executors from rating their own work. The gate is independent. Impartial.

The `^verification ^depth8` parameters encode the rigor. `^depth8` means deep scrutiny. `^depth3` means surface-level checks. The notation makes rigor visible. Different stages can have different gate strictness. Late stages often need harder gates.

The pattern encodes a principle: in sequential work, interfaces matter more than stages. What gets passed from stage 2 to stage 3 determines what stage 3 can produce. The notation puts interfaces first. The gates are the interfaces.

Relationship to **Overnight Factory**: the factory is cyclical, parallel. It evaluates across many independent runs. The pipeline is linear, sequential. It evaluates within a single artifact's journey. Use the pipeline when one thing flows through multiple transformations. Use the factory when many things flow through repeated evaluations.

Relationship to **Async Handoff**: the handoff is temporal — it pauses, summarizes, hands off to a different agent or human at a defined moment. The gate is synchronous — it executes immediately after the stage completes. Use the gate for immediate quality control. Use the handoff for asynchronous work boundaries.
