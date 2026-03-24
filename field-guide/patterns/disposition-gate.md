# Disposition Gate

## Notation

```
^ [disposition gate]
  for each item in [pending]
    shelve or plan
      → shelve: reference | backlog | pending
      → plan: human | agent
    move item to destination
```

## What it does

A binary checkpoint that asks one question: does this item warrant action now, or should it be stored for later. Shelve it (reference, backlog, pending) or plan it (assign to human or agent). The human makes the decision. The system presents the item, waits for a choice, then moves it accordingly. Nothing passes through without explicit disposition.

## When to use it

When you have more work than you can do. When the human needs to review and approve before the system acts. When you want to prevent the system from committing to work it can't complete. When you want a single human-authoritative checkpoint that gates all downstream activity.

## When not to use it

When everything that arrives is urgent and must be acted on immediately. When you need sub-second decisions. When you're trying to build a system that minimizes human touches. When the volume is so high that human review becomes the bottleneck.

## Design notes

The gate is a policy boundary. It's where humans say yes or no. Everything before the gate is agnostic. Everything after the gate has been approved. The gate itself is the only place where policy lives.

The binary question is deliberate. Shelve or plan. Not: important, medium, low. Not: urgent, today, this week. Those categories are noise. The real question is binary: do we do this now, or do we store it. If you're storing it, where does it live. If you're doing it, who does it. That's the full scope.

Shelve has three destinations. Reference is for general knowledge that has no time dimension. Backlog is for things you want to do but haven't committed to. Pending is for things that depend on something else finishing first. Each destination has different semantics. Reference doesn't expire. Pending expires when the dependency resolves. Backlog is the to-do list without commitment.

Plan has two destinations. Human is for work that only a human can do. Agent is for work that an agent can do without supervision. The distinction is not about skill. It's about authority. A human can choose to do something an agent could do. An agent should never choose to do something only a human can decide.

The review is a read operation. The system doesn't modify the item during review. It only reads it, waits for a decision, then moves it. This means you can re-run the gate on the same item multiple times without side effects. If the human decides differently the second time, that's allowed.

Batching matters. If items arrive one at a time and the gate opens one at a time, you have latency. If items accumulate and the gate opens a batch, you have higher throughput. Know your volume and design accordingly. A daily gate review is different from a gate that runs on every arrival.

The human's decision is final. The system doesn't second-guess it. If the human shelves an item the system thought was urgent, the system accepts that. This prevents the system from assuming it knows better than the human. That's dangerous.

Authority is explicit. Who can make gate decisions. Usually one person. If multiple people can make decisions, how do they resolve conflicts. What happens if no one makes a decision (timeout). These are policy questions. Encode them near the gate, not downstream.

The gate is stateful. Each item has a disposition. If an item is shelved, it stays shelved until explicitly reviewed again. If it's planned, it stays planned until completed. The system tracks state. Don't lose it.

Logging is essential. Log every gate decision. Who decided, when, what the decision was, what the item was. This is your audit trail. Later, if someone asks why something didn't happen, you can check the gate log.

The gate is the structural complement to the overnight factory's approval loop. The overnight factory is a macro gate: it decides which goals are approved. This gate is the micro gate: it decides which tasks are approved. Both are about preventing the system from committing to work it can't do.

Testing is straightforward. Create test items. Feed them through the gate. Verify that each decision (shelve-to-reference, shelve-to-backlog, shelve-to-pending, plan-to-human, plan-to-agent) moves the item to the right place. Verify that the audit log records the decision. Verify that items can be re-reviewed. Verify that re-review can change the disposition.

One trap to avoid: don't let the gate become a black hole. If something is shelved in backlog, it needs a regular review cycle or it will sit there forever. Backlog needs to be reviewed periodically. Set a schedule. Weekly backlog review. Monthly pending review. Without these, your system fills with dead items.

Another trap: don't overload the gate with ranking. You'll be tempted to ask the human to rank items by priority. Don't. Ranking is expensive and changes over time. The gate asks one question: now or later. If the item is "now", the human can sequence it separately. If you need sequencing, build a separate orchestration layer downstream of the gate, not at the gate.

The gate is where signal is highest. Every decision that passes through has been explicitly approved. This makes the downstream work high-confidence. The cost is latency and human effort. The benefit is that you never start work that shouldn't start.
