# Triggered Review

## Notation

```
^review
  ^trigger: risk | uncertainty | external-consequence
```

Review fires when a threshold is crossed. Not on every output. Not on a schedule. On conditions.

## What it does

Replaces blanket review with conditional review. Instead of reviewing everything (expensive, numbing) or reviewing nothing (dangerous), the system defines trigger conditions that activate review only when it matters.

Three default trigger categories:

**Risk** — the output could cause harm if wrong. External-facing content, financial decisions, irreversible actions.

**Uncertainty** — the agent is not confident. Novel domain, ambiguous instructions, conflicting signals.

**External consequence** — the output touches the outside world. Publishing, sending, deploying, committing.

When a trigger fires, review activates. When no trigger fires, the work flows through without review overhead.

## When to use it

When review has become ceremony. When every output gets reviewed because the system does not know which outputs need it. When review fatigue is setting in and reviewers are rubber-stamping because the volume is too high.

Specific triggers:

- The review queue is growing faster than the team can clear it
- Most reviewed items pass without changes
- Reviewers are spending equal time on trivial and critical outputs
- The cost of review is slowing the pipeline without proportional quality benefit

## When not to use it

When everything is high-risk. If every output touches the outside world or carries real consequences, blanket review is correct. The pattern assumes most outputs are low-risk and a minority need scrutiny.

Also wrong in early-stage systems where you don't yet know what's risky. In that phase, review everything until patterns emerge. Then switch to triggers once you can articulate the conditions.

## Design notes

The core trade-off is safety versus velocity. Blanket review is maximally safe and maximally slow. No review is maximally fast and maximally reckless. Triggered review targets the sweet spot: fast on routine work, careful on consequential work.

**Define triggers explicitly.** Vague triggers ("review when important") are the same as no triggers. Good triggers are binary: either the condition is met or it is not. "Output will be published externally" is a clear trigger. "Output is significant" is not.

**Trigger categories are starter set, not canon.** Risk, uncertainty, and external consequence cover most cases. Your system may need others: regulatory compliance, cross-domain impact, budget threshold. Add what your workflow needs.

**The absence of review is a signal, not an oversight.** When an output ships without review, the system is saying: "this met no trigger conditions." If that turns out to be wrong — if an unreviewed output causes a problem — that is a correction. The correction produces a new trigger. The system gets smarter. See **Accumulated Corrections**.

**Fresh-eyes review is expensive.** When a trigger fires, the review itself should match the severity. Low-risk triggers get a quick pass (`^review3`). High-risk triggers get deep scrutiny (`^review8`) or a full fresh-eyes boundary (`^^^^`). Not all triggered reviews need the same depth.

**Review theater is the enemy.** If review exists because "we always review" rather than because something specific needs checking, the pattern is not working. Periodic audits of trigger coverage help: are the triggers catching the right things? Are unreviewed outputs staying clean?

Relationship to **Publication Gate**: the publication gate is a specific instance of triggered review where the trigger is "this will be published externally."

Relationship to **Overnight Factory**: the factory evaluator uses triggered review. It does not review every line of output. It spot-checks, verifies voice, checks rule compliance. Those are trigger conditions.

Relationship to **Disposition Gate**: disposition gates route work. Triggered review gates quality. They often work together: the disposition gate routes, and the review trigger decides whether the routed work needs scrutiny before proceeding.
