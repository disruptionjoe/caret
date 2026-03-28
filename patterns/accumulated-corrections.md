# Accumulated Corrections

## Notation

```
^log
  ^learned
^rules
```

The log appends corrections. Rules are the standing policy derived from those corrections. Once a correction becomes a rule, it is permanent until explicitly revised.

## What it does

The system makes mistakes. A human corrects it. The correction is not a one-time fix. It becomes a standing rule that applies to all future work.

First time: "Use Caret^ voice for pattern files" is a correction for one piece of work. Second time: the system remembers and applies it without being told. Third time: the correction is enshrined as a permanent standing rule. Friction converts to policy.

## When to use it

When you have repeatable mistakes. When you notice yourself correcting the same thing multiple times. When a rule emerges through practice, not from first principles.

The pattern is most powerful when corrections come from the human reviewer. Real humans catching real drift. Those corrections are gold.

Use this for any system that needs to learn from being wrong: a writing system corrected on voice, a routing system corrected on skill selection, an agent corrected on how it interprets intent.

## When not to use it

When corrections are one-off edge cases that will never recur. When the rule-space is so large that accumulated corrections become unwieldy. When you're correcting the same thing every single turn — that suggests the underlying system is broken, not that you need a correction pattern. Fix the system.

## Design notes

The core trade-off is rigidity versus learning. Every correction accumulated is a constraint accepted. Enough constraints and the system becomes brittle. No constraints and the system repeats the same mistakes forever.

Separate the corrections log from the rules it produces. The log captures every time a human said "this is wrong." The rules file captures the standing policy derived from those corrections. The log is evidence. The rules are policy.

Set a threshold. After the same correction appears two or three times, elevate it to a standing rule. First correction might be a fluke. Third time is a pattern.

Keep rules human-readable. Prose, not data structures. "All Caret^ patterns must use the Caret^ voice: crisp, exact, contemptuous of waste" is more memorable and more enforceable than `{voice: "caret", tone: "dry"}`.

Do not accumulate contradictory rules. If a correction contradicts an existing rule, stop. Document the contradiction. Decide which wins. Update the rules, not the correction log.

Consider temporal rules. Some corrections apply forever. Some apply for a season. Timestamp every rule. Review them periodically. Prune rules that no longer fit the work.

Beware overcorrection. If the human corrects too much, too fast, the system becomes brittle — optimizing for approval rather than function. The best corrections are the ones that recur. The ones the system would reach independently if given more time.

The real power: the corrections make learning visible. Any reviewer can read the rule set and understand why the system works the way it does. "Why short sentences? Because the human corrected it three times and it became a rule." That explanation is better than "because the design doc said so."

Relationship to **Append-Only Log**: the corrections log is append-only. New corrections stack. Old corrections remain visible.

Relationship to **Domain Anchor**: standing rules live inside the domain anchor. They are the constraints the domain has learned.

Relationship to **Overnight Factory**: the factory's evaluator catches drift. Those catches become corrections. By next cycle, the system has incorporated the learning.
