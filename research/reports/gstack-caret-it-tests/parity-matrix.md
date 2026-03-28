# Gstack Caret-it Parity Matrix

This matrix reflects the stricter behavioral parity rerun.

The comparison was **inferred**, not fully executed, because no local gstack harness was available in this workspace.

That means each result comes from static contract comparison:

- required questions and prompts
- required commands and side effects
- required outputs and templates
- safety and approval boundaries
- logging and completion behavior

| Skill | Shorter | Parity | Adoption | Replacement-ready | Main Gap |
| --- | ---: | --- | --- | --- | --- |
| `design-review` | 94.7% | `partial` | `hybrid` | `no` | Shared contract and exact audit surfaces are referenced, not preserved inline |
| `ship` | 96.9% | `fail` | `keep mostly prose` | `no` | Release commands, templates, and platform-specific gates are too exact to compress this aggressively |
| `plan-eng-review` | 95.2% | `partial` | `hybrid` | `no` | Lens structure survives, but dashboard, report, and logging contract stay underspecified |

## Read This Correctly

The old run proved there is a lot of token drag in these files.

The stricter rerun shows something else:

compression is not the same thing as replacement.

Until the shared gstack runtime contract is extracted into a real reusable artifact, and the local literal surfaces stay embedded where they matter, these rewrites are best treated as design evidence, not drop-in skill replacements.
