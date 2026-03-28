# Work Item Lifecycle

## Notation

```
^^^coordinator ^grip9
  ^queue
    ^status:agent-ready
    ^status:active
    ^status:done
    ^status:needs-human
    ^status:blocked
    ^status:skip
```

Six states. Each state owns who acts and what they can decide.

## What it does

Tracks project lifecycle through explicit state transitions. Ownership and authority are bound to state, not to person or project type. `agent-ready` means the factory can pull and work. `active` means work is underway. `needs-human` means blocked until a human acts. `done` means shipped. `blocked` means an external dependency is missing. `skip` means the item was dropped deliberately, not lost.

The state is the permission layer. Not roles. Not credentials. Not approval documents. State. An item in `agent-ready` state is permission for the factory to work. An item in `needs-human` state is a stop sign. The factory does not ask for permission. It reads state.

## When to use it

Queue-based systems where multiple agents need to know who owns the next decision without asking. Night factories. Project management at scale. Any pipeline where work sits in a queue and different actors (human, executor, evaluator) have different authority over transitions.

## When not to use it

Simple single-agent tasks. Trivial one-offs. Anything that finishes in one session. Six states require discipline. If the work fits in working memory without tracking, skip the pattern.

Also overkill for purely creative or exploratory work where the concept of "states" creates false linearity.

## Design notes

Transitions follow an approval loop. The human is the gate at the top. The factory is the agent gate in the middle. The evaluator is the goal-alignment gate. The human promotes items to `agent-ready`. The factory moves items from `agent-ready` to `active` to `done`. The evaluator can queue work within already-approved goals. No state moves backward except back to `needs-human` when active work hits a blocker.

`skip` is not failure. It is decision. An evaluator concludes an approved goal no longer serves the mission. `skip` records that. The item is not lost — it is archived with state. If the goal becomes relevant again later, the item is still there with full context.

`blocked` is rare. It means active work hit an external dependency. The item stays blocked with clear notes on what unblocks it. If the dependency will never clear, promotion to `skip` is explicit.

The state machine is not a waterfall. Active items can pause and return to `needs-human` when work uncovers blockers. The state encodes what happened, not a linear progression.

Design consequence: states must be kept current or the system lies. A stale `agent-ready` item will get picked up even if work has stopped. Integration with a regular update cadence is essential.

Relationship to **Overnight Factory**: the factory consumes this lifecycle. It reads states to decide what to work on.

Relationship to **Disposition Gate**: the gate is the entry point where incoming work gets its first state assignment.

Relationship to **Layered Authority**: authority governs which actor can trigger which state transitions.
