# Incremental Profiling

## Notation

```
^^^ [anchored agent]
  ^ drip: one question per day
  ^ observation: passive collection
  ^ update: explicit capture on correction
```

The three channels feed a single model. No upfront interview. No comprehensive form. Water drips. The model grows.

## What it does

Builds a user profile incrementally through three channels: drip questions (max one lightweight personal question per daily interaction), passive observation during conversation (inferences from what you do and say), explicit capture on correction (when you correct an assumption, the correction becomes model fact).

No friction upfront. No "tell me about yourself" forms. Instead, over fifty conversations, an anchored agent learns your voice, your priorities, your edge cases. The learning is ambient. The agent notices. The agent remembers.

## When to use it

When you want a model that tracks real behavior over time. When upfront interviews are expensive or inaccurate anyway. When you're going to interact with the system repeatedly and depth comes from repetition.

When you want the agent to adapt without asking. You say "that's not right" once. The agent internalizes it. Never again.

## When not to use it

When you need the model right now. Incremental profiling takes time. No shortcut. If you need accurate context on the first interaction, use explicit intake and upfront questions.

When the user is temporary. Spends five minutes, never returns. The drip is wasted.

## Design notes

Incremental profiling is a response to the friction of upfront learning. Traditional systems ask: "Tell me your top three priorities. What's your decision-making style. How much detail do you prefer." Users hate this. They give surface-level answers. They change their minds. The model is stale in three weeks.

The alternative is ambient learning. You don't ask. You watch. An agent that sees you correct it twice on a topic learns faster and more accurately than one that asked you a five-point scale question.

The pattern requires an anchored agent (memory that persists). Not an ephemeral one. Ephemeral agents are clean slates. They can't learn. Anchored agents carry session-to-session memory. That's where the model lives.

Three channels in order of strength:

**Drip questions.** One question per day maximum. Must be lightweight. Not "What is your risk tolerance" but "Did that summary hit the right level of detail." The answer trains the model. The question itself costs almost nothing. The user barely notices. But done daily, you have fifty data points in two months.

The constraint is important: one per day maximum. More and it becomes friction. You're not building a profile, you're conducting an interview. One per day stays ambient. Stays ignorable. Gets answered between the real work.

**Passive observation.** The agent watches what you do. You spend three minutes on a document that you said you'd ignore. You asked for detail yesterday but skim summaries today. You're engaged with one domain but delegating another. These observations don't require your input. They just happen. They're noisy. But over time, they calibrate the model.

Example: An agent notices you read the full text of every third email but delete the rest unread. Not "what's your email style" question. Just observation. Over six months, the agent learns your triage pattern and can predict which emails you'll care about with eighty percent accuracy.

**Explicit capture on correction.** You say "That's not my voice." The agent writes it down. You say "I don't want that level of detail." The agent updates the model. These are the highest-signal inputs. They're corrections against a wrong assumption. They teach faster than affirmations. An agent that assumes and gets corrected learns more than an agent that assumes and gets confirmation.

The three channels work together. Drip questions prime the model with rough shape. Passive observation fills in texture and edge cases. Corrections sharpen the boundaries.

Implementation detail: the model must be queryable but not editable by the agent itself. The agent can read its own assumptions. It cannot change them directly. When an agent wants to update the model, it flags the observation for you. You confirm or reject it. This prevents the agent from drifting its own model into uselessness through runaway self-correction.

Another detail: timestamp the learning. A correction from two weeks ago carries more weight than passive observation from three months ago. Recency matters. But also weight the frequency. If you've made the same correction five times, it's a hard constraint, not a soft preference.

The pattern requires discipline on your end: actually correct the agent when it's wrong. If an agent makes an assumption and you ignore it, you're training it that the assumption was right. Silence is consent in incremental profiling. So correct actively. Correct early.

One more detail: the model should be visible to you. You should be able to read what the agent thinks it knows about you. You should be able to see the confidence levels. "This user prefers summaries" at ninety percent confidence means something different than the same statement at forty percent. Transparency lets you spot drift before it compounds.

The cost is time. Three months to build an accurate model. Six months to get deep patterns. This is slower than upfront intake. It's also more accurate, more stable, and survives contact with reality better. You trade speed for accuracy and durability.
