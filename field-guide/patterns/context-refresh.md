# Context Refresh

## Notation

```
^^^work.agent
  ...
  ^^^^
  ^^^work.agent
```

## What it does

An anchored agent works until its context window degrades. State is saved. Context is cleared (`^^^^`). A new anchored agent resumes from the saved state.

The ellipsis (`...`) represents the work phase. The quad-caret (`^^^^`) is the hard reset.

## When to use it

Long-running sessions. The context window fills with intermediate reasoning, dead-end explorations, and stale information. The agent's output quality degrades silently. Most people notice only when the result is wrong.

Context Refresh is the agent equivalent of closing all your browser tabs and reopening only the ones you need.

## When not to use it

Short tasks that fit comfortably in a single context window. The overhead of saving state, clearing, and reloading is not free.

Also risky when the state cannot be cleanly serialized. If the work depends on nuanced reasoning chains that do not reduce to structured data, the refresh loses signal the new instance cannot recover.

## Design notes

The quad-caret (`^^^^`) is the most aggressive operation in the notation. It clears everything. The choice to follow it with triple-caret (`^^^`, anchored) rather than double-caret (`^^`, ephemeral) is deliberate: the new agent needs to inherit the principles and memory that the cleared agent accumulated.

The pattern reveals a tension in all agent systems: context is both resource and liability. Early in a session, more context improves output. Late in a session, accumulated context degrades it. The notation does not solve this tension. It gives you a clean way to manage it.

When to trigger the refresh is a judgment call. The notation expresses the structure, not the heuristic.
