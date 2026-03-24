# Append-Only Log

## Notation

```
^log: [timestamp] [entry]
```

Where log is an immutable sequence. No edits. No deletions. New entries stack below. The structure is the audit trail.

## What it does

Captures state changes as a permanent sequence. Each entry carries its timestamp. Later entries do not overwrite or revise earlier ones. The log grows monotonically. If an error was logged, the error stays in the history. If a correction occurred, the correction is appended as a new entry, not inserted retroactively.

## When to use it

When history itself is the contract. Coaching logs that show learning progression. Memory files that accumulate insights without forgetting what came before. Factory logs that prove work happened at specific times. State improvement logs where you need to track _when_ each change occurred and _why_, not just what the current state is.

Use this when the human needs to understand not just the present but the path to the present.

## When not to use it

When the current state is all that matters and the path is noise. When storage is severely constrained. When you need to frequently mutate past entries. When the log becomes so large it becomes unwieldy to read. Then split it: archive the old and start fresh, but mark the archive clearly.

## Design notes

The core trade-off is growth versus reliability. A log that never shrinks will eventually consume resources. A log that allows editing sacrifices auditability.

The pattern assumes append is cheaper than mutation. In most systems, it is. A new line costs almost nothing. Reaching backward to change something requires reading, parsing, modifying, rewriting. Append is linear. Mutation is friction.

Timestamp every entry. Not just the date—the time. If two entries happened in the same minute, you need granularity to know the order. A factory log without timestamps is just a story someone is telling. A story drifts.

Use append-only logs for systems that need proof. Legal logs. Audit trails. Decision records. A human reviewer should be able to read the entire sequence and say: this is what happened, in order, with evidence.

The log is not a journal. It is evidence. Write it like that.

Keep entries dense. One line per significant event. If you need to explain, append more lines. But do not editorialize the past. Do not smooth over mistakes by rewriting what came before.

Consider rotation. When a log reaches a size threshold—one month, 10,000 entries, whatever fits your rhythm—archive it with a clear marker and start a new one. The archive becomes immutable. The new log grows from zero again. This keeps any single log small and fast to read while preserving the full history.

JSON is a reasonable format. Each entry can be `{timestamp: ISO8601, event: string, context: object}`. Or simple plaintext: one line per entry, structured so machines can parse it later if needed.

The append-only log is a foundation. Stack other patterns on top of it. Accumulated Corrections learns by appending to a corrections log. The Async Handoff summarizes what was appended overnight. The Lazy Loading system may reference the log to understand which skills were most recently used.

The pattern enforces honesty. A system that cannot edit the past must own what it did. This creates a kind of accountability that systems without append-only logs lack.
