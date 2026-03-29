# Patterns

Patterns are reusable workflow shapes. Structural decisions that change how agents coordinate.

Not tutorials. Not recipes. Not code conventions. Patterns name real choices you face when building agent systems—and help you recognize when you're making them.

## What qualifies

A pattern is in this catalog if it:

- Names a structural choice, not a workflow or preference
- Changes how agents coordinate, not just what they do
- Works beyond one private system
- Has notation that uses Caret^ canon
- Surfaces a trade-off you'll actually face
- Helps someone recognize a decision they're already making
- Can't be expressed better as prose

## What doesn't

- Workflows or sequences of steps
- Design preferences or coding conventions
- System-specific logic
- Custom notation outside the cheatsheet
- Evaluation frameworks or assessment methods

## Categories

### Delegation and Coordination

Structure who does what and who decides.

- **[disposable-specialists](disposable-specialists.md)**: Continuity vs. contamination
- **[perspective-matrix](perspective-matrix.md)**: Breadth vs. coherence
- **[layered-authority](layered-authority.md)**: Autonomy vs. oversight

### Routing and Intake

Shape how work enters the system and where it goes.

- **[decision-tree-router](decision-tree-router.md)**: Determinism vs. flexibility
- **[capture-before-route](capture-before-route.md)**: Latency vs. completeness
- **[disposition-gate](disposition-gate.md)**: Speed vs. human agency
- **[lazy-loading](lazy-loading.md)**: Context economy vs. cross-skill awareness

### Context and Boundaries

Manage what agents know and what they're allowed to do.

- **[context-refresh](context-refresh.md)**: Session length vs. context quality
- **[scope-constraint](scope-constraint.md)**: Freedom vs. containment
- **[harness-layering](harness-layering.md)**: Portability vs. simplicity
- **[publication-gate](publication-gate.md)**: Safety vs. velocity

### Temporal Workflows

Orchestrate work across time.

- **[gated-pipeline](gated-pipeline.md)**: Speed vs. quality control
- **[async-handoff](async-handoff.md)**: Async productivity vs. human awareness
- **[overnight-factory](overnight-factory.md)**: Autonomy vs. drift

### State and Memory

Manage how agents remember, learn, and protect what matters.

- **[domain-anchor](domain-anchor.md)**: Coherence vs. overhead
- **[append-only-log](append-only-log.md)**: Growth vs. reliability
- **[accumulated-corrections](accumulated-corrections.md)**: Rigidity vs. learning
- **[immutable-state](immutable-state.md)**: Stability vs. speed
- **[work-item-lifecycle](work-item-lifecycle.md)**: Discipline vs. simplicity
- **[incremental-profiling](incremental-profiling.md)**: Accuracy vs. immediacy
- **[voice-follows-domain](voice-follows-domain.md)**: Consistency vs. flexibility

### Governance and Learning

Control how agents learn, review, and maintain system integrity.

- **[hat-before-worker](hat-before-worker.md)**: Efficiency vs. independence
- **[anchored-memory-stack](anchored-memory-stack.md)**: Recall vs. cost
- **[triggered-review](triggered-review.md)**: Safety vs. velocity
- **[promotion-gate](promotion-gate.md)**: Adaptability vs. stability
- **[source-of-truth-hierarchy](source-of-truth-hierarchy.md)**: Clarity vs. flexibility
- **[live-registry](live-registry.md)**: Accuracy vs. maintenance cost

### Safety and Mutation

Control how agents change state.

- **[safe-mutation](safe-mutation.md)**: Safety vs. ceremony

## Pattern structure

Each pattern has five sections:

1. **Notation** — How to draw it in Caret^ canon
2. **What it does** — The structural shape and why it matters
3. **When to use it** — Conditions where this choice pays off
4. **When not to use it** — Where this pattern creates drag
5. **Design notes** — Tensions, variants, and gotchas

## About this catalog

Caret^ exists because agent workflows got bloated. We build with small marks. Hard edges. Clear intent.

Patterns support a portable artifact: the cheatsheet. Everything else—including these files—makes that notation concrete and useful.
