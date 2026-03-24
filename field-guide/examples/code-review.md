# Multi-Lens Code Review

## Scenario

A developer submits a pull request. The review should catch structural issues, performance problems, and usability concerns. No single reviewer reliably catches all three. Running three independent reviews with no shared context produces broader coverage than one reviewer trying to think about everything.

## Notation

```
^^^review.coordinator
  ^context.selected "pull-request.diff", "project-standards.md"

  ^^reviewer.structure
    ^context.selected "pull-request.diff"
    ^focus "architecture, coupling, abstraction boundaries, naming"
    ^output "review-structure.md"

  ^^reviewer.performance
    ^context.selected "pull-request.diff"
    ^focus "time complexity, memory allocation, query patterns, caching"
    ^output "review-performance.md"

  ^^reviewer.usability
    ^context.selected "pull-request.diff"
    ^focus "API surface, error messages, documentation, developer experience"
    ^output "review-usability.md"

  ^^synthesizer
    ^context.selected "review-structure.md", "review-performance.md", "review-usability.md"
    ^output "review-summary.md"

  ^gate.human
```

## Annotation

```
^^^review.coordinator           → anchored; knows the project standards and review history
  ^context.selected ...         → the diff and the standards the reviewers check against

  ^^reviewer.structure          → ephemeral; only sees the diff, no other reviews
    ^focus ...                  → directive: constrain attention to specific concerns
    ^output ...                 → structured findings

  ^^reviewer.performance        → ephemeral; same diff, different lens
    ^focus ...                  → performance-specific attention constraint
    ^output ...                 → structured findings

  ^^reviewer.usability          → ephemeral; same diff, third independent perspective
    ^focus ...                  → usability-specific attention constraint
    ^output ...                 → structured findings

  ^^synthesizer                 → ephemeral; reads all three reviews, writes summary
    ^context.selected ...       → receives only the review outputs, not the original diff
    ^output ...                 → consolidated review with conflicts identified

  ^gate.human                   → developer reads the synthesis and decides
```

## Runtime behavior

1. The coordinator loads the diff and project standards.
2. Three reviewers spawn in parallel. Each receives only the diff and a focus directive. No reviewer sees another reviewer's output. No reviewer sees the project standards — they review the code on its own merits.
3. Each reviewer produces independent findings and terminates.
4. A synthesizer spawns with all three review outputs. It identifies overlapping concerns, conflicting recommendations, and issues flagged by multiple lenses (high confidence) vs. single lenses (worth investigating).
5. The human gate presents the synthesis. The developer reads one document, not three.

## Variations

**Named perspectives vs. numbered:** This example uses named reviewers for clarity. The compact form is:

```
^^^review.coordinator
  ^^3
    ^context.selected "pull-request.diff"
  ^^synthesizer
```

The numbered form (`^^3`) is cleaner when the focus directives are omitted and the coordinator handles lens assignment.

**Without synthesizer:** Skip the `^^synthesizer` and present all three reviews directly at the human gate. Useful when the developer wants raw feedback, not a summary. More noise, more signal.

**With project context:** Give reviewers `^context.selected "pull-request.diff", "project-standards.md"`. They check against standards instead of reviewing in isolation. More targeted. Less likely to surface novel concerns the standards do not cover.
