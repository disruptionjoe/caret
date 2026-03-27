# Round 2 Summary

Round 2 tested diagnostic and decision-heavy skills:

- `coach.md`
- `improve.md`
- `priority.md`

## Results

| Skill | Original Tokens | Rewritten Tokens | Saved | Shorter | Adoption |
| --- | ---: | ---: | ---: | ---: | --- |
| `coach.md` | 643 | 381 | 262 | 40.7% | adopt |
| `improve.md` | 988 | 612 | 376 | 38.1% | adopt |
| `priority.md` | 1539 | 774 | 765 | 49.7% | adopt |
| **Total** | **3170** | **1767** | **1403** | **44.3%** | **strong round** |

## Round Signal

This round broke the assumption that only small operational skills compress well.

Even a dense start-of-day orchestration file compressed hard once the rewrite:

- kept literal schemas literal
- used notation for flow and gating
- stopped re-narrating every step header

## Patch Implication

Caret-it should explicitly tell the user:

- complex flows are still strong candidates
- notation should carry the sequence
- schemas, examples, and payload formats should usually stay fenced or plain
