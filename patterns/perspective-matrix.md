# Perspective Matrix

## Notation

```
^^^coordinator
  ^^3
```

Or named:

```
^^^coordinator
  ^^engineer
  ^^designer
  ^^user
```

## What it does

Spawns multiple ephemeral agents on the same task, no shared context between them. Each produces independent analysis. The coordinator synthesizes across all views.

The count form (`^^3`) means three fresh perspectives, zero cross-talk. The named form specifies which lenses.

## When to use it

Decisions that need independent judgment. Code review where three reviewers work blind to each other's notes. Risk assessment where each analyst flags different threats. Quality evaluation where groupthink is the enemy.

One draft, genuine critique. Engineer spots performance gaps. Designer spots UX brittleness. User representative spots purpose drift. None saw the others' feedback. Synthesis is richer because perspectives stayed separate.

## When not to use it

Single correct answer. Three ephemeral agents on a factual lookup wastes tokens.

Also poor when the problem needs deep shared context. Three reviewers with no background produce shallow, overlapping notes. For complex artifacts, give reviewers *selected* context—but never each other's output.

## Design notes

This encodes the Three-Lens Review pattern from systems engineering in two lines. The notation does not specify which lenses—that is the coordinator's job.

The count form (`^^3`) avoids naming three identical agents. When the purpose is parallel evaluation, names don't matter. Count does.

Named perspectives work when the diversity comes from role, not from simple redundancy. That choice is readability, not function.

Relates to **Disposable Specialists**: both spawn ephemeral agents to eliminate bias, but Matrix treats each agent as *equally valid* (parallel evaluation) while Specialists treat them as *sequential handlers* with a coordinator on top that synthesizes and remembers.
