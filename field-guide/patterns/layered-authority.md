# Layered Authority

## Notation

```
^^^governor
  ^^^executor
    ^^worker
    ^^worker
```

## What it does

A hierarchy with two levels of anchored agents and disposable workers at the leaf level. The governor sets constraints and monitors outcomes. The executor makes tactical decisions within those constraints. The workers execute without judgment.

## When to use it

Complex tasks where a single coordinator cannot hold both strategic oversight and tactical execution without one compromising the other.

Common in: multi-domain project management, content production pipelines where editorial standards must be maintained across many pieces, and any system where "who approves" and "who builds" should not be the same agent.

## When not to use it

Single-domain tasks. Two levels of anchored coordination add latency and token cost. If the governor and executor would make identical decisions, collapse them into one.

Also poor for creative exploration. Authority hierarchies suppress divergent thinking. Use flat structures (Perspective Matrix) instead.

## Design notes

The notation makes the authority relationship explicit through nesting. The governor contains the executor. The executor contains the workers. Each level sees only what its parent passes down and what its children pass up.

The choice between `^^^` (anchored) and `^^` (ephemeral) at each level is the key design decision. Anchored governors remember past decisions and evolving standards. Anchored executors maintain project continuity. Ephemeral workers stay cheap and disposable.

This pattern maps directly to the approval gate concept: work flows upward for review, authority flows downward as constraints. The notation makes the gate structure visible in two characters.
