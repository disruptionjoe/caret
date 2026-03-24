# Notation Design Principles

Why the notation is shaped the way it is.

---

## 1. Structure over prose

If something can be a directive, it should not be a paragraph. Prose is for domain expertise. Orchestration intent belongs in notation.

## 2. The caret count is the lifecycle

`^` = directive. `^^` = ephemeral. `^^^` = anchored. `^^^^` = clear. The depth of the caret tells you the agent's relationship to context. No other information needed.

## 3. Declarative, not procedural

The notation says *what*, not *how*. `^^3` says "three ephemeral agents." It does not say how to spawn them, allocate resources, or manage their lifecycle. That is the adapter's problem.

## 4. Context is first-class

Every agent's context posture is an explicit declaration, not a runtime default. `^context.none`, `^context.selected`, `^^^` vs `^^` — the notation forces you to decide about context instead of leaving it to chance.

## 5. Portable across runtimes

The notation sits inside `.md` files. Adapters translate to whatever runtime your agents use. If the notation requires a specific runtime to work, the notation is wrong.

## 6. Short over clever

`^grip7` over `^prescriptiveness.high`. Every character costs a token. Every extra word is a parsing burden. Abbreviation is acceptable when the metaphor holds.

## 7. Governance is scannable

Permission rules are atomic directives, not buried prose. You can grep a Caret file for all governance declarations in one pass. A machine can verify them. A human can audit them.

## 8. Patterns are portable

The context refresh pattern (`^^^agent / ^^^^ / ^^^agent`) looks the same whether it's a writer, coder, or researcher. Once you've seen the pattern, you recognize it anywhere.

## 9. No hyphens, no parentheses

Dots are the only separator. Compound words collapse. Speed of typing matters — every keystroke counts in a notation you write daily.

## 10. Parameters are hints, not contracts

If a runtime adapter doesn't recognize a parameter, it ignores it. The notation does not break. This makes adoption incremental — you can start using Caret before your tools fully support it.
