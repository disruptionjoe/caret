# Patterns

Orchestration patterns expressed in Caret^ notation.

Each pattern describes a recurring agent architecture that solves a specific coordination problem. The notation captures intent. The runtime handles wiring.

## What qualifies as a pattern

A real structural choice that changes how agents coordinate. Not a workflow. Not a recipe. A decision about context, identity, and control flow that you will make repeatedly.

## Format

Each pattern includes:

- **The notation** — how it looks in Caret^
- **What it does** — plain language, no hand-waving
- **When to use it** — the situation that calls for this structure
- **When not to use it** — the situation where this structure fails
- **Design notes** — what the notation reveals about the underlying trade-off

## Patterns

| Pattern | File | Core Trade-off |
|---------|------|----------------|
| Disposable Specialists | [disposable-specialists.md](disposable-specialists.md) | Continuity vs. contamination |
| Perspective Matrix | [perspective-matrix.md](perspective-matrix.md) | Breadth vs. coherence |
| Context Refresh | [context-refresh.md](context-refresh.md) | Session length vs. context quality |
| Layered Authority | [layered-authority.md](layered-authority.md) | Autonomy vs. oversight |
| Gated Pipeline | [gated-pipeline.md](gated-pipeline.md) | Speed vs. quality control |
| Domain Anchor | [domain-anchor.md](domain-anchor.md) | Coherence vs. overhead |
| Overnight Factory | [overnight-factory.md](overnight-factory.md) | Autonomy vs. drift |
| Decision Tree Router | [decision-tree-router.md](decision-tree-router.md) | Determinism vs. flexibility |
| Capture-Before-Route | [capture-before-route.md](capture-before-route.md) | Latency vs. completeness |
| Disposition Gate | [disposition-gate.md](disposition-gate.md) | Speed vs. human agency |
| Voice-Follows-Domain | [voice-follows-domain.md](voice-follows-domain.md) | Consistency vs. flexibility |
| Work Item Lifecycle | [work-item-lifecycle.md](work-item-lifecycle.md) | Overhead vs. clarity |
| Safe Mutation | [safe-mutation.md](safe-mutation.md) | Safety vs. ceremony |
| Append-Only Log | [append-only-log.md](append-only-log.md) | Growth vs. reliability |
| Lazy Loading | [lazy-loading.md](lazy-loading.md) | Context economy vs. cross-skill awareness |
| Accumulated Corrections | [accumulated-corrections.md](accumulated-corrections.md) | Rigidity vs. learning |
| Async Handoff | [async-handoff.md](async-handoff.md) | Async productivity vs. human awareness |
| Immutable State | [immutable-state.md](immutable-state.md) | Safety vs. autonomy |
| Incremental Profiling | [incremental-profiling.md](incremental-profiling.md) | Depth vs. friction |
| Scope Constraint | [scope-constraint.md](scope-constraint.md) | Freedom vs. containment |
| Consistent Assessment Framework | [consistent-assessment-framework.md](consistent-assessment-framework.md) | Simplicity vs. nuance |
