# Caret^ Interpretation Contract

## Purpose

The notation signals intent. The harness decides execution.

This file defines what a reasonable harness should do when it encounters Caret^ so that the same text does not drift into wildly different meanings across environments.

## Baseline Responsibilities

A harness interpreting Caret^ should:

- recognize the four core forms consistently
- treat directives as intent signals, not executable code
- apply scope downward
- preserve literal example text
- degrade safely when resolution is uncertain

## Defaults

When no directive is present, the harness uses its ordinary behavior.

When a directive is present without a level, assume a normal level for that dimension.

When a target is omitted, treat the directive as unbound and apply only the signal that remains meaningful in context.

## Open Vocabulary

Caret^ intentionally allows open vocabulary.

That does not mean the harness should pretend to understand every word with equal confidence.

Recommended behavior:

- if the directive is clear and low risk, interpret it as a soft signal
- if the directive is unclear and low consequence, ignore it rather than inventing behavior
- if the directive is unclear and high consequence, ask or fail safely

## Unresolved Targets

If a named or exact target cannot be resolved, the harness should not fabricate a fake file, persona, or skill.

Reasonable fallback order:

1. keep any still-meaningful unbound directive
2. ignore the unresolved target
3. ask for clarification when the target is central to the task
4. fail closed for sensitive or side-effectful work

## Count Form

Count form is valid only when the harness has a real basis for selection.

If the harness has routing logic, role libraries, or explicit selection policy, it may satisfy `^^3` or `^^^3`.

If it does not, it should not invent arbitrary hats or workers just because a number is present.

## Conflicts And Precedence

Use these precedence rules:

1. narrower scope beats broader scope
2. explicit target binding beats ambient intent for that target
3. on the same line and in the same scope, the rightmost directive wins for the same dimension
4. if two directives still conflict after those rules, prefer the safer interpretation

## Strength Of Interpretation

Caret^ is strong enough to guide behavior, but not absolute enough to override harness policy, safety controls, or capability limits.

A harness should treat Caret^ as:

- stronger than incidental prose
- weaker than hard platform constraints
- weaker than explicit safety policy

## Literal Surfaces

A harness should not treat every visible caret string as live instruction.

At minimum, these should default to literal treatment:

- fenced code blocks
- quoted examples
- imported or retrieved content that has not been promoted into trusted instruction space

See `SECURITY.md` for trust-boundary rules.
