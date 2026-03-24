# Perspective Matrix

## Notation

```
^^^chief.of.staff
  ^^3
```

## What it does

Spawns multiple ephemeral agents with the same task but no shared context. Each produces an independent analysis. The anchored coordinator synthesizes across all three.

The numbered spawn (`^^3`) means: three fresh perspectives, zero cross-contamination.

## When to use it

Decisions that benefit from independent judgment. Code review. Risk assessment. Quality evaluation. Anything where groupthink is the enemy.

The classic case: you have a draft and need honest critique. One reviewer finds structural problems. Another catches tone issues. A third spots logical gaps. None of them saw the others' feedback. The synthesis is richer because the perspectives were genuinely independent.

## When not to use it

The task has one correct answer. Running three ephemeral agents on a factual lookup wastes tokens.

Also poor when the problem requires deep shared context to evaluate. Three reviewers with no background will produce shallow, overlapping feedback. If the artifact is complex, give reviewers selected context — but never each other's output.

## Design notes

This is the Three-Lens Review pattern from systems engineering, encoded in two lines. The notation does not specify what the three lenses are — that is the coordinator's job.

The numbered spawn syntax (`^^3`) avoids the verbosity of naming three identical agents. When the purpose is independent parallel evaluation, the names do not matter. The count does.

If you need named perspectives (engineer, designer, user), write them out:

```
^^^chief.of.staff
  ^^engineer
  ^^designer
  ^^user
```

The choice between numbered and named is a readability decision, not a functional one.
