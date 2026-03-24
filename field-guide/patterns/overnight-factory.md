# Overnight Factory

## Notation

```
^^^factory
  ^directive "queue.md"
  ^cycle
    ^^exec
    ^^eval ^scope.queue
    ^^exec
    ^^eval ^scope.review-only
      ^compile "summary"
```

## What it does

Separates execution from evaluation across a repeating cycle. Execution agents work a queue of approved tasks. Evaluation agents review what was produced, check it against domain standards, and — within strict constraints — feed new tasks back into the queue. The cycle repeats. A human reads the summary.

The executor is ephemeral. It picks up the queue, does the work, logs the output. No memory between runs.

The evaluator is anchored. It knows the domains, the voice standards, the standing rules. It reads what the executor produced and judges it. On designated passes, it can auto-queue the obvious next step. On final passes, it only reviews and compiles a summary for the human.

## When to use it

You have a directive with a queue of approved work. You want agents to grind through that queue unsupervised for an extended period — overnight, over a weekend, during off-hours. But you do not trust execution alone. You have seen what unchecked agents produce: voice drift, shallow work, scope creep, compounding errors across runs.

The factory pattern is the answer to a specific fear: what happens when no one is watching?

What happens is: someone is watching. The evaluator.

Specific triggers:

- A backlog of approved tasks that exceeds a single session
- Extended periods where the human is unavailable (sleep, travel, deep work)
- Domains with strict voice or quality standards that execution agents routinely violate
- Sequential work where each step depends on the previous step being correct

## When not to use it

The work requires real-time human judgment. If the next step cannot be determined without the human's input, the factory will either stall or invent work — both bad.

Also wrong for exploratory or creative work. The factory assumes a queue of known tasks with clear next steps. Discovery does not queue well.

If you have fewer than three tasks, this is overhead. Just run them and review the output yourself.

## Design notes

The notation encodes three structural decisions.

**First: the executor forgets.** Double-caret (`^^exec`) means each execution run starts clean. It reads the directive, works the queue, logs what it did. It does not remember the last run. This is deliberate. An executor that accumulates state across runs develops blind spots. It stops reading the directive carefully because it "already knows." Fresh eyes on the queue, every run.

**Second: the evaluator remembers.** Also double-caret in notation (`^^eval`), but anchored through the directive and decision log. It knows the voice guide. It knows the standing rules. It knows what the human corrected last time. This asymmetry — forgetful executor, knowledgeable evaluator — is what prevents drift without requiring the human to be present.

**Third: scope constraints are first-class.** The `^scope.queue` and `^scope.review-only` directives are not suggestions. They are hard boundaries on what the evaluator can do. `^scope.queue` means: you may add tasks, but only the obvious next step within already-approved goals. `^scope.review-only` means: you may evaluate, but you may not touch the queue. This prevents the most dangerous failure mode — the evaluator becoming a second executor that generates unbounded work.

The `^compile "summary"` on the final pass is what makes the pattern human-compatible. Without it, the factory is a black box. The summary is the contract between the overnight system and the human who wakes up to its output.

**The core trade-off is autonomy versus drift.** You want the system to run for hours without you. You also want it to not go sideways. The factory pattern gives you both by splitting the "running" into two roles with different authorities. The executor has permission to act but not to decide what to act on next. The evaluator has permission to decide what comes next but not to do the work. Neither role alone can run away.

**On cycle structure.** The pattern shows two exec/eval pairs per cycle. This is not arbitrary. A single pair means the evaluator's auto-queued tasks sit until the next cycle — potentially 24 hours. Two pairs mean the factory's own feedback loop closes within the same night. The second execution run picks up what the first evaluation queued. The second evaluation reviews it but does not queue more. This is a closed loop with a hard stop. No infinite recursion. No runaway queue growth.

**Relationship to Gated Pipeline.** A gated pipeline is linear: stage → gate → stage → gate. The factory is cyclical: exec → eval → exec → eval → summary. Gates are quality checkpoints between sequential stages of a single artifact. Factory evaluations are quality checkpoints between independent runs across a backlog. Use gates when one artifact moves through stages. Use the factory when many tasks move through runs.
