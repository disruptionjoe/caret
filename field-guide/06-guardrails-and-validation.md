# Guardrails and Validation

## Questions for Joe

- OpenAI has the most structured guardrails implementation (input guardrails, output guardrails, can block execution). Should ACON adopt OpenAI's taxonomy or stay more general?
- Eval, guardrails, and validation overlap. The research suggests they're distinct but the boundaries are blurry in practice. Should this entry try to draw a hard line, or acknowledge the overlap and focus on when each concept applies?
- "Deterministic scaffolding" from your existing glossary is a related concept (offload predictable checks to scripts, not the model). Reference it here or treat it as a separate design philosophy entry?
- How much should this entry address safety/security guardrails vs quality/correctness validation? The research covers both but they have different audiences and stakes.

---

> Mechanisms for checking, constraining, and validating what an agent does — but "guardrail," "validation," and "eval" mean different things in different contexts, and the boundaries between them affect how you design quality assurance.

## Status

Established (concepts are stable), but fragmented (scope and naming vary)

## What problem this helps you think about

When you need to make sure an agent doesn't do something harmful, produce incorrect output, or drift from its instructions, you'll reach for "guardrails." But the term covers a wide range of mechanisms — from hard-coded input validation to runtime behavior monitoring to post-hoc evaluation — and different ecosystems scope it differently. Knowing which mechanism you need prevents over-engineering simple checks and under-engineering critical safety layers.

## Terms in this cluster

| Term | Used by | Meaning in that context | Source |
|------|---------|------------------------|--------|
| Guardrails (input) | OpenAI Agents SDK | Validation that runs on the input before the agent processes it. Can block execution if the input fails checks. | OpenAI Agents SDK guardrails docs |
| Guardrails (output) | OpenAI Agents SDK | Validation that runs on the agent's output before it's returned. Can reject, transform, or flag outputs. | OpenAI Agents SDK guardrails docs |
| Guardrails (general) | General usage | Any mechanism that constrains agent behavior — often used loosely to mean "safety checks" without specifying where in the pipeline they run. | Widespread informal usage |
| Validation | General usage | Checking that output meets defined criteria. Can be structural (is the JSON valid?), semantic (does the answer make sense?), or procedural (did it follow the right steps?). | General software engineering |
| Eval | OpenAI, general usage | Evaluating agent performance against benchmarks or test cases. Typically post-hoc (after the agent has run), not inline (during execution). "Eval-driven design" uses evaluation results to improve prompts and agent behavior. | OpenAI cookbook; widespread usage |
| Reflection / self-critique | Academic (Reflexion), general | The agent evaluating its own output and revising. Uses linguistic feedback rather than external validation. Episodic memory of past failures can improve future performance. | Reflexion paper (2023); practitioner implementations |
| Hooks | Anthropic (Claude Code) | Middleware that can inspect or modify tool calls before or after execution. Can be used to implement guardrails at the tool level. | Claude Code hooks documentation |
| Tracing | OpenAI, LangChain | Recording the agent's execution path for debugging and evaluation. Not a guardrail itself, but provides the data needed for post-hoc eval. | OpenAI tracing docs; LangSmith |

## Key distinctions

**Three layers of quality assurance, not one:**

1. **Inline guardrails** — run during execution. They check inputs/outputs in real time and can block, redirect, or transform. These are safety nets. OpenAI's input/output guardrails and Claude Code's hooks are examples.

2. **Critique/reflection loops** — run as part of the workflow. The agent (or another agent) reviews the work before it's final. Not a hard block — more like a review step that can trigger revision. The "fresh-eyes review" pattern is a specific implementation.

3. **Evaluation (eval)** — run after execution. Measures performance against benchmarks, test cases, or human judgment. Evals don't prevent bad outputs in real time; they improve the system over time by identifying failure patterns.

These layers serve different purposes and run at different times. A system that relies only on evals has no real-time protection. A system that relies only on guardrails can't improve systematically.

**The "guardrail" vs "validation" distinction** is mostly about scope: "guardrail" implies constraining behavior (preventing bad things), while "validation" implies checking correctness (confirming good things). In practice they overlap, but the framing affects design: guardrail-thinking leads to blocklists and safety checks; validation-thinking leads to test suites and acceptance criteria.

**Reflection is an agent-internal mechanism.** Unlike external guardrails or evals, reflection happens within the agent's own reasoning loop. The Reflexion paper formalized this: linguistic feedback + episodic memory of past failures enables the agent to improve across attempts. This is powerful but unreliable — the agent may "reflect" superficially without actually catching errors.

## How major ecosystems use this

### OpenAI
Structured guardrails in the Agents SDK: input guardrails (validate before processing), output guardrails (validate before returning). Can run alongside agents or block execution. Also emphasizes "eval-driven system design" — use evaluation results to iteratively improve prompts, tools, and agent behavior.

### Anthropic
Hooks system in Claude Code allows middleware-style interception of tool calls. Permission modes (allow/ask/deny) serve as tool-level guardrails. Formal guidance on context engineering includes validation strategies. No named "guardrail" framework, but the building blocks exist.

### LangChain / LangGraph
No dedicated guardrails framework in the same sense as OpenAI, but human-in-the-loop workflows enabled by LangGraph's persistence serve a similar function — the workflow pauses for human validation at critical points. LangSmith provides tracing and evaluation infrastructure.

### Academic
Reflexion (2023) formalizes self-critique as a learning mechanism. ReAct interleaves reasoning and action, enabling the agent to catch errors during execution rather than only after. These patterns are widely implemented but usually informally.

## Why the distinction matters in practice

If you only build guardrails (real-time checks) without evals (systematic measurement), you'll catch obvious errors but never know how well the system actually performs. If you only build evals without guardrails, you'll have great dashboards but your agent will occasionally do harmful things in production.

The practical recommendation: inline guardrails for safety-critical constraints (don't allow unauthorized actions), critique loops for quality (review before finalizing), evals for systematic improvement (measure, identify patterns, iterate).

## Examples

### Pattern in action
A financial analysis agent: (1) **Input guardrail** rejects requests that include personally identifiable financial data. (2) **Output guardrail** checks that generated reports include required disclaimers. (3) **Critique loop** — a second agent reviews the analysis for logical consistency before the user sees it. (4) **Eval** — weekly batch evaluation of output quality against analyst benchmarks to tune prompts.

### Anti-patterns / confusion traps
- Calling everything a "guardrail." Post-hoc evaluation isn't a guardrail; it's an eval. A review step isn't a guardrail; it's a critique loop. Precision in naming helps design the right mechanism.
- Over-relying on agent self-reflection. Agents can "reflect" without actually catching errors — the reflection may be as biased as the original output. External validation (different agent, human review, automated checks) is more reliable.
- Building guardrails that are too strict. If guardrails block legitimate use cases frequently, users will work around them — which is worse than having no guardrails at all.

## Evidence level

- **Established terms:** "guardrails" (OpenAI-led, broadly adopted), "eval" (universal), "validation" (general engineering)
- **Fragmented terms:** "hooks" (Anthropic-specific), "reflection" (academic term, informal implementation), "tracing" (implementation varies)
- **Inferred patterns:** The three-layer framework (inline guardrails → critique loops → evaluation) is an ACON synthesis, supported by the observation that each ecosystem implements some subset but no single ecosystem documents the full stack

## ACON recommendation

ACON uses **"guardrails"** for real-time input/output constraints, **"critique"** for in-workflow review steps, and **"eval"** for post-hoc performance measurement. These are three layers, not synonyms. When designing agent quality assurance, specify which layer each check belongs to — the implementation, timing, and reliability differ for each.

## Related entries

- Orchestrator vs Router vs Supervisor — orchestrators often manage guardrail and critique checkpoints
- Fresh-Eyes Review Loop (emerging) — a specific critique loop pattern
- File-Based Instruction Patterns — guardrail rules can be expressed as file-based instructions

## Changelog

- 2026-03-22: Initial entry
