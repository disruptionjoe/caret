# Append-Only Log

## Notation

```
^log
```

New entries stack below. No edits. No deletions. The structure is the audit trail.

## What it does

Captures state changes as a permanent sequence. Each entry carries a timestamp. Later entries do not overwrite or revise earlier ones. The log grows monotonically. If an error was logged, the error stays. If a correction occurred, the correction is appended as a new entry, not inserted retroactively.

The log is evidence, not a journal. Write it like that.

## When to use it

When history itself is the contract. Factory logs that prove work happened at specific times. Decision records where you need to know *when* each change occurred and *why*, not just what the current state is. Coaching logs that show learning progression. Memory files that accumulate insights without forgetting what came before.

Use this when the human needs to understand not just the present but the path to the present.

## When not to use it

When the current state is all that matters and the path is noise. When storage is constrained. When you need to frequently rewrite past entries — then you want a mutable document, not a log.

When the log grows unwieldy, split it: archive the old section and start fresh. Mark the archive clearly.

## Design notes

The core trade-off is growth versus reliability. A log that never shrinks will eventually consume resources. A log that allows editing sacrifices auditability.

Append is cheaper than mutation. A new line costs almost nothing. Reaching backward to change something requires reading, parsing, modifying, rewriting. Append is linear. Mutation is friction.

Timestamp every entry. Not just the date — the time. If two entries happened in the same minute, you need granularity to know order. A log without timestamps is a story someone is telling. Stories drift.

Keep entries dense. One line per significant event. If you need to explain, append more lines. But do not editorialize the past. Do not smooth over mistakes by rewriting what came before.

Consider rotation. When a log reaches a size threshold — one month, a few hundred entries, whatever fits your rhythm — archive it with a clear marker and start fresh. The archive becomes immutable. The new log starts from zero. This keeps any single log small and fast to read while preserving full history.

The append-only log is a foundation. Stack other patterns on top of it. **Accumulated Corrections** learns by appending to a corrections log. **Async Handoff** summarizes what was appended overnight. **Domain Anchor** uses the log as domain memory across sessions.

The pattern enforces honesty. A system that cannot edit the past must own what it did.
