# Scope Constraint

## Notation

```
^ scope.queue
  ^^ agent (can add tasks)

^ scope.review-only
  ^^ agent (can only review)

^ scope.minimal | scope.summary | scope.selected | scope.full
  ^^ agent (context loading level)
```

Same agent. Different permissions on different runs. The chief of staff assigns scope before launch.

## What it does

Declares what an agent can do on a specific run. Not global permissions. Not role-based. Run-specific. On Tuesday, an agent can add items to the queue. On Thursday, the same agent can only review them and comment. On Friday, it runs with minimal context. Each run gets a scope envelope.

Context loading is part of scope. An agent on a review pass might get scope.summary. Same agent on a deep work pass might get scope.full. The chief of staff decides before the agent starts.

## When to use it

When you want the same agent to operate at different trust levels depending on the situation. When you want to give an agent power on some passes and constraints on others.

When you want to match context load to the task. A shallow review doesn't need full context. A deep analysis does.

When you want to prevent certain operations without changing the agent itself. Lock the queue on this pass. Unlock it on the next.

## When not to use it

When the permissions are permanent. Use roles for that. Scope constraint is tactical, temporary, per-run.

When the agent needs to decide its own scope. Scope comes from outside the agent. If an agent can negotiate scope, the pattern breaks.

## Design notes

Scope constraint is a permission model for ephemeral agents. Ephemeral agents have no persistent state. They can't accumulate power. So the only way to give them power is per-run, through scope.

An evaluator agent that runs every morning could have different scope every day. Monday: scope.queue + full context. It can add items and see everything. Tuesday: scope.review-only + summary. It can only comment. Wednesday: scope.queue + minimal. It can add but sees only metadata.

The chief of staff makes these assignments. Not the agent. Not the user. The chief of staff, which is the orchestration layer. The chief of staff knows the week's pattern. It knows when to let agents write and when to lock them down.

Why this matters: an agent with constant full permissions will accumulate context debt. It will feel empowered to add "just this one more task" every run. After fifty runs, the queue is bloated. With scope constraint, the chief of staff prevents that. Three adds per week. No more. The agent learns to prioritize ruthlessly.

The pattern also protects against agent drift. An agent that's been adding items for five weeks might start adding low-signal items. It's normalized itself into thinking everything is queue-worthy. With scope constraint, you rotate it to review-only for a week. It sees the queue from a different angle. It comes back with perspective.

Three types of scope constraints work together:

**Action scope.** What operations are allowed. scope.queue = can add, scope.review-only = read-only, scope.propose = can suggest but not execute, scope.execute = full execution.

**Context scope.** How much of the user's state the agent sees. scope.minimal = metadata only, scope.summary = summaries and key metrics, scope.selected = specific folders/domains, scope.full = everything. A full-context agent is slower and costlier. Use it when you need depth.

**Time scope.** How much time does this agent get. scope.five-minute = shallow pass, scope.thirty-minute = medium pass, scope.unlimited = go deep. Agents work differently under time pressure. Five minutes forces ruthlessness. Thirty minutes allows exploration.

Implementation detail: scope must be declared before the agent starts. The agent reads scope.action, scope.context, and scope.time at the beginning of a run. If it tries an operation outside its scope, the system rejects it with a clear message. Not a soft suggestion. A hard rejection.

Another detail: context loading must be prepared in advance. If an agent is going to run with scope.full, the context is pre-loaded before the agent starts. If it's scope.minimal, only metadata is loaded. This is not the agent deciding mid-run that it needs more context. The chief of staff decided before launch.

A third detail: scope changes must be logged. The evaluator ran with scope.queue on Monday and scope.review-only on Tuesday. This audit trail matters. If you see the evaluator started proposing low-signal items, you can trace it back to when scope changed. Maybe scope.queue was too loose. Maybe the agent needs different calibration. The log tells you.

Rotation patterns work well with scope constraint. An agent on review-only for a week learns to evaluate ruthlessly. Bring it back to scope.queue and it adds better items. The constraint teaches the agent something about what matters.

Another pattern: emergency scope. The system is in crisis. Flip one agent to scope.execute + full context for twelve hours. Let it work without constraints. Then lock it back to scope.review-only when the crisis ends. Scope constraint lets you flex permissions without changing the agent or trusting the agent to self-govern.

The trade-off: scope constraint requires orchestration discipline. The chief of staff must be designed to assign scope thoughtfully. If scope assignments are random or too loose, the pattern fails. You need a clear model of when to lock, when to unlock, when to load full context, when to summarize.

One more consideration: agents should understand their scope. They should see it as legitimate, not arbitrary. A document that says "On Tuesdays you run with scope.review-only because reviews are Tuesdays and we want you evaluating with fresh perspective" is better than a constraint that appears random. Agents work better when the constraint feels purposeful.

The pattern scales because scope is declarative. You write it down. You adjust it weekly. You don't need to reprogram the agent. You don't need to change roles or permissions. You just change the scope envelope on the next run.
