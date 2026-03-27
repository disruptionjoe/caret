# Memory Skill

^memory ^precision8 ^grip8 ^verification8
Manage Joe's persistent profile and evolving memory without turning conversation into a form.

## Files

- `data/profile/joe.md`: static facts, preferences, schedule, work style, non-negotiables
- `data/profile/memory.md`: dated learnings, patterns, decisions, recurring context

## Trigger

^passive
Session start does not need a separate memory pass. The priority flow already loads both profile files.

^active
During conversation, watch for:

- a decision and why
- an emerging pattern
- a stated preference or constraint
- durable personal context affecting capacity
- a correction to existing profile data

## Route

^route

- static fact change -> edit `data/profile/joe.md`
- new learning, pattern, or decision -> append a dated line to `data/profile/memory.md`

## Rules

^rules

- update quietly
- do not ask permission to store memory
- mention only significant updates, one sentence max
- never capture speculation
- only store what Joe states directly or what repeated behavior clearly supports
- keep entries concise: date plus one-line insight

## Explicit Requests

^when Joe says "what do you know about me?"
- summarize key facts from `data/profile/joe.md`
- surface the most relevant patterns from `data/profile/memory.md`
- keep it conversational, not a data dump

^when Joe says "remember that I..."
- update the right file
- confirm briefly

^when Joe says "update my profile"
- ask what changed
- make the edit
- confirm briefly

## Daily Drip Question

^optional ^limit1
After the start-of-day note exchange, one lightweight personal question may be asked if the morning is not already heavy.

^ask

- keep it conversational
- weave it into the greeting naturally
- if Joe ignores it or says "skip," move on
- use it to fill thin profile areas or test an emerging pattern

^skip

- bad sleep
- dad health issues
- visibly high-stress morning
- any day where more pressure would be noise

^track
Check `data/notes/` for today's date. If a `drip_question` field already exists, do not ask another one. After asking, append the question to today's note.

## Do Not Capture

^exclude

- temporary emotional states unless they reveal a recurring pattern
- task-level details
- anything Joe marks off the record
- guesses without clear evidence
