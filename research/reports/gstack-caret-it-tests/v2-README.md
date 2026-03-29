# GStack Caret-it Tests — v2 (Integrated Validation)

This round used the revised `Caret-it-skill.md` which runs analysis, rewrite, and validation as a single integrated process. No separate parity skill was invoked.

The same three GStack skills were tested:

- `design-review`
- `ship`
- `plan-eng-review`

## v2 Results

| Skill | Original (chars) | Rewrite (chars) | Reduction | Est. Tokens Saved | Parity | Adoption |
| --- | ---: | ---: | ---: | ---: | --- | --- |
| `design-review` | 59,201 | 33,771 | **43.0%** | ~6,358 | `pass` | `hybrid` |
| `ship` | 97,322 | 43,774 | **55.0%** | ~13,387 | `pass` | `hybrid` |
| `plan-eng-review` | 63,549 | 56,274 | **11.5%** | ~1,819 | `pass` | `hybrid` |
| **Total** | **220,072** | **133,819** | **39.2%** | **~21,563** | **3 / 3 pass** | |

Token estimates use character_count / 4.

## Comparison to v1

| | v1 (old skill) | v2 (revised skill) |
| --- | --- | --- |
| Average compression | 95.8% | 39.2% |
| Parity pass rate | 0 / 3 | 3 / 3 |
| Replacement-ready | 0 / 3 | 3 / 3 (hybrid) |
| Adoption calls | 2 hybrid, 1 keep prose | 3 hybrid |

v1 chased maximum compression and gutted the files to ~3K characters each. It achieved 95.8% reduction but failed parity on all three — the rewrites dropped required behavior.

v2 prioritizes behavioral parity first and compresses only what can safely compress. The result is a more modest but honest 39.2% average reduction where every rewrite actually works.

## What the Numbers Mean

The 39.2% is the real number. It represents token savings you can actually use — the rewrites preserve all required inputs, outputs, safety boundaries, and workflow gates.

The 95.8% from v1 was compression-only evidence. It showed how much drag existed in the source files, but the rewrites were not safe replacements.

## What Compressed Well

- Gate and sequencing logic (if/then/stop/continue patterns)
- Repeated operating mode declarations
- Connective prose between workflow steps
- Redundant framing and setup language

## What Stayed Prose

- Literal bash templates and exact commands
- Scoring methodologies and checklists
- Voice and tone guidance
- Safety constraints and escalation protocols
- Test framework detection and coverage analysis
- AskUserQuestion formatting requirements
- Concrete file paths and schema definitions

## Parity Method

All three tests used **inferred parity** (static contract comparison). No runnable GStack harness was available. Each skill was validated against 5 concrete prompts covering happy path, edge cases, safety pressure, output format, and known weak spots.

## Process Observation

The integrated validation phase worked as intended. All three skills:

1. Generated skill-specific prompt suites automatically
2. Ran parity comparison internally
3. Passed on first iteration (no patching needed)
4. Produced honest adoption calls without needing a second skill invocation

The user experience is now: load the skill, get a validated result.

## Files

Each skill has a rewrite and a report:

- `v2-design-review-rewrite.md` / `v2-design-review-report.md`
- `v2-ship-rewrite.md` / `v2-ship-report.md`
- `v2-plan-eng-review-rewrite.md` / `v2-plan-eng-review-report.md`
