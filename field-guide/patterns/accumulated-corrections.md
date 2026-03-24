# Accumulated Corrections

## Notation

```
^decision: [rule]
^learned: [timestamp] [correction origin] [new rule]
```

A decision log captures standing rules. A learned log appends corrections that became rules. Once logged as learned, the correction is permanent policy.

## What it does

The system makes mistakes. A human corrects it. The correction is not a one-time fix. It becomes a standing rule that applies to all future work.

The first time: "Use Caret^ voice in all pattern writing" is a correction for one piece of work. The second time: the system remembers this correction and applies it to new pattern writing without being prompted again. The third time: the correction is enshrined in decisions.md as a permanent standing rule. Friction converts to policy.

## When to use it

When you have repeatable mistakes. When you notice yourself correcting the same thing multiple times. When a rule emerges through practice, not from first principles.

Use this for systems that need to learn from being wrong. A writing system that gets corrected on voice, tone, format. A routing system that gets corrected on which skill to invoke for which input. An agent that gets corrected on how to read data or interpret intent.

The pattern is most powerful when corrections come from the human reviewer. Real humans catching real drift. Those corrections are gold.

## When not to use it

When you have no repeatable work. When corrections are one-off edge cases that will never occur again. When the rule-space is so large that accumulated corrections becomes unwieldy.

Do not use this if you are correcting the same thing every single turn. That suggests the underlying system is wrong, not that you need to learn. Learn when there is a pattern. Fix the system when there is chaos.

## Design notes

The core trade-off is rigidity versus learning. Every correction you accumulate is a constraint you accept. Enough constraints and the system becomes brittle. It cannot adapt. But no constraints and the system repeats the same mistakes forever.

The pattern works because humans catch what metrics miss. A automated test catches crashes. A human reviewer catches when the voice drifts, the structure breaks down, the logic becomes sloppy. Those catches are the real improvement signal.

Separate the corrections log from the rules they become. A corrections.log file (append-only) captures every time a human said "this is wrong." A decisions.md file (edited, maintained) captures the standing rules derived from those corrections. The log is evidence. The decisions file is policy.

The log entry should capture: what was corrected, who corrected it, when, and what the correct behavior should be. `[timestamp] [work_id] [corrected_field] [old_value] [new_value] [explanation]`. This gives context. Later, when you wonder why a rule exists, the log explains it.

Set a threshold. After the same correction appears N times in the log, elevate it to decisions.md. What is N? 2 or 3, probably. First correction might be a fluke. Third time is a pattern.

Keep decisions.md human-readable. Not a data structure. Prose. Prose is easier to remember. "All Caret^ patterns must use the Caret^ voice: crisp, exact, dry, contemptuous of waste" is more memorable than `{voice: "caret", tone: "dry"}`.

Do not accumulate contradictory rules. If a correction contradicts an existing rule, stop. Document the contradiction. Decide which rule is right. Update the rules, not the correction log.

Consider temporal rules. Some corrections should apply forever. Some should apply for a season. A correction from six months ago might be outdated. Timestamp every rule. Review them quarterly. Prune rules that no longer fit the work.

The pattern pairs with Append-Only Log. The corrections log is append-only. New corrections stack. Old corrections remain visible. You can see the evolution of what the system has learned.

The pattern also pairs with Async Handoff. The overnight batch might run with old rules. The morning review catches mistakes. Those mistakes are logged as corrections. By next night, the system has incorporated the learning. Asynchronous improvement. The human decides. The system remembers.

Beware overcorrection. If the human corrects too much, too fast, the system becomes brittle. It optimizes for approval rather than function. The best corrections are the ones that recur. The ones that the system would reach independently if given more time.

This pattern assumes the human reviewer is right more often than the system is. This is usually true. But it is not always true. Build in a mechanism to challenge corrections. "Is this rule still valid?" Every few months. Have the human re-confirm.

The real power of this pattern is that it makes learning visible. The decision log is public. Any reviewer can read it and understand why the system works the way it does. "Why does Caret^ use short sentences? Because the human corrected it three times and it became a rule." That is a better explanation than "because the design doc said so."

Accumulated corrections turn friction into wisdom. The system that gets corrected and remembers outpaces the system that gets corrected and forgets.
