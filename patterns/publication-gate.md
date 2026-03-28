# Publication Gate

## Notation

```
^^^worker ^autonomy7
  ^review
  ^log

^^reviewer ^verification9
  ^triage
```

Hard boundary between draft/build and anything public, sent, deployed, or published. The worker prepares. The reviewer — always human — decides.

## What it does

Nothing crosses the gate without explicit human approval. Work agents prepare, humans publish. Gate is disposition step — after work is done, it goes through review before it can be promoted to public.

Agents can draft, analyze, iterate, suggest, prepare. Only humans decide what becomes live, what ships, what the world sees.

## When to use it

When work affects public reputation, stability, or trust. When mistakes are expensive or permanent. When published content requires accountability that agents cannot bear.

When preparing for launch, publication, deployment, sending. When material will be read by people outside your immediate group. When reversal is costly.

Before any of: publishing to web, sending emails at scale, posting to social media, deploying code to production, sharing with external stakeholders, releasing reports or research.

## When not to use it

When agent can safely self-publish per domain rules. When governance already requires the gate upstream. When the gate adds bureaucracy without adding safety.

When work is purely internal draft or exploration. When agents have earned explicit publication permission for specific classes of work.

## Design notes

Gate governance is structural. It does not say whether to approve — that is human judgment. It says that approval must happen.

The night factory prepares. Joe publishes. Agents prepare. Humans publish.

This maps to organizational governance: when decisions affect brand, safety, or trust, humans decide. Agents execute decisions, prepare evidence, suggest direction. Humans sign off.

Gate prevents silent escalation. Agents cannot gradually shift from draft to production. They cannot normalize publication over time. Each item requires explicit restart of human attention.

Gate forces clarity. Before gate: agent knows it is preparing, not shipping. After gate: decision is explicit and logged. No ambiguity about whether something was published "by accident" or "gradually adopted."

Gate scales with automation depth. Single agent? Gate is simple conversation. Hundred agents prepping work daily? Gate becomes workflow bottleneck. Optimize by clarifying which work must always go through gate (anything public) and what can auto-promote (internal use, logs, metrics).

Three practical patterns:

**Per-item gate.** Every piece of work waits. Human reviews, approves, rejects, or revises. Costly. Use when mistakes are expensive.

**Batch gate.** Agents prep multiple items. Humans review batch together. Efficient for high-volume routine work. Use when categories of work have similar risk.

**Domain gate.** Certain work types always gate (published docs, customer email, code shipping). Other types auto-promote (internal notes, draft analysis). Use when categories are clear and stable.

Publication gate is not about speed. It is about accountability. It is about knowing that every public thing was consciously chosen.

Related to **Scope Constraint** — publication scope is a specific kind of constraint. Work agents have no publish permission. Only humans cross the gate.

Related to **Context Refresh** — when refreshing from draft to publication context, clear draft-phase reasoning. New instance focuses only on published requirements, not exploration.

Failure mode: gate becomes theater. Humans approve without reading. Button-clicking ceremony. Prevent by making reviews lean: agent provides summary, human spot-checks, human decides. Not every line needs human eyes, but the shape and impact must.

Failure mode: gate gets bypassed. "Just ship it, we'll review later." Defeats pattern. Gate is only effective if crossing it is the only way to publish. Requires platform enforcement: published artifacts cannot appear until gate opens.

Failure mode: gate too fine-grained. Every sentence needs approval. Agents cannot ship anything. Gate exists to protect impact, not to slow work. Optimize scope: does this item need approval, or does this category?

The trade-off: **Safety vs. velocity.** Gate slows work to ensure humans decide impact. If safety is low priority, skip the gate. If impact matters, pay the cost of human decision.
