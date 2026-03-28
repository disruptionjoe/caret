# Context Refresh

## Notation

```
^^^work.agent
  ...
  ^^^^
  ^^^work.agent
```

## What it does

An anchored agent works until context window degrades. State saves. The quad-caret (`^^^^`) clears everything. A new anchored agent resumes from saved state. The ellipsis (`...`) is the work phase. The quad-caret is the hard reset.

## When to use it

Long-running sessions where context fills with intermediate reasoning, dead-end exploration, stale information. Output quality degrades silently. You notice only when the result is wrong.

Context Refresh is closing all tabs and reopening only what you need.

## When not to use it

Short tasks fitting comfortably in one context window. Saving state, clearing, reloading has overhead.

Risky when state cannot serialize cleanly. If work depends on nuanced reasoning chains that don't reduce to structured data, the refresh loses signal the new instance cannot recover.

## Design notes

The quad-caret (`^^^^`) is the most aggressive operation in the notation. It clears everything. Following it with triple-caret (`^^^`, anchored) rather than double-caret (`^^`, ephemeral) is deliberate. The new agent inherits principles and memory the cleared agent accumulated.

The pattern reveals tension in all agent systems: context is both resource and liability. Early in a session, more context improves output. Late in a session, accumulated context degrades it. The notation does not solve this tension. It gives you a clean way to manage it.

Relates to **Scope Constraint** — refresh clears context debt; scope constraint prevents it from accumulating in the first place by rotating agents through different permission levels.

Relates to **Harness Layering** — when refreshing across platform changes, preserve the personal and project harnesses; reset only the platform state to prevent leakage.

When to trigger refresh is a judgment call. The notation expresses structure, not heuristic.
