# Round 2: Coach Skill

## Source

- original: local private skill `coach.md`
- rewrite: `coach-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The CCF framework compressed cleanly because the source kept repeating the assessment mode and output framing.
- The output board stayed literal because the example is more useful as a concrete display than as live notation.
- The main harness assumption is that `data/state.json` reliably stores both `domains` and `coaching_log`.

## Adoption Call

`adopt`

The rewrite is materially shorter and still keeps the scoring model and output shape intact. This is a strong example of Caret^ helping a repeated assessment loop.

## Compression Report

- original tokens: `643`
- rewritten tokens: `381`
- tokens saved: `262`
- percentage shorter: `40.7%`
- projected savings over 1,000 runs: `262000`

## Example Compression

Before:

```text
For each domain, assess:

### Containment - "Is anything leaking?"
### Coherence - "Are your actions aligned with your goals?"
### Flow - "Is progress actually happening?"
```

After:

```text
^assess each domain across:
- containment
- coherence
- flow
```

Why it compresses:

The assessment frame becomes a reusable operating signal instead of three separately narrated setup blocks.

## Log Note

This report file is the completion record for the run.

This rewrite is 40.7% shorter. At roughly 262 tokens saved per run, using it 1,000 times saves about 262000 tokens.
