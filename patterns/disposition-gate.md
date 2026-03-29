# Disposition Gate

## Notation

```
^^reviewer ^depth5
  ^triage
  ^route
  ^log
```

Human reads each item. Decides: now or later. If later, where. If now, who. Nothing passes without explicit disposition. The notation above encodes the workflow steps; the gating contract — that a human must make an explicit binary decision before anything proceeds — lives in the prose below.

## What it does

A checkpoint before any downstream action. Human reviews each item. Asks one question: now or later. If later, choose a shelf: reference (general knowledge, no expiration), backlog (want it, not committed), pending (blocked on dependency). If now, choose who: human or agent. Item moves to destination. Nothing passes without explicit disposition.

## When to use it

When you have more work than capacity. When humans must approve before system commits. When you want to prevent runaway agents that commit to work they can't finish. When you need a single authoritative checkpoint that gates all downstream activity.

## When not to use it

When everything is urgent and must act immediately. When you need sub-second decisions. When volume is so high that human review becomes the bottleneck. When you're trying to build a system that minimizes human touches.

## Design notes

The gate is where policy lives. Everything before the gate is agnostic. Everything after has been explicitly approved. The gate is the boundary.

The binary question is deliberate. Shelve or plan. Not: urgent, medium, low. Not: today, this week, next month. Those are noise. The real split is binary: do we commit now, or do we store it. If we store it, where does it live. If we commit, who owns it. That's the full scope.

Shelve has three destinations with different semantics. Reference doesn't expire. Backlog is committed-someday but not now. Pending is blocked-on-something and expires when the dependency clears. Each has different review frequency. Reference: annual. Backlog: weekly. Pending: on-unblock.

Plan has two destinations. Human is for work that requires human authority or judgment. Agent is for work that humans can delegate. The distinction is about authorization, not capability. A skilled agent might be able to do something a human chooses to do anyway. An agent should never choose to do something that only humans can authorize.

The review is a read operation. No side effects. No mutations during review. Item is unchanged. This means you can re-review the same item and change disposition without cascading failures. The human is sovereign.

Batching matters. Single-item gates have latency. Batch gates have throughput. Daily gate review. Weekly. Per-user-request. Know your volume and design accordingly.

The human's decision is final. The system doesn't second-guess. If the human shelves something the system thought urgent, the system accepts it. This prevents the system from assuming it knows better. That's the whole point.

Authority is explicit. Who can make gate decisions. One person. Multiple people. How do they resolve conflicts. Timeout default. Encode this as policy near the gate, not buried downstream.

The gate is stateful. Each item has a disposition. Shelved items stay shelved until reviewed again. Planned items stay planned until completed. Tracking state is mandatory.

Logging is essential. Every decision. Who. When. What. Why (short). Audit trail. Later, when someone asks why something didn't happen, you check the gate log.

Contrast with `decision-tree-router`: a router decides which branch immediately. The gate delays decision until humans can review. Router is fast. Gate is deliberate. Router is for automated filtering. Gate is for human authority.

One trap: don't let backlog become a black hole. Items arrive, get shelved, then sit forever. Backlog needs a review cycle. Weekly. Monthly. Without it, dead items accumulate and signal becomes noise.

Another trap: don't ask the gate to rank. You'll be tempted. Resist. Ranking is expensive and changes constantly. The gate asks one question: now or later. If now, sequence it downstream in a separate orchestration layer. Keep the gate binary.
