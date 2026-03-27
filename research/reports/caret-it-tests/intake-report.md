# Caret-it Test: Intake Skill

## Source

- original: local private skill `intake.md`
- rewrite: `intake-rewrite.md`
- token method: estimated with `ceiling(character_count / 4)` because no local tokenizer surface was exposed in this test

## Findings

- The biggest gain came from turning repeated "what to do" scaffolding into `^capture`, `^normalize`, `^rules`, `^update`, and `^ask` blocks.
- The preview-header templates stayed literal because they are examples, not live instruction.
- The main unresolved harness assumption is the handoff model to the paired review skill and the expected schema for `data/state.json`.

## Caret^ Rewrite

Full rewrite: `intake-rewrite.md`

## Compression Report

- original tokens: `842`
- rewritten tokens: `496`
- tokens saved: `346`
- percentage shorter: `41.1%`
- projected savings over 1,000 runs: `346000` tokens

## Example Compression

Before:

```text
Step 3: Update state and acknowledge

1. Update `data/state.json`: increment `intake_count`.
2. Acknowledge briefly: "Logged." or "Got it, captured."
3. On mobile / quick capture: If Joe says "log this" or similar from Dispatch, skip the "review now?" question.
4. Otherwise, ask once: "Want me to review this now, or hold it?"
```

After:

```text
^update
Increment `data/state.json` intake count.

^ack
Confirm in one line.

^mobile
If this is a quick mobile capture, stop after capture and confirmation.

^ask
Otherwise ask once: "Want me to review this now, or hold it?"
```

Why it compresses:

The closeout becomes a clean sequence of operating signals instead of a stack of narrated step labels.

## Log Note

No separate harness log action was exposed in this test. This report file is the completion record for the run.

This rewrite is 41.1% shorter. At roughly 346 tokens saved per run, using it 1,000 times saves about 346000 tokens.
