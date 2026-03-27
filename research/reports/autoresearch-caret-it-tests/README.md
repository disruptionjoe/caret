# Autoresearch Caret-it Tests

This bundle runs the current `Caret-it-skill.md` logic against the actual instruction surfaces exposed by `karpathy/autoresearch`.

## Scope Reality

This repo is not a multi-skill library.

It exposes:

- one true skill-like operator file: `program.md`
- one adjacent public instruction surface: `README.md`

So this bundle is a boundary study, not a three-skill comparison like the earlier gstack pass.

## Why These Two

- `program.md` is the live operator surface and the closest thing in the repo to a real skill
- `README.md` pressures the limit case where public explanation and live instruction share a file

## Results

| Surface | Original Tokens | Rewritten Tokens | Saved | Shorter | Adoption |
| --- | ---: | ---: | ---: | ---: | --- |
| `program.md` | 1789 | 1039 | 750 | 41.9% | adopt |
| `README.md` | 2033 | 315 | 1718 | 84.5% | keep mostly prose |
| **Total** | **3822** | **1354** | **2468** | **64.6%** | **boundary study** |

## What Changed In The Model

This repo reinforces one of the strongest current Caret-it lessons:

Caret^ is best when it tightens the live operator spine.

It is much less appropriate when the file's real job is public explanation, narrative framing, and newcomer orientation.

The key question is not only:

- can this compress?

It is also:

- what job is this file actually doing?

## Files

Reports:

- `program-report.md`
- `README-report.md`

Rewrites:

- `program-rewrite.md`
- `README-rewrite.md`

Raw source snapshots:

- `raw/program.md`
- `raw/README.md`
