# Fresh-Eyes Review Loop

## Questions for Joe

- This is one of ACON's strongest original contributions — the pattern is real and documented but no one has named it well. Is "Fresh-Eyes Loop" the right name, or do you prefer "Fresh-Context Review" or something else?
- Your EA system uses a version of this (the Three-Lens Review / Tech Trio). Should that be referenced as a practitioner example?
- The research found at least 2-3 independent implementations (practitioner repos that strip prior iterations, coding workflow reviewers that spawn fresh subagents). Is that enough evidence to eventually graduate this to the main field guide, or does it need more?

---

> ⚠️ EMERGING PATTERN — This describes a real practice that does not yet have a stable community name. The label "Fresh-Eyes Review Loop" is a working label proposed by ACON. Expect this entry to evolve as terminology stabilizes.

## The pattern

Spawning a new agent instance to review work produced by a previous agent — deliberately without giving the reviewer access to the working agent's reasoning, drafts, or intermediate steps. The reviewer sees only the output, evaluating it on its own merits.

## Why it matters

Agents that work on something for a long time accumulate context bias. They stop questioning assumptions they made early in the process. They develop blind spots around compromises they've already accepted. A fresh reviewer — one with no knowledge of the creative process — catches things the working agent can't see.

## Where it appears

- Practitioner implementations that explicitly strip prior iterations before review, creating "fresh eyes" on each pass
- Coding workflows where a separate subagent reviews code without access to the conversation that produced it
- Multi-agent systems where a "critic" agent operates independently of the "creator" agent
- The actor-critic pattern in RL, adapted to LLM workflows

## How it works

1. An agent produces work (draft, code, analysis, plan)
2. A new agent instance is spawned — ephemeral, with no inherited context from the working agent
3. The reviewer receives only the output and the evaluation criteria
4. The reviewer provides feedback
5. The original agent (or a new instance) incorporates feedback and revises
6. Optionally: the cycle repeats with a fresh reviewer each time

## Key design decisions

- **How many review cycles?** One pass catches obvious issues. Two catches deeper problems. Beyond three, diminishing returns unless the task is high-stakes.
- **Same persona type or different?** A reviewer with the same expertise catches technical errors. A reviewer with a different perspective (user, critic, domain expert) catches different classes of issues.
- **What does the reviewer see?** Just the output? The output plus the original requirements? The output plus the requirements plus evaluation rubric? More context makes review more relevant but risks introducing some of the same bias.

## Naming variants observed

- "Fresh eyes review" (most common informal usage)
- "Fresh context review" (emphasizes the context reset)
- "Independent review loop" (emphasizes independence from the working agent)
- "Clean-room review" (borrows from hardware engineering)
- No single term has emerged as standard.

## Evidence

- Practitioner repos documenting the pattern of stripping prior iterations for review
- "Fresh eyes" subagent reviewers in coding workflow implementations
- Actor-critic patterns adapted from RL to LLM-based review

## Status: Working label

"Fresh-Eyes Review Loop" is an ACON-proposed working label. The pattern is real and independently implemented by multiple practitioners, but no consensus name has emerged. ACON will track ecosystem adoption and graduate this term to the main field guide if a stable name converges.

## Related entries

- Ephemeral vs Persistent Agent Identity — fresh-eyes review depends on ephemeral spawning
- Guardrails and Validation — this is a specific implementation of a critique loop
- Orchestrator vs Router vs Supervisor — the orchestrator decides when to trigger a fresh-eyes review

## Changelog

- 2026-03-22: Initial entry as emerging pattern
