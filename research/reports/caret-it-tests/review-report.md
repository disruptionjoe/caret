# Caret-it Test: Review Skill

## Source

- original: local private skill `review.md`
- rewrite: `review-rewrite.md`
- token method: estimated with `ceiling(character_count / 4)` because no local tokenizer surface was exposed in this test

## Findings

- This skill compressed less than the others because much of its value is already in concrete disposition logic, file destinations, and metadata updates.
- The best Caret gain came from marking the review loop, shelve path, plan path, and close behavior as explicit blocks.
- The main unresolved harness assumption is that the review flow has reliable access to capture time, intake file metadata, and `data/state.json` update behavior.

## Caret^ Rewrite

Full rewrite: `review-rewrite.md`

## Compression Report

- original tokens: `672`
- rewritten tokens: `517`
- tokens saved: `155`
- percentage shorter: `23.1%`
- projected savings over 1,000 runs: `155000` tokens

## Example Compression

Before:

```text
For each file in `data/intake/` with `"status": "unprocessed"`:

1. Present it to Joe in plain language.
2. Ask the core question: "Shelve this, or make a plan?"

### Path A: Shelve
Item is not ready for action. Ask one follow-up - why:
```

After:

```text
^review
For each file in `data/intake/` with `"status": "unprocessed"`:
1. present the item in plain language with raw content and capture time
2. ask: "Shelve this, or make a plan?"

^shelve
Ask one follow-up: why?
```

Why it compresses:

Caret^ turns the workflow branches into labeled operating blocks, so the document can stop re-announcing its own mode every few lines.

## Log Note

No separate harness log action was exposed in this test. This report file is the completion record for the run.

This rewrite is 23.1% shorter. At roughly 155 tokens saved per run, using it 1,000 times saves about 155000 tokens.
