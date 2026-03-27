# Gstack Caret-it Tests

This bundle runs the current `Caret-it-skill.md` logic against three gstack skills chosen for shape diversity:

- `design-review`
- `ship`
- `plan-eng-review`

## Why These Three

- `design-review` stresses browser-driven audit loops, scoring systems, and fix verification
- `ship` stresses long orchestration, release gates, templates, and exact command surfaces
- `plan-eng-review` stresses multi-lens reasoning, interactive review flow, and persistent reporting

## Results

| Skill | Original Tokens | Rewritten Tokens | Saved | Shorter | Adoption |
| --- | ---: | ---: | ---: | ---: | --- |
| `design-review` | 14710 | 773 | 13937 | 94.7% | hybrid |
| `ship` | 24009 | 756 | 23253 | 96.9% | hybrid |
| `plan-eng-review` | 15663 | 754 | 14909 | 95.2% | hybrid |
| **Total** | **54382** | **2283** | **52099** | **95.8%** | **shared-contract pattern** |

## Cross-Repo Signal

The external repo changed the picture in one important way:

The dominant compression opportunity is not only "turn prose into Caret^."

It is also:

- separate shared runtime contract from skill-specific workflow
- use Caret^ on the workflow spine
- keep commands, templates, tables, and schemas literal

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
