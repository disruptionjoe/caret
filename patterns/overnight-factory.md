# Overnight Factory

## Notation

```
^^^factory ^autonomy3 ^grip9
  ^^^executor
    ^log
  ^^^evaluator ^verification8
    ^queue
    ^log
  ^^^executor
    ^log
  ^^^evaluator ^verification8 ^scope3
    ^review
    ^report
```

The executor has permission to work. Not to decide what to work on. The evaluator has permission to queue work. Not to do it. Neither alone can run away.

## What it does

Separates execution from evaluation across repeating cycles. Executors work a queue of approved tasks, fresh each run. Evaluators review output, check it against standards, queue obvious next steps within strict scope limits, and compile a summary.

The executor is ephemeral. It picks up the queue, works, logs, forgets. No state between runs. Fresh eyes on every cycle.

The evaluator is anchored. It knows the domain, the voice, the standing rules. It reads what was produced. Judges it. Decides whether the work meets standard. Within its queue scope, it may queue the obvious next step. On final passes, it only reviews and compiles.

The cycle runs twice per night. Twice means the evaluator's queued work gets picked up and executed before the night ends. The loop closes. No queued work sits until tomorrow.

## When to use it

You have a backlog of approved work. You want it ground through unsupervised for hours or overnight. But you do not trust execution alone. You have seen agents drift: voice changes, shallow work, scope creep, errors compound.

Specific triggers:

- Backlog of 5+ approved tasks that exceeds one session
- Extended offline periods (sleep, travel, deep work blocks)
- Domains with strict voice or quality standards that agents routinely violate
- Sequential work where each step depends on the prior step being correct

The factory pattern answers: what happens when no one watches? Answer: someone is watching. The evaluator.

## When not to use it

The work requires real-time human judgment. If the next step cannot be determined without human input, the factory will stall or invent work — both bad.

Also wrong for exploratory or creative work. The factory assumes a known queue with clear next steps. Discovery does not queue well.

Overkill for small queues. Fewer than three tasks: just run and review yourself.

## Design notes

The notation encodes three structural choices.

**First: the executor forgets.** `^^^exec ^autonomy3` means it starts clean every cycle. Reads the directive. Works the queue. Logs. Does not remember the last run. This is deliberate. An executor that accumulates state develops blindness. It stops reading directives carefully. Fresh eyes, every cycle.

**Second: the evaluator remembers.** It is anchored to the decision log and the directive. It knows what the human corrected last time. It knows the voice guide. It knows the standing rules. This asymmetry — forgetful executor, knowledgeable evaluator — prevents drift without human presence.

**Third: scope is first-class.** The `^queue` directive on the evaluator means: queue only the obvious next step within already-approved goals. The narrowed `^scope3` on the final evaluator pass means: review only, do not touch the queue. These are hard boundaries. They prevent the most dangerous failure: the evaluator becoming a second executor that generates unbounded work.

The notation distinguishes scope permission from execution permission. The evaluator can decide what to queue (permission: queue). The executor can decide how to execute (permission: execute, within assigned task). Neither can both decide and execute everything.

The double-cycle structure matters. First exec/eval: execute a batch, evaluate the batch output, queue the next obvious step. Second exec/eval: execute the queued work, evaluate it, compile summary, halt. This is a closed loop with a hard stop. No infinite recursion. No runaway queue growth. The night has a boundary.

**The core trade-off is autonomy versus drift.** You want the system to run unsupervised for hours. You want it to not stray. The factory gives both by splitting authority. The executor has permission to act but not to decide what to act on. The evaluator has permission to decide what comes next but not to do the work. Neither role alone can drift.

Relationship to **Gated Pipeline**: the pipeline is linear — artifact flows through stages, gates control the flow. The factory is cyclical — tasks flow through queues, evaluation controls both work and queue progression. Use the pipeline for single-artifact transformation. Use the factory for batch-queue processing.

Relationship to **Async Handoff**: both involve unsupervised execution. The handoff batches work, executes, halts, waits for human decision. The factory executes, evaluates, re-executes, evaluates again, then halts. The handoff expects human decision to drive the next cycle. The factory drives its own next cycle through evaluation, until the final halt. Use the handoff when only the human should decide next steps. Use the factory when evaluation can queue work within scope limits.
