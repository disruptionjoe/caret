# `program.md` Caret-it Report

## Findings

- The file is a strong Caret^ target because it is a live operator program with repeated setup, boundary, loop, and logging language.
- The main compression win comes from collapsing repeated operating stance into scoped directives like `^setup`, `^log`, and `^loop`.
- Commands, output samples, and TSV schema should stay literal. Converting those into notation would make the file worse.
- Harness assumptions remain local: the source expects git, `uv`, a GPU-backed training environment, and a human who can stop the loop manually.
- No canon normalization was required. The file does not contain stale Caret semantics.
- Shared-contract extraction was not a major factor. Most of the win is local workflow compression.

## Adoption Call

`adopt`

This file is doing exactly the kind of repetitive operational work Caret^ is built for. The hybrid shape is still important, but the live spine wants notation and gets clearer with it.

## Caret^ Rewrite

See `program-rewrite.md`.

## Compression Report

- Original token count: `1789`
- Rewritten token count: `983`
- Tokens saved: `806`
- Percentage shorter: `45.1%`
- Projected savings over 1,000 runs: `806000`

Token counts use the fallback estimator `ceiling(character_count / 4)`.

## Example Compression

```text
Before:
What you CAN do:
- Modify `train.py` - this is the only file you edit.

What you CANNOT do:
- Modify `prepare.py`.
- Install new packages or add dependencies.
- Modify the evaluation harness.

After:
^grip9
- Edit only `train.py`.
- Do not modify `prepare.py`.
- Do not add packages or dependencies.
- Do not modify the evaluation harness.

Why it compresses:
The rewrite removes heading overhead and collapses the permission boundary into one scoped rule block.
```

## Log Note

Completed as a research report bundle only.

No external side effects were triggered in the source repo.
