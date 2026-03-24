# Disposable Specialists

## Notation

```
^^^chief.of.staff
  ^^researcher
  ^^writer
  ^^reviewer
```

## What it does

One anchored agent holds continuity and delegates to ephemeral specialists. Each specialist starts clean, does one job, returns results. The anchored agent synthesizes. The specialists hold nothing.

## When to use it

You need multiple distinct capabilities applied to the same problem, but you do not want the researcher's framing to contaminate the writer's output, or the writer's attachment to contaminate the reviewer's judgment.

Any task where the quality of each step depends on not knowing what the other steps produced.

## When not to use it

The task requires deep shared context across steps. If the writer needs the researcher's reasoning (not just findings), ephemeral specialists lose too much signal. Use anchored collaborators instead.

Also wasteful for simple sequential tasks where a single agent could handle all steps without bias risk.

## Design notes

The triple-caret (`^^^`) on the coordinator is the structural choice that matters. It carries memory, principles, and accumulated context. The double-caret (`^^`) specialists are deliberately disposable. They cannot access the coordinator's full state — only what the coordinator explicitly passes.

This is the most common pattern in production agent systems, whether people name it or not. The insight is that contamination between steps is the default. Clean separation requires architectural intent.

The notation makes the intent visible. Three carets: this agent remembers. Two carets: this agent forgets.
