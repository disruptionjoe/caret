# Round 2: Improve Skill

## Source

- original: local private skill `improve.md`
- rewrite: `improve-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The three-lens structure maps cleanly onto `^^` hats because the source wants perspective shifts, not necessarily separate workers.
- Synthesis, re-review, routing, and logging all benefited from explicit operating blocks.
- The main harness assumption is that the same worker can apply the three lenses cleanly without losing the "independent diagnosis" intent.

## Adoption Call

`adopt`

This is a strong Caret^ fit. The file already thinks in lenses, review passes, and route decisions. The notation makes that structure easier to see without losing the concrete implementation rules.

## Compression Report

- original tokens: `988`
- rewritten tokens: `612`
- tokens saved: `376`
- percentage shorter: `38.1%`
- projected savings over 1,000 runs: `376000`

## Example Compression

Before:

```text
### Lens 1: Software Engineer
- Asks: Is the data model wrong? Is there a bug in the logic?
- Proposes: The smallest code or schema change that fixes the root cause.
- Avoids: Rewriting systems.
```

After:

```text
^^software-engineer
  Diagnose data-model issues, logic bugs, broken scripts, and misconfigured skill wiring.
  Propose the smallest code or schema change that fixes the root cause.
  Avoid rewrites. Prefer patches and guards.
```

Why it compresses:

The lens becomes a real structural boundary instead of a repeated heading formula.

## Log Note

This report file is the completion record for the run.

This rewrite is 38.1% shorter. At roughly 376 tokens saved per run, using it 1,000 times saves about 376000 tokens.
