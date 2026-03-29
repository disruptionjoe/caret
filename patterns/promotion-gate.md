# Promotion Gate

## Notation

```
^log
  ^observation
  ^threshold
^rules
  ^promoted
```

Observations accumulate in the log. When a threshold is met, the observation is promoted to a standing rule. The gate is the threshold.

## What it does

Controls how raw learning becomes stable guidance. Agents observe things. They notice patterns. They receive corrections. Without a promotion gate, those observations either die when the session ends or silently infiltrate the system's behavior without deliberate adoption.

The gate requires an explicit decision: this observation has recurred enough, or carries enough weight, to become a standing rule. Until that threshold is crossed, the observation stays in the log as evidence — visible, timestamped, but not binding.

## When to use it

When the system learns from experience and you need to control what gets absorbed into permanent behavior.

Specific triggers:

- Corrections keep recurring and you want them to become rules automatically after N occurrences
- You've found stale or contradictory rules and suspect they were promoted without deliberation
- The system's behavior has drifted and no one can explain why — silent promotion happened
- You need an audit trail for why the system behaves the way it does

## When not to use it

When the system does not learn. Static rule sets that are authored by humans and never updated from experience do not need promotion gates. The gate exists for systems that accumulate corrections over time.

Also wrong when speed matters more than accuracy. If the system must adapt instantly to every correction — zero tolerance for repeated mistakes — then every correction is a standing rule on first occurrence. The threshold is 1, which is no gate at all.

## Design notes

The core trade-off is adaptability versus stability. Promote too eagerly and the system becomes brittle — every fluke correction hardens into permanent policy. Promote too slowly and the system repeats mistakes while evidence piles up in the log.

**Threshold design.** The simplest threshold is count: promote after the same correction appears three times. More sophisticated thresholds weight by source (human correction > automated detection), severity (public-facing > internal), and recency (recent corrections matter more than old ones).

**Promotion is not copying.** Promoting an observation to a rule means distilling it. The log entry says "Joe corrected the voice on this pattern file." The promoted rule says "All Caret^ patterns must use the Caret^ voice." The rule is sharper, broader, and more actionable than the raw observation.

**Demotion exists.** Rules that no longer apply should be retired, not silently ignored. If a promoted rule stops being enforced or starts creating friction, demote it back to an observation with a note explaining why. Timestamp the demotion. The audit trail matters.

**Supersession.** When a new rule contradicts an existing rule, the system must choose. Never accumulate contradictory rules. Resolve the conflict, retire the old rule, promote the new one. Document the reasoning. See **Source of Truth Hierarchy** for precedence conventions.

**The gate prevents silent drift.** Without it, every agent observation has equal weight. A one-time correction from a human and a statistical fluke from an automated check both silently reshape behavior. The gate forces: "is this real? Has it recurred? Does it deserve to be policy?"

Relationship to **Accumulated Corrections**: corrections are the raw material. The promotion gate is the mechanism that turns them into standing rules.

Relationship to **Anchored Memory Stack**: promotions move observations up the stack — from log (cold evidence) to summary (hot heuristic) to charter (stable rule). Each layer has a different mutation rate and a different promotion threshold.

Relationship to **Immutable State**: promoted rules live in the immutable layer. They are protected from casual modification. Changing a promoted rule requires the same deliberation that promoting it required.
