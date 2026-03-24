# Work Item Lifecycle

## Notation

```
[agent-ready] -> [active] -> [done]
      ^                         |
      |                    [skip]
      +-- [blocked] <-- [needs-joe]
```

Six states. Each state owns who acts and what they can decide.

## What it does

Tracks project lifecycle through explicit state transitions. Ownership and authority are bound to state, not to person or project type. Agent-ready means factory can pull and work. Active means work is underway. Needs-joe means blocked until Joe acts. Done means shipped. Skip means discarded. Each transition is a decision point with a clear decision maker.

## When to use it

Night factory directive. Project management at scale. Any system where multiple agents need to know who owns the next decision without asking. The factory walks the directive and acts only on agent-ready and active items. Evaluator can promote within approved goals. Joe promotes items to agent-ready from needs-joe.

## When not to use it

Simple single-agent tasks. Trivial one-off scripts. Anything that will finish in one session. The overhead is real: six states require discipline. If the work is small enough to fit in working memory without state tracking, skip this pattern.

## Design notes

State is the permission layer. Not roles, not credentials, not approval documents. State. An item in agent-ready state is permission for the factory to work. An item in needs-joe state is a blocker on the factory. The factory does not ask for permission; it reads state.

Transitions follow the approval loop. Joe is the human gate at the top. The factory is the agent gate in the middle. The evaluator is the goal-alignment gate. Joe can move items from needs-joe to agent-ready. The factory can move from agent-ready to active to done. The evaluator can promote within goals already approved by Joe. No state can move backward except back to needs-joe when an active item hits a blocker.

The skip state is not failure. It is decision. An evaluator might conclude that an approved goal no longer serves the mission. Skip records that decision. The item is not lost; it is archived with state recorded. Next season, if the goal becomes relevant again, the item is still there with full context.

Blocked state is rare. It means active work hit an external dependency. The item stays in blocked state with clear notes on what unblocks it. When the dependency clears, the blocker is lifted and the item returns to active. If the dependency will never clear, promotion to skip is explicit.

The state machine is not a waterfall. Active items can pause and return to needs-joe if the work uncovers blockers. This is fine. The state encodes what happened, not a linear progression. The factory respects the state and does not burn time on needs-joe items.

Design consequence: this pattern requires discipline. States must be kept current or the system lies. A stale item in agent-ready state will get picked up even if work has stopped. Integration with the feed update cadence is essential. States change, the feed updates, the factory runs. Cadence matters.

Related: Overnight Factory consumes this lifecycle. Disposition Gate is the entry point. Layered Authority governs transitions.
