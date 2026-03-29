# Anchored Memory Stack

## Notation

```
^^^agent ^grip9
  ^charter
  ^summary
  ^log
```

Three layers. The charter is stable identity. The summary is hot working memory. The log is cold evidence.

## What it does

Gives a long-lived agent a structured memory that survives across sessions without loading everything every time. The stack has three layers, each with a different read frequency and mutation rate:

**Charter** — what the agent is, what it owns, what it refuses. Rarely changes. Always loaded. This is identity.

**Summary** — current heuristics, active state, recent lessons. Changes often. Always loaded. This is working memory.

**Log** — append-only record of decisions, corrections, outcomes. Grows continuously. Loaded on demand. This is evidence.

The agent reads charter and summary by default. It dips into the log only when it needs evidence for a specific decision. This keeps the hot path lean while preserving full history.

## When to use it

Any agent that persists across sessions and needs to remember what it learned.

Specific triggers:

- Domain stewards that accumulate knowledge over weeks or months
- Coordinators that make routing decisions informed by past outcomes
- Any agent where "it keeps forgetting" is a recurring complaint
- Systems where the context window cannot hold the full history but the agent still needs continuity

## When not to use it

Ephemeral agents. If the agent is born, works, and dies in one session, a memory stack is overhead. The whole point of disposable specialists is that they carry no memory.

Also wrong for agents that genuinely need full context every time. Some synthesis tasks require the complete record. For those, load the log. But make that an explicit choice, not the default.

## Design notes

The core trade-off is recall versus cost. Loading everything gives perfect recall but burns context budget. Loading nothing keeps costs low but produces an agent that cannot learn. The three-layer stack is the middle path: always load the cheap stuff (charter + summary), load the expensive stuff (log) only when needed.

**Charter stability matters.** If the charter changes frequently, something is wrong. Either the agent's role is unclear or the system is using the charter as a scratchpad. Charters should change on the order of weeks or months, not sessions.

**Summary compaction.** The summary is the most dangerous layer. It drifts. It grows. It accumulates stale heuristics. Regular compaction is essential: review the summary, prune what no longer applies, sharpen what remains. Without compaction, the summary becomes a second log — defeating the purpose.

**Log rotation.** Append-only logs grow forever. Set a rotation convention. Archive old entries. Keep the active log short enough that a targeted read is fast. The archive preserves history; the active log serves working decisions.

**Promotion path.** Observations in the log get promoted to heuristics in the summary. Heuristics in the summary get promoted to standing rules in the charter. Each promotion is an explicit decision, not silent drift. See **Promotion Gate** for the mechanism.

Relationship to **Domain Anchor**: the domain anchor is the canonical example of an anchored memory stack. Purpose, voice, goals, log, rules — that is a stack with the same three layers under different names.

Relationship to **Append-Only Log**: the log layer of this stack is an append-only log. This pattern describes the stack; that pattern describes the log.

Relationship to **Accumulated Corrections**: corrections enter through the log, get promoted to the summary as heuristics, and eventually harden into charter rules. The memory stack is the container; accumulated corrections is the learning process.
