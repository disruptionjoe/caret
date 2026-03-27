# Round 3: Pattern Drafting

## Source

- original: `C:\Users\joe\JoeEA\ea-os\skills\pattern-draft.md`
- rewrite: `C:\Users\joe\JoeEA\caret-repo\research\reports\caret-it-optimization\round-3\pattern-draft-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The file compressed aggressively because the section rules and quality gate are highly structured.
- The real boundary is again canonical mismatch: the original pattern guidance still encodes obsolete worker semantics and dot-based notation.
- This is another case where semantic repair is part of the job.

## Adoption Call

`hybrid`

The rewrite is strong, but the source is not merely verbose. It is partially wrong under the current canon. That makes this a normalize-first case before it becomes a clean adoption case.

## Compression Report

- original tokens: `1104`
- rewritten tokens: `534`
- tokens saved: `570`
- percentage shorter: `51.6%`
- projected savings over 1,000 runs: `570000`

## Example Compression

Before:

```text
- `^^` - ephemeral agent
- `^^^` - anchored agent
- Named agents use dot-syntax
```

After:

```text
- `^^` -> hat, not worker
- `^^^` -> worker boundary
- `^^^^` -> fresh-eyes boundary
```

Why it compresses:

Some of the gain comes from notation. Some comes from deleting obsolete semantics and replacing them with current canon.

## Log Note

This report file is the completion record for the run.

This rewrite is 51.6% shorter. At roughly 570 tokens saved per run, using it 1,000 times saves about 570000 tokens.
