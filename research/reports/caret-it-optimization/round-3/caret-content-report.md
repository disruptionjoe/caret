# Round 3: Caret Content Authoring

## Source

- original: local private skill `caret-content.md`
- rewrite: `caret-content-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The file compressed strongly, but the important finding is not the shrinkage. It is the canonical mismatch in the source.
- The original still teaches obsolete notation semantics and dot-based forms that conflict with the current Caret^ canon.
- This means the rewrite is partly a conversion and partly a normalization pass.

## Adoption Call

`hybrid`

The rewritten file is better, but this case should not be treated as a pure "Caret-it" success. It first requires semantic normalization against current canon, then notation compression. That makes it a boundary case, not a straight adoption case.

## Compression Report

- original tokens: `693`
- rewritten tokens: `353`
- tokens saved: `340`
- percentage shorter: `49.1%`
- projected savings over 1,000 runs: `340000`

## Example Compression

Before:

```text
- Control knobs are 0-9 ordinals.
- Dots separate parameters.
- Domain prose stays in prose.
```

After:

```text
^rules
- notation examples must match the current canon
- use `0-9` scalar levels
- keep domain prose in prose
```

Why it compresses:

The rewrite drops stale syntax rules and turns the remaining operating constraints into one real rule block.

## Log Note

This report file is the completion record for the run.

This rewrite is 49.1% shorter. At roughly 340 tokens saved per run, using it 1,000 times saves about 340000 tokens.
