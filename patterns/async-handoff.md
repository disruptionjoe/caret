# Async Handoff

## Notation

```
^^^worker ^autonomy9 ^grip3
  ^log
  ^log

^^^reporter ^scope3 ^length3
  ^report
  ^archive
```

Machine runs. Machine logs. At the boundary: one summary. Human reads. Human decides. Machine resumes.

## What it does

An agent executes work asynchronously over hours. It logs everything. At a fixed moment (dawn, shift end, defined boundary), it halts, compiles a single structured summary, and waits. The human reads the summary once. Makes decisions. Returns instructions. The agent resumes with new directives.

The pattern decouples machine rhythm from human attention span. The machine works continuously. The human engages in discrete windows.

## When to use it

Work that batches cleanly. Overnight skill improvements. A week of routine maintenance tasks. Coaching logs compiled nightly. Anything that does not need real-time feedback.

Use this when the human is the bottleneck, not the machine. The machine can execute 12 hours of work. The human has 20 minutes to review. Batch the execution. Summarize at the handoff. Respect the human's time scarcity.

Also: work with predictable cadence. Every midnight. Every Friday 8 AM. Every shift end. Rhythm matters. The human knows when to pay attention. The machine knows when to compile.

## When not to use it

Work that needs in-flight correction. If the machine might stray and requires real-time course correction, async is wrong. Handoff is too late.

Also wrong for interactive systems. Do not use async handoff when the human is waiting for an answer. Do not use it for high-consequence work that demands constant supervision.

## Design notes

The core trade-off is autonomy versus awareness. Running the machine overnight buys execution time. The human is blind until morning. If the factory catches fire at 3 AM, the human does not know until dawn.

Mitigate with health checks. Not "did the code crash" — error handling covers that. Instead: "am I making progress toward the goal?" If the overnight log is 20 appends and all are failures, the health check flags it. The human sees it in the summary. Awareness restored.

The summary is not a data dump. It is a narrative. What did the agent try. What succeeded. What failed. What needs human attention. The summary is 10 minutes of reading, max. If it takes longer, it will be skipped. Skipped summaries mean drift.

Use a fixed template. Shape: `[Period] [Goals] [Completed] [Blockers] [Improved] [Decisions Needed] [Next Steps]`. Consistency matters. The human pattern-matches. Fast recognition. Low cognitive load.

The handoff moment is a hard boundary. Not "sometime in the morning." Precisely 6 AM. 8 AM. Whatever. The human blocks the calendar. The machine knows when to compile. Everything aligns to that moment.

The summary becomes input to the next cycle. The human's decisions become the agent's new directives. The agent reads them first thing. Appends them to the decision log. Runs the next batch with better information. Every cycle, small improvement.

The pattern creates cadence. Execute overnight. Review at dawn. Decide. Execute. Review. Every day, a learning loop. Not dramatic. But it compounds across weeks.

Risk: the human stops reading summaries. The agent drifts. Old rules persist. Prevent this by making the handoff sacred. Block the calendar. Read every summary. Ten minutes. The cost is nothing. The benefit is drift prevention.

Relationship to **Gated Pipeline**: the pipeline is synchronous, linear. Each gate fires immediately after a stage completes. The handoff is asynchronous, temporal. It batches work and hands off at a defined moment. Use the pipeline for immediate quality control on sequential work. Use the handoff for decoupling machine rhythm from human engagement.

Relationship to **Overnight Factory**: both involve unsupervised execution. The factory is cyclical — it executes, evaluates, re-executes, compiles a summary. The handoff is linear — it executes, then halts and waits for human decision. Use the factory when evaluation should feed back into the queue. Use the handoff when the queue is fixed and only the human can decide what comes next.
