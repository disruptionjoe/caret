# Incremental Profiling

## Notation

```
^^^anchored-agent
  ^intake       — one drip question per interaction, max
  ^observation  — passive; no user input required
  ^log          — corrections are highest-signal; append-only
```

Three channels feed one model over time. No upfront interview. No comprehensive form. The model grows by drip, observation, and correction. The notation encodes the three channels; the temporal learning loop — that profiling happens across many sessions, not in one pass — is a design constraint defined in the prose below.

## What it does

Builds a user profile incrementally through three channels:

1. **Drip questions.** One lightweight question per interaction, maximum. Not "what is your risk tolerance" but "did that summary hit the right level of detail." The answer trains the model. The question costs almost nothing.

2. **Passive observation.** The agent watches what you do. You spend three minutes on a document you said you'd ignore. You skim summaries today but wanted detail yesterday. Observations don't require input. They calibrate the model over time.

3. **Explicit capture on correction.** You say "that's not my voice." The agent writes it down. Corrections are the highest-signal input. An agent that assumes and gets corrected learns more than one that assumes and gets confirmation.

No friction upfront. Over fifty conversations, an anchored agent learns your voice, your priorities, your edge cases. The learning is ambient.

## When to use it

When you want a model that tracks real behavior over time. When upfront interviews are expensive or inaccurate. When you'll interact with the system repeatedly and depth comes from repetition.

When you want the agent to adapt without asking. You correct once. The agent internalizes it. Never again.

## When not to use it

When you need the model right now. Incremental profiling takes time. No shortcut. If accurate context is needed on the first interaction, use explicit intake and upfront questions.

When the user is temporary. Five minutes, never returns. The drip is wasted.

## Design notes

The pattern requires an anchored agent — memory that persists across sessions. Ephemeral agents are clean slates. They can't learn. Anchored agents carry the model.

The drip constraint matters: one question per interaction maximum. More and it becomes friction. You're not building a profile, you're conducting an interview. One per interaction stays ambient. Gets answered between the real work.

Corrections are the strongest signal. They teach faster than affirmations. Separate the corrections log from the model it produces — the log is evidence, the model is current belief.

The model should be visible. You should be able to read what the agent thinks it knows about you. You should see confidence levels. "Prefers summaries" at high confidence means something different than the same statement at low confidence. Transparency lets you spot drift before it compounds.

Implementation detail: the model must be queryable but not self-editable by the agent. The agent reads its own assumptions. It cannot change them directly. When it wants to update the model, it flags the observation. You confirm or reject. This prevents runaway self-correction.

The cost is time. Three months to build an accurate model. Six months for deep patterns. Slower than upfront intake. Also more accurate, more stable, and more resilient to contact with reality.

Relationship to **Accumulated Corrections**: both patterns learn from being wrong. Accumulated Corrections turns friction into standing rules. Incremental Profiling turns friction into a user model. The mechanism is the same: observe, correct, internalize.

Relationship to **Domain Anchor**: the profile can live inside a domain anchor as part of its persistent context. An anchored agent entering the domain reads both the domain state and the user model.

Relationship to **Append-Only Log**: the observations and corrections that feed the profile are append-only. No rewriting history. The model is derived from the log, not the other way around.
