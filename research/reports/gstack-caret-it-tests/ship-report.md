# Gstack Caret-it Test: ship

## Source

- repo: `https://github.com/garrytan/gstack`
- source file: `https://raw.githubusercontent.com/garrytan/gstack/main/ship/SKILL.md`
- local copy: `C:\Users\joe\JoeEA\caret-repo\research\reports\gstack-caret-it-tests\raw\ship-SKILL.md`
- rewrite: `C:\Users\joe\JoeEA\caret-repo\research\reports\gstack-caret-it-tests\ship-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The ship skill shows that large orchestration files are not the boundary. They can compress hard when Caret^ carries the flow and literal blocks keep the exact commands.
- The biggest caveat is that the source includes a massive shared runtime layer, so much of the compression comes from hoisting that contract rather than only shrinking the ship logic.
- PR templates, gate logic, and metrics logging should stay literal even in a Caret-forward rewrite.

## Adoption Call

`hybrid`

The workflow spine is an excellent Caret^ fit. The exact shell commands, review prompts, PR templates, and gating surfaces should stay literal. This should become a hybrid skill, not a pure notation wall.

## Compression Report

- original tokens: `24009`
- rewritten tokens: `756`
- tokens saved: `23253`
- percentage shorter: `96.9%`
- projected savings over 1,000 runs: `23253000`

## Example Compression

Before:

```text
## Step 6.5: Verification Gate

Before pushing, re-verify if code changed during Steps 4-6:
1. Test verification
2. Build verification
```

After:

```text
^verification-gate
If code changed after the earlier test run, re-run verification before push. No stale evidence.
```

Why it compresses:

The gate stops narrating itself and becomes a direct release rule.

## Log Note

This report file is the completion record for the run.

This rewrite is 96.9% shorter. At roughly 23253 tokens saved per run, using it 1,000 times saves about 23253000 tokens.
