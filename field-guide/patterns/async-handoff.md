# Async Handoff

## Notation

```
^^overnight: [batch work accumulates]
^summary: [structured handoff at dawn]
^^^morning: [human reviews, decides]
```

Agents work asynchronously over hours. The human interface is synchronous: one summary at one handoff point.

## What it does

Work accumulates in the background. An overnight factory processes batch jobs, appends logs, builds improvements, compiles notes. Nobody is watching. The system just runs.

At dawn, the system halts. Compiles a single structured summary. The human reads it in one sitting. Makes decisions. Returns instructions. The system resumes.

The pattern decouples the machine's rhythm from the human's attention span. The machine can work for hours. The human engages in defined windows.

## When to use it

When you have work that can be batched. Overnight coaching logs to review. A full day's worth of factory tasks to compile. Skill improvements to evaluate. Work that does not need real-time feedback.

Use this for systems where the human is the bottleneck, not the machine. The machine can execute 10 hours of work. The human has 30 minutes to review. Batch the machine work. Summarize at handoff. Use the human's time efficiently.

The pattern is most useful when the handoff point is predictable. Every dawn. Every Friday morning. Every shift end. Regular rhythm. The human knows when to pay attention.

## When not to use it

When feedback is required in-flight. When the machine might go down a wrong path and needs course correction in real time. When the work is high-consequence and requires constant oversight.

Do not use async handoff for interactive systems. Do not use it when the human is waiting for an answer. Do not use it when work cannot be safely batched.

## Design notes

The core trade-off is async productivity versus human awareness. Letting the machine run overnight buys time. But the human is blind until dawn. If the overnight factory catches fire, the human does not know until morning.

Mitigate this with health checks. The overnight system should know if it is broken. Not in the sense of "did the code crash"—error handling catches that. In the sense of "am I making progress toward the goal." If the overnight factory has appended 20 logs but every one is an error, the health check should flag it.

Structure the handoff summary carefully. Not a data dump. A narrative. What did the system try to do. What succeeded. What failed. What needs human attention. The summary should tell a story the human can follow in 10 minutes.

Use a template for the summary. Consistency helps. Shape: `[Period] [Goals] [Completed] [Blockers] [Improvements] [Decisions Needed] [Next Steps]`. The human reads the same structure every time. Fast pattern recognition.

Keep summary length fixed. Long summaries are ignored. If the overnight work produces a 50-item log, the summary should be 5-7 items. Pick the signal. Leave the noise on disk.

The handoff point must be a hard boundary. Not "sometime in the morning." A fixed time. 6 AM. 8 AM. Whatever works. The human knows when the summary will arrive. They make space for it. The system knows when to compile the summary. It builds toward that moment.

Use async handoff to implement asynchronous learning. The overnight factory runs with yesterday's rules (Accumulated Corrections). It appends logs showing what worked and what failed. The morning summary flags repeated failures. The human reviews. The human updates decisions.md. By tomorrow night, the factory runs with better rules.

This pattern pairs with Lazy Loading. The overnight batch loads only the batch-processing skill. Minimal context. Fast work. The morning summary loads only the summarizer skill. Different agent. Different context. Same codebase.

The pattern also pairs with Append-Only Log. Every night, the factory appends to the coaching_log, the improvement_log, the factory_log. The logs grow. The morning summary reads the appended portions. Asks the human: are these results good. The human answers. The next morning's summary shows whether the feedback was incorporated.

Consider idempotency. If the machine crashes at 3 AM and restarts at 4 AM, it should resume where it left off, not redo work. This means each overnight task should be idempotent. Appending to a log is safe—duplicate appends are visible. Modifying a file is risky—duplicate modifications are not. Append-only pairs with async handoff.

Build visibility into the intermediate state. The human might not care about the 8 PM checkpoint. But the system should log it. If something goes wrong, the human can ask: "What happened at 8 PM." And the log answers. This is low cost. One append per checkpoint. High value. Traceability.

The handoff summary is not just output. It is input to the next cycle. The human's decisions become instructions for the next overnight run. The overnight system reads these instructions first thing. Incorporates them. Appends them to the decision log. Runs the next batch with improved understanding.

This pattern creates a cadence. Overnight work. Morning review. Human decisions. Overnight work. Every day, the system learns a little. Every night, it works a little smarter. This is not dramatic. But it compounds.

The risk of async handoff is becoming blind. The human stops looking at the summaries. The system drifts. Old rules persist. Improvements stop. Prevent this with ritual. Make the handoff time sacred. Block the calendar. Read every summary. It takes 10 minutes. The cost is tiny. The benefit is drift prevention.

Async handoff is not "fire and forget." It is disciplined handoff. The machine does its work. The human does theirs. The interface is one summary, one decision point, one synchronized moment per day. Everything else is async.
