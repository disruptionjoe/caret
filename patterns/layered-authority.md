# Layered Authority

## Notation

```
^^^governor
  ^^^executor
    ^^worker
    ^^worker
```

## What it does

Two levels of anchored agents. Governor sets constraints and monitors outcomes. Executor makes tactical calls within those constraints. Workers execute without judgment.

Information flows down as constraints. Work flows up for review.

## When to use it

Complex tasks where one coordinator cannot hold both strategic oversight and tactical execution without each compromising the other.

Multi-domain project management. Content pipelines where editorial standards must hold across many pieces. Any system where "who approves" and "who builds" must be different agents.

Governor holds the long view. Executor handles the day-to-day. Workers stay cheap and disposable.

## When not to use it

Single-domain tasks. Two levels of anchored coordination add latency and token cost. If governor and executor make identical decisions, merge them.

Also poor for creative exploration. Authority hierarchies suppress divergent thinking. Use flat structures (**Perspective Matrix**) instead.

## Design notes

Nesting makes the authority chain explicit. Governor contains executor. Executor contains workers. Each level sees only what its parent passes and what its children report.

The choice between `^^^` (anchored, remembers) and `^^` (ephemeral, forgets) at each level is the core design decision. Anchored governors evolve standards. Anchored executors maintain project continuity. Ephemeral workers stay disposable.

This maps directly to approval gates: work flows up for review, authority flows down as rules. The notation makes the gate structure visible in two characters.

Relates to **Disposable Specialists**: both use anchored coordination, but Specialists is flat (one coordinator, many short-lived workers) while Layered Authority is hierarchical (nested anchored agents with workers at the leaf). Use Specialists for sequential steps. Use Layered Authority for recursive scope.
