# Source of Truth Hierarchy

## Notation

```
^^^agent ^grip9
  ^charter     — law layer, wins all conflicts
  ^summary     — working layer, wins over log
  ^rules       — standing policy, wins over observations
  ^log         — evidence layer, informs but does not override
```

Precedence flows top to bottom. Higher layers override lower layers. Lower layers inform higher layers through promotion.

## What it does

Defines which file wins when two files disagree. In any system with multiple layers of guidance — charters, summaries, rules, decision logs, outcome records — conflicts are inevitable. Without a declared hierarchy, agents resolve conflicts by guessing, by recency, or by whichever file they read last.

The hierarchy makes precedence explicit. The charter is law. The summary is working interpretation of that law. Rules are standing policy derived from experience. The log is raw evidence. When they conflict, the higher layer wins. Always.

## When to use it

When the system has multiple files that can influence agent behavior and you've seen agents resolve contradictions inconsistently.

Specific triggers:

- A rule in the decision log contradicts a statement in the charter
- An agent's summary has drifted from the charter's stated purpose
- Two files give different guidance and the agent picks one arbitrarily
- You need to explain to a reviewer or auditor why the system behaves a certain way
- Promoted rules have started overriding charter-level constraints

## When not to use it

Single-file systems. If the agent reads one instruction file, there is no hierarchy to declare. The hierarchy pattern exists because multi-layered systems create ambiguity.

Also wrong when all layers are equally authoritative by design. Some systems intentionally avoid hierarchy — every contributor has equal weight, every document is equally binding. Those systems resolve conflicts through consensus, not precedence. Different architecture, different pattern.

## Design notes

The core trade-off is clarity versus flexibility. A strict hierarchy makes conflicts resolvable but makes lower layers feel powerless. A loose hierarchy preserves flexibility but lets contradictions fester.

**The charter is the constitution.** It changes rarely and only through deliberate revision. If a correction contradicts the charter, the correction is wrong — or the charter needs revision. Both are valid outcomes, but the decision must be explicit. Silently overriding the charter through accumulated corrections is drift.

**Summaries are interpretive, not authoritative.** The summary says "here is what we currently believe the charter means for today's work." It is allowed to simplify, paraphrase, and focus. It is not allowed to contradict. If the summary conflicts with the charter, update the summary.

**Rules are promoted observations.** They carry real authority — agents must follow standing rules. But rules live below the charter. A rule that contradicts the charter is either wrong or evidence that the charter needs revision. The resolution is explicit either way.

**The log never wins.** The log is evidence. It informs decisions. It does not make them. An observation in the log might say "this approach failed three times." That is evidence. The rule derived from it says "do not use this approach." The rule wins, not the log entry. The log explains why the rule exists.

**Supersession protocol.** When updating the hierarchy, document what changed and what it supersedes. "Rule X is retired because Charter revision Y made it redundant." The audit trail prevents ghost rules — retired policies that no one remembers retiring but that still influence behavior through muscle memory.

**Cross-domain precedence.** Within a domain, the hierarchy is clean. Across domains, it gets complicated. When Domain A's charter conflicts with Domain B's rules, which wins? Answer: neither. Cross-domain conflicts escalate to the orchestrator or human. The hierarchy operates within its scope.

Relationship to **Anchored Memory Stack**: the stack is the container. The hierarchy defines precedence within that container. Charter = stable identity (top). Summary = hot memory (middle). Log = cold evidence (bottom).

Relationship to **Promotion Gate**: the gate controls upward movement through the hierarchy. Observations get promoted to rules. Rules get promoted to charter amendments. Each promotion crosses a layer boundary.

Relationship to **Immutable State**: the law layer of immutable state maps to the charter layer of the hierarchy. Both are protected from casual modification.

Relationship to **Domain Anchor**: every domain anchor implicitly uses this hierarchy. Purpose and voice are charter-level. Goals and rules are policy-level. The log is evidence-level.
