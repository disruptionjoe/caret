# Content Production Pipeline

## Scenario

A solo operator publishes articles under a specific brand voice. The writing process requires research, drafting, voice matching, and review. Each step benefits from fresh context. The operator reviews the final output, not every intermediate step.

## Notation

```
^^^editorial.director
  ^voice.load "brand-voice-guide.md"

  ^^researcher
    ^context.minimal
    ^output "research-brief.md"

  ^gate.complete

  ^^writer
    ^context.selected "research-brief.md", "brand-voice-guide.md"
    ^output "draft.md"

  ^gate.quality
    ^check voice.match "brand-voice-guide.md"
    ^check length.range 1000, 1400

  ^^reviewer
    ^context.selected "draft.md"
    ^output "review-notes.md"

  ^gate.human
```

## Annotation

```
^^^editorial.director           → anchored coordinator; holds brand knowledge and editorial standards
  ^voice.load "brand-voice..."  → directive: load voice definition into coordinator's context

  ^^researcher                  → ephemeral; knows nothing about the brand or prior articles
    ^context.minimal            → directive: only task instructions, no prior state
    ^output "research-brief.md" → directive: structured output file

  ^gate.complete                → checkpoint: did the researcher produce a usable brief?

  ^^writer                      → ephemeral; fresh perspective, no researcher bias
    ^context.selected ...       → directive: receives only the brief and voice guide
    ^output "draft.md"          → directive: structured output file

  ^gate.quality                 → checkpoint: automated quality checks
    ^check voice.match ...      → does the draft match the loaded voice definition?
    ^check length.range ...     → is the word count within bounds?

  ^^reviewer                    → ephemeral; has never seen the brief or the writing process
    ^context.selected "draft.md" → only the draft; judges the artifact, not the process
    ^output "review-notes.md"   → directive: structured feedback

  ^gate.human                   → final gate: the operator reviews before publication
```

## Runtime behavior

1. The editorial director loads the voice guide into its working context.
2. A fresh researcher is spawned with minimal context. It produces a research brief and terminates.
3. The `complete` gate checks the brief exists and is non-empty. If it fails, the director can retry or escalate.
4. A fresh writer is spawned with the brief and voice guide. It produces a draft and terminates. The writer never sees the researcher's reasoning — only its output.
5. The `quality` gate runs two automated checks. Voice matching compares the draft against the guide's calibration phrases and rules. Length range validates word count.
6. A fresh reviewer is spawned with only the draft. No brief, no voice guide, no process context. It evaluates the draft on its own terms and produces review notes.
7. The `human` gate pauses the pipeline. The operator reads the draft and review notes. The pipeline does not complete until the operator approves.

## Variations

**Without quality gate:** Remove `^gate.quality` and its checks. The reviewer catches quality issues instead. Faster, but the reviewer's context is limited to the draft — it cannot check voice match without the guide.

**With revision loop:** After the reviewer's notes, spawn a new `^^editor` with the draft and review notes. The editor revises. Add another `^gate.quality` before the human gate. More thorough, more tokens.

**Single-agent shortcut:** For low-stakes content, collapse to `^^^writer` with full context. No pipeline, no gates. Faster. Less reliable.
