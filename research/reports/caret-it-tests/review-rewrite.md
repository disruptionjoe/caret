# Review Skill

^review ^depth7 ^grip8 ^precision8
Walk unprocessed intake through a review gate. Every item gets a disposition. Nothing moves forward without Joe's awareness.

## Trigger

^when

- Joe says "triage"
- Joe says "review inbox"
- Joe says "process intake"
- intake handoff says "review now"

## Intake Review Loop

^review
For each file in `data/intake/` with `"status": "unprocessed"`:

1. present the item in plain language with raw content and capture time
2. ask: "Shelve this, or make a plan?"

## Shelve Path

^shelve
Ask one follow-up: why?

- reference -> move to `data/archive/` with `type: reference`
- backlog -> move to `data/backlog/`
- pending-strategy -> move to `data/reviewed/` with `status: pending`, `pending_reason: pending-strategy`
- pending-info -> move to `data/reviewed/` with `status: pending`, `pending_reason: pending-info`
- pending-timing -> move to `data/reviewed/` with `status: pending`, `pending_reason: pending-timing`

If Joe only says "shelve," default to backlog.

## Plan Path

^plan
Ask two quick things:

- who executes: Joe or EA
- which domain: infer if obvious, otherwise ask

Then create a plan item in `data/plans/` with:

- original content
- `executor: human` or `executor: agent`
- domain
- `status: active`

Keep the plan brief. It is a commitment to act, not a project document.

## After Each Item

^update
Move the intake file to the chosen directory and add:

- `reviewed`: ISO timestamp
- `disposition`: shelve type or `human-plan` / `agent-plan`
- `domain`: life domain

Update `data/state.json` counts.

## Batch Mode

^batch3
If there are many items, present them in batches of 3. After each batch, ask: "Continue, or pause here?"

## Rules

^rules

- Joe decides the disposition
- never auto-assign
- never delete or merge intake items during review
- if Joe is unsure, default to shelve -> backlog
- keep the conversation tight: present item -> shelve or plan -> next item

## Close

^summary
After all items are reviewed, give one line with counts for shelved items, plans, and pending items.
