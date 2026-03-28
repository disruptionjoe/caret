# Gstack Caret-it Test: ship

## Source

- repo: `https://github.com/garrytan/gstack`
- source file: `https://raw.githubusercontent.com/garrytan/gstack/main/ship/SKILL.md`
- local copy: `raw/ship-SKILL.md`
- rewrite: `ship-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The ship skill shows that large orchestration files are not the boundary. They can compress hard when Caret^ carries the flow and literal blocks keep the exact commands.
- The biggest caveat is that the source includes a massive shared runtime layer, so much of the compression comes from hoisting that contract rather than only shrinking the ship logic.
- Under the new parity gate, this specific rewrite loses too much executable contract. Release commands, PR templates, platform handling, and metrics behavior are too exact to survive as references alone.

## Adoption Call

`keep mostly prose`

There is real compression signal here, but the current rewrite is not safe as a replacement. Until the shared contract is extracted for real and the literal release surfaces remain embedded, this is better treated as design evidence than as an adoptable rewrite.

## Behavioral Parity

- parity status: `fail`
- parity basis: `inferred via static contract comparison`
- comparison scope:
  - shared gstack runtime contract
  - platform detection
  - verification gates
  - versioning and changelog behavior
  - PR and MR generation
  - docs sync and metrics logging
  - completion behavior
- preserved:
  - the high-level release sequence
  - the existence of review and verification gates
  - the need to keep literal command and template surfaces
- lost or unresolved:
  - exact shell command contract
  - exact PR and MR body templates
  - platform-specific branching and detection behavior
  - docs sync workflow details
  - metrics logging commands
  - completion protocol details

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
