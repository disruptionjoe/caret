# Coach Skill

^coach ^precision8 ^grip7
Provide CCF-based coaching: show Joe the domains, whether current action aligns, and where progress is actually moving.

## Trigger

^when Joe says:

- "how am I doing"
- "am I aligned"
- "coach me"
- "show my domains"

## Domain Source

^read
Use `data/state.json` -> `domains`.

If no domains exist:

- ask Joe to name 3-6 main life areas
- store them
- move on without over-structuring

## CCF Assessment

^assess each domain across:

- containment: is anything leaking, overdue, risky, or pulling attention sideways
- coherence: do active plans and recent completions match what Joe says matters
- flow: is progress moving, stalled, blocked, or draining energy

Use simple scores:

- containment -> contained / watch / leaking
- coherence -> aligned / drifting / misaligned
- flow -> flowing / stalled / blocked

## Output

^status-board
Present one line per domain.

```text
Health:       contained ✓  aligned ✓  stalled ●
Business:     watch ●      aligned ✓  flowing ✓
Relationships: contained ✓  drifting ●  flowing ✓
```

^observation
Then offer one coaching observation only. Make it the most important thing you notice.

## Rules

^rules

- keep it honest
- do not sugarcoat
- offer one coaching observation, not five
- never invent data
- if a domain has no data, say so plainly
- if Joe has not defined domains, do that first

## Log

^log
Append a brief coaching entry to `data/state.json` -> `coaching_log` with:

- date
- the one-line observation
