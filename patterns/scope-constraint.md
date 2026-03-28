# Scope Constraint

## Notation

```
^^^agent ^scope3 ^autonomy2
  ^review

^^^agent ^scope7 ^autonomy6
  ^queue
  ^log
```

Same agent. Different permissions on different runs. Scalars encode the constraint. The orchestrator assigns scope before launch.

## What it does

Declares what an agent can do on a specific run. Not global permissions. Not role-based. Run-specific. On Tuesday the agent can add items to the queue. On Thursday, it can only review them. On Friday, it runs with minimal context. Each run gets a scope envelope.

Context loading is part of scope. A review pass gets summary scope. A deep work pass gets full scope. The orchestrator decides before the agent starts.

## When to use it

When the same agent needs to operate at different trust levels depending on situation. When you want power on some passes, constraints on others.

When you want context load matching the task. Shallow review doesn't need full context. Deep analysis does.

When you want to prevent operations without changing the agent itself. Lock the queue this pass. Unlock it next.

## When not to use it

When permissions are permanent. Use roles for that. Scope constraint is tactical, temporary, per-run.

When the agent needs to decide its own scope. Scope comes from outside. If an agent can negotiate scope, the pattern breaks.

## Design notes

Scope constraint is a permission model for ephemeral agents. Ephemeral agents have no persistent state. They cannot accumulate power. So the only way to give them power is per-run, through scope.

An evaluator running every morning could have different scope daily. Monday: queue scope + full context. Can add items, sees everything. Tuesday: review-only scope + summary. Can only comment. Wednesday: queue scope + minimal. Can add but sees only metadata.

The orchestrator makes scope assignments. Not the agent. Not the user. The orchestrator knows the week's pattern. It knows when to lock agents down.

Three types work together:

**Action scope.** What operations allowed. queue scope = add, review-only scope = read-only, propose scope = suggest but don't execute, execute scope = full execution.

**Context scope.** How much state the agent sees. minimal scope = metadata, summary scope = summaries and key metrics, selected scope = specific folders, full scope = everything. Full context is slower, costlier. Use when you need depth.

**Time scope.** How much time does this agent get. five-minute scope = shallow pass, thirty-minute scope = medium pass, unlimited scope = go deep. Agents work differently under time pressure. Five minutes forces ruthlessness. Thirty minutes allows exploration.

Scope declared before agent starts. Agent reads action scope, context scope, time scope at beginning. If it tries operation outside scope, system rejects with clear message. Not soft suggestion. Hard rejection.

Context loading prepared in advance. Full scope means context pre-loaded. Minimal scope means metadata only. Not the agent deciding mid-run it needs more context. The orchestrator decided before launch.

Scope changes logged. Evaluator ran queue scope Monday, review-only scope Tuesday. This audit trail matters. If you see low-signal items appearing, trace back to when scope changed. Maybe queue scope was too loose. Maybe agent needs calibration.

Rotation patterns work well with scope constraint. Agent on review-only for a week learns to evaluate ruthlessly. Bring it back to queue scope and it adds better items. Constraint teaches the agent what matters.

Emergency scope exists. System in crisis. Flip one agent to execute scope + full context for twelve hours. Let it work without constraints. Lock it back when crisis ends. Scope constraint lets you flex permissions without changing agent or trusting agent to self-govern.

Trade-off: scope constraint requires orchestration discipline. Orchestrator must assign scope thoughtfully. If assignments are random or loose, pattern fails. You need clear model of when to lock, when to unlock, when to load full context, when to summarize.

Agents should understand their scope. Should see it as legitimate, not arbitrary. Document says "Tuesday you run review-only scope because reviews are Tuesday and we want you evaluating fresh" beats random constraint. Agents work better when constraint feels purposeful.

Pattern scales because scope is declarative. Write it down. Adjust weekly. No reprogramming needed. No roles or permissions change. Just change scope envelope next run.

Relates to **Context Refresh** — refresh clears context debt after long sessions; scope constraint prevents accumulation by rotating permission levels.

Relates to **Publication Gate** — publication decision is a scope constraint: work agents have no publish scope; only humans can cross the gate.
