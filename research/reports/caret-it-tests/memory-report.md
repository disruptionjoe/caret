# Caret-it Test: Memory Skill

## Source

- original: `C:\Users\joe\JoeEA\ea-os\skills\memory.md`
- rewrite: `C:\Users\joe\JoeEA\caret-repo\research\reports\caret-it-tests\memory-rewrite.md`
- token method: estimated with `ceiling(character_count / 4)` because no local tokenizer surface was exposed in this test

## Findings

- The strongest gain came from collapsing repeated trigger prose into `^active`, `^route`, `^rules`, and `^track` blocks.
- The daily drip section stayed partly prose because the skip conditions and note-tracking rule still need plain-language precision.
- The main unresolved harness assumption is that the priority flow already loads both profile files and that today's note can reliably carry a `drip_question` field.

## Caret^ Rewrite

Full rewrite: `C:\Users\joe\JoeEA\caret-repo\research\reports\caret-it-tests\memory-rewrite.md`

## Compression Report

- original tokens: `1029`
- rewritten tokens: `581`
- tokens saved: `448`
- percentage shorter: `43.5%`
- projected savings over 1,000 runs: `448000` tokens

## Example Compression

Before:

```text
When you detect one of these, update the appropriate file:

- Static fact change -> Edit `data/profile/joe.md` directly.
- New learning/pattern/decision -> Append to the relevant section in
  `data/profile/memory.md` with today's date.

Rules for updating:
- Don't ask permission to update memory -> just do it quietly.
- Don't announce every update.
```

After:

```text
^route
- static fact change -> edit `data/profile/joe.md`
- new learning, pattern, or decision -> append a dated line to `data/profile/memory.md`

^rules
- update quietly
- do not ask permission to store memory
```

Why it compresses:

The route logic and update constraints stop repeating their own setup. Caret^ carries the signal, so the prose only has to hold the content.

## Log Note

No separate harness log action was exposed in this test. This report file is the completion record for the run.

This rewrite is 43.5% shorter. At roughly 448 tokens saved per run, using it 1,000 times saves about 448000 tokens.
