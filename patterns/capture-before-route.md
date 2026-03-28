# Capture Before Route

## Notation

```
^^^intake ^grip9 ^scope3
  ^extract

^^^router ^depth7
  ^route
  ^triage
```

Intake captures raw. Router decides later. Two agents, two moments, no premature interpretation.

## What it does

Splits intake and routing into two operations by different agents at different times. Intake agent captures raw input—email, message, file—without judgment. Stores one file per arrival. Writes extraction header for quick review. Hands off to routing agent later. No decision at capture time.

## When to use it

When you need a complete record of all arrivals. When intake rate is bursty and you want to decouple arrival from processing. When humans must review before the system acts downstream. When you need backpressure: intake can keep working while routing catches up. When you can afford latency in exchange for completeness.

## When not to use it

When you need real-time routing. When disk is constrained and you can't buffer everything. When you need to prevent duplicates and can only make one pass. When the system is simple enough that single-shot routing at intake is sufficient.

## Design notes

Separation of concerns. Intake is dumb. It reads input and writes files. Nothing else. No parsing. No categorizing. No deciding. It's a pump, not a filter.

The extraction header is metadata for the review agent. Enough to route without re-reading the whole payload. Subject line. First paragraph. Sender. Date. File size. Type. Signals, not summaries.

Original text stays as-is. Full email. Threading. Attachments. Noise and all. You may learn later that what looked like noise was the signal. Preserve it.

Naming is policy. Use ISO 8601 timestamps plus source ID: `/data/intake/2026-03-27T14:30:00Z-email-alice@example.com.md`. Tells you arrival time and origin without opening the file.

Restrict the intake agent. Read from source. Write to /data/intake/. Nothing else. No downstream access. No authority to approve or classify. If intake fails, you lose one item. If intake routes, you waste cycles on one misclassified item. The blast radius is small.

Review runs on schedule or on demand. Daily. Hourly. Per-user-request. Reads each file in /data/intake/. Checks the extraction header. Makes disposition. Moves file out of /data/intake/. Keep it transient, not a database.

Duplicates are your problem to solve. If the same email arrives twice, intake captures it twice. Review must detect and handle it. Good: deduplication lives in one place. Not scattered across ten intake agents.

Backpressure is automatic visibility. Items accumulate in /data/intake/. Count the files. See the queue depth instantly. Slow down intake or spin up more review agents. The separation buys you control.

Latency is the cost. Time passes between arrival and action. Acceptable for batch. Unacceptable for urgent. Know which you are. If you need both fast and slow paths, hybrid: fast-path for urgent items, capture-before-route for the rest.

Storage is the other cost. Every item takes space. High-volume + large payloads = full disk. Implement cleanup: delete after review or after time limit or both. Don't let it grow unbounded.

Make the extraction header machine-readable. YAML or JSON. Let the review agent parse it fast without opening the full file. Speed. Focus.

Contrast with `decision-tree-router`: a router decides and acts at arrival time, hot and immediate. Capture-before-route preserves everything and decides later, cool and complete. Router sacrifices fidelity for speed. Capture sacrifices speed for fidelity.
