# Voice Follows Domain

## Notation

```
^^^domain
  ^voice
```

The domain owns the voice. The agent borrows it.

## What it does

Routes output voice based on domain assignment, not agent identity. The Caret^ domain gets Caret^ voice. A consulting domain gets the consultant's voice. Same agent, different domains, different voices. A registry maps domains to voices. The registry is the source of truth.

Before the first word is written, the voice is already decided. Not by the agent. Not by the coordinator. By the domain the work belongs to.

## When to use it

Every content assignment. Every output generation. Any system where multiple agents work across multiple domains and voice consistency matters.

The moment you have two domains with different voice requirements and agents that might touch both, you need this pattern. Without it, agents default to their own style or the coordinator's style, and voice bleed is inevitable.

## When not to use it

Single-domain systems where there is only one voice. The routing is unnecessary — just embed the voice directly.

Also wrong when the platform supersedes the domain. Example: a personal blog uses the author's voice regardless of topic. The platform is the domain, not the content subject. In that case, voice follows platform, which is still voice-follows-domain — the platform *is* the domain.

## Design notes

Voice is not personality. It is constraint. Constraint on tempo, sentence length, vocabulary, what gets said and what stays silent. A domain that requires a specific voice requires a specific constraint set. The agent is a tool that must fit the constraint.

The registry exists because human memory fails at scale. Written once, consulted always. When a new domain enters the system, the registry gets a new line. No agent decides voice on the fly. No coordinator improvises. The registry is consulted; the decision is made.

The most common failure in multi-domain systems is voice bleed — an agent using Domain A's voice while working in Domain B. This pattern prevents it by making voice a first-class property of the domain, not the agent. The agent's own inclinations are irrelevant. The domain's voice wins.

Platform exceptions exist but follow the same logic. A personal newsletter uses the author's voice regardless of what it covers. The newsletter is the domain. Content subject is not. A project repo uses the project's voice. Files living in that repo use that voice. Migration of a file between repos triggers voice conversion. This is work. Document it.

The pattern breaks when domains have fuzzy boundaries. If a task could belong to Domain A or Domain B, voice routing fails unless the assignment is explicit. Solve this at the routing layer — assign a domain before work begins, not after.

Relationship to **Domain Anchor**: the anchor holds the voice assignment. This pattern is the routing rule. The anchor is the data structure.

Relationship to **Disposable Specialists**: specialists inherit voice from the domain, not from the coordinator. When a specialist is rotated out, the voice stays because the domain stays.

Relationship to **Accumulated Corrections**: voice mismatches are the most common correction in multi-domain systems. Those corrections become standing rules. The pattern that routes voice correctly from the start prevents the correction from ever being needed.
