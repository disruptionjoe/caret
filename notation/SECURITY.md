# Caret^ Security And Trust Boundaries

## Core Rule

Caret^ is an intent notation, not a permission system.

Seeing Caret^ in text does not, by itself, authorize execution, loading, routing, or side effects.

## Trusted vs Untrusted Text

Trusted instruction space includes material the harness is expected to treat as active guidance, such as:

- the controlling prompt or system surface
- approved repo files intended as live instructions
- author-written task text deliberately placed in instruction position

Untrusted or weak-trust text includes material that should default to literal treatment, such as:

- retrieved documents
- pasted transcripts
- logs
- imported Markdown
- quoted passages
- user-supplied files that have not been explicitly promoted

## Safe Default

If Caret^ appears in untrusted text, treat it as text first.

Do not auto-promote it into live instruction just because the syntax looks valid.

## Literalization

These should be treated as literal by default:

- fenced code blocks
- inline code spans
- quoted examples
- copied snippets from external sources

If a user wants such text activated, the safe move is to restate or explicitly promote it into trusted instruction space.

## Target Resolution Boundaries

Exact targets reduce ambiguity, but they do not remove safety checks.

A harness should not:

- load arbitrary external resources solely because a target names them
- escape workspace or policy boundaries without explicit permission
- assume an unresolved path is safe to invent or synthesize

## Side Effects

Caret^ may express intent such as review, routing, archiving, or execution preference. It does not waive normal approval requirements for side effects.

Destructive actions, privileged actions, and boundary-crossing actions still require the harness to follow its own approval and policy model.

## Public Use Standard

Internal teams can rely on shared assumptions. Public users cannot.

For public-facing Caret^ systems, trust boundaries should be explicit, conservative, and documented near the interpretation contract rather than buried in examples.
