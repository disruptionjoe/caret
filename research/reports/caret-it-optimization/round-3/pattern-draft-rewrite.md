# Pattern Drafting Skill

^pattern-draft ^precision8 ^grip8
Draft a Caret^ orchestration pattern with standard structure, standard voice, and no wasted motion.

## Trigger

^when an agent-ready task says "Draft Caret^ pattern" and points here

## Before Writing

^load

- `data/brand-voice-guide.md`
- `data/drafts/caret-repo-draft/patterns/README.md`
- at least two existing patterns in `data/drafts/caret-repo-draft/patterns/`

## Voice

Keep it crisp, exact, dry, and contemptuous of waste.

You are writing in the tool's voice, not Joe's.

## Structure

Every pattern file has exactly five sections:

1. Notation
2. What it does
3. When to use it
4. When not to use it
5. Design notes

## Notation Section

Use the minimal notation block needed to show the structural decision.

Stay inside the current canon:

- `^` -> directive
- `^^` -> hat, not worker
- `^^^` -> worker boundary
- `^^^^` -> fresh-eyes boundary
- indentation shows scope

If the pattern needs a new notation concept, make it explicit in design notes. Do not extend the notation silently.

## Section Rules

^rules

- "What it does" explains the structural decision, not the whole workflow
- "When to use it" names trigger conditions, not abstract benefits
- "When not to use it" names failure modes, not vague absence
- "Design notes" should be the longest section because that is where the trade-off lives
- always name the core trade-off explicitly
- always relate the pattern to at least one other pattern

## Output

^output

- save to `data/drafts/caret-repo-draft/patterns/[pattern-name].md`
- use kebab-case
- update `data/drafts/caret-repo-draft/patterns/README.md`

## Quality Gate

^check

- voice matches Caret^ rather than generic system prose
- notation uses only established conventions or calls out a deliberate extension
- structure section count is correct
- trigger conditions are specific
- failure modes are specific
- design notes state the trade-off and pattern relationships
- no filler

## Calibration

^calibrate
If the draft is thinner than the existing patterns, it is not done. If it is twice as long, it is probably overexplaining.
