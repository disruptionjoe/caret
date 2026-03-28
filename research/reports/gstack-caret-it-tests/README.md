# Gstack Caret-it Tests

This bundle has been rerun under the new behavioral parity gate in `Caret-it-skill.md`.

The same three gstack skills were re-evaluated for both compression and replacement safety:

- `design-review`
- `ship`
- `plan-eng-review`

## Why These Three

- `design-review` stresses browser-driven audit loops, scoring systems, and fix verification
- `ship` stresses long orchestration, release gates, templates, and exact command surfaces
- `plan-eng-review` stresses multi-lens reasoning, interactive review flow, and persistent reporting

## Results

| Skill | Original Tokens | Rewritten Tokens | Saved | Shorter | Parity | Adoption | Replacement-ready |
| --- | ---: | ---: | ---: | ---: | --- | --- | --- |
| `design-review` | 14710 | 773 | 13937 | 94.7% | `partial` | `hybrid` | `no` |
| `ship` | 24009 | 756 | 23253 | 96.9% | `fail` | `keep mostly prose` | `no` |
| `plan-eng-review` | 15663 | 754 | 14909 | 95.2% | `partial` | `hybrid` | `no` |
| **Total** | **54382** | **2283** | **52099** | **95.8%** | **0 / 3 parity-pass** | **compression-only evidence** | **0 / 3** |

## Parity Rerun Rule

This rerun used **static contract comparison**, not live execution, because no local gstack harness was available here.

So the bundle now answers two different questions:

- how much token drag is present
- whether the proposed rewrite is safe to replace the original with

The answer is more conservative than the first pass.

## Cross-Repo Signal

The external repo changed the picture in one important way:

The dominant compression opportunity is not only "turn prose into Caret^."

It is also:

- separate shared runtime contract from skill-specific workflow
- use Caret^ on the workflow spine
- keep commands, templates, tables, and schemas literal

The stricter rerun adds the missing caution:

- a rewrite that only says "inherit the shared contract" is not behaviorally equivalent unless that contract exists as a real reusable artifact
- a rewrite that names literal surfaces without actually carrying them forward is not replacement-safe

So the bundle now shows strong compression potential, but not drop-in equivalence.

## Files

Reports:

- `design-review-report.md`
- `ship-report.md`
- `plan-eng-review-report.md`

Rewrites:

- `design-review-rewrite.md`
- `ship-rewrite.md`
- `plan-eng-review-rewrite.md`

Raw source snapshots:

- `raw/design-review-SKILL.md`
- `raw/ship-SKILL.md`
- `raw/plan-eng-review-SKILL.md`

Parity summary:

- `parity-matrix.md`
