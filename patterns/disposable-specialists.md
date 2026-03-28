# Disposable Specialists

## Notation

```
^^^coordinator
  ^^researcher
  ^^writer
  ^^reviewer
```

## What it does

A coordinator holds continuity. Each specialist does one job cleanly, then disappears. No state leaks between steps. Researcher finds facts. Writer shapes them. Reviewer judges the shape. None of them see each other's work.

## When to use it

Multiple distinct skills applied to the same problem, and the quality of each step depends on *not knowing* what the other steps produced.

Code review where the reviewer must judge independently. Copy editing where the editor doesn't see the drafting notes. Research synthesis where each analyst works from raw data, not each other's conclusions.

Any task where cross-contamination is the enemy.

## When not to use it

Deep shared context is required. If the writer needs the researcher's *reasoning* (not just the findings), ephemeral specialists lose signal. Collapse them into anchored collaborators instead.

Also wasteful for simple sequential work a single agent could handle without bias risk.

## Design notes

The triple-caret (`^^^`) coordinator carries memory, principles, accumulated context. The double-caret (`^^`) specialists are deliberately empty. They see only what the coordinator explicitly passes.

This is the default pattern in production systems, whether named or not. Contamination between steps happens by accident. Clean separation requires architecture.

The notation makes it visible: three carets remember. Two carets forget.

Relates to **Perspective Matrix**: both use ephemeral agents to prevent bias, but Specialists separate *sequence* (one task after another, same goal) while Matrix separates *viewpoint* (same task, multiple eyes, no hierarchy).
