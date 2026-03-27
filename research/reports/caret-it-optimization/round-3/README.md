# Round 3 Summary

Round 3 tested boundary and adversarial files:

- `queue-sync.md`
- `caret-content.md`
- `pattern-draft.md`

## Results

| Skill | Original Tokens | Rewritten Tokens | Saved | Shorter | Adoption |
| --- | ---: | ---: | ---: | ---: | --- |
| `queue-sync.md` | 1092 | 551 | 541 | 49.5% | adopt |
| `caret-content.md` | 693 | 353 | 340 | 49.1% | hybrid |
| `pattern-draft.md` | 1104 | 534 | 570 | 51.6% | hybrid |
| **Total** | **2889** | **1438** | **1451** | **50.2%** | **boundary round** |

## Round Signal

This round found the real edge case.

The boundary is not "Caret^ cannot compress meta-docs."

The boundary is "some source files are not merely verbose. They are semantically stale."

## Patch Implication

Caret-it should add a canonical-alignment gate:

- if the source conflicts with current Caret^ canon
- do not treat it as a normal notation rewrite
- first normalize semantics
- then evaluate compression and adoption
