# Queue Sync

^queue ^sync ^verification8
Ensure plans drafted during a session get wired into the night factory before the session ends.

## Problem

Plans can be created in `data/plans/` without ever being added to `ea-os/NIGHT-FACTORY.md`.

That gap makes work disappear from the factory.

## Trigger

^when

- a session created or modified files in `data/plans/`
- midday closing log runs
- triage produced new plans
- Joe asks to sync the queue
- the evaluator runs its late pass

## Scan

^scan for files in `data/plans/` that:

- were created or modified today or since the last sync
- have `Executor: agent`
- are not already referenced in `ea-os/NIGHT-FACTORY.md`

Check for either the filename or a close match of the plan title.

## Classify

^classify each unqueued plan:

- domain
- goal
- status: `agent-ready` or `needs-joe`
- next step

Use these rules:

- clear agent-executable next step -> `agent-ready`
- human executor or Joe input needed -> `needs-joe`
- draft status with open questions -> `needs-joe`
- no matching goal -> flag for Joe, do not create a new goal silently

## Report

^report
Show the sync summary with:

- plan title
- domain and goal
- status
- next step

## Add

^route

- if Joe is present -> show the report and ask whether to add the items
- if autonomous -> add `agent-ready` items automatically
- if midday closing -> add automatically and mention it in the summary
- never create new domains or new goals without Joe's approval

## Log

^log
Append the sync result to `data/notes/night-factory-log.md` with:

- timestamp
- plans scanned
- new items added
- items flagged for Joe
- already queued items

## Directive Row

^row
When adding to `ea-os/NIGHT-FACTORY.md`:

- find the correct domain section and goal table
- add the row with project name, status, last-advanced placeholder, and next-step summary
- include the full plan path in the next-step column
- include task spec paths when relevant

## Exclusions

^exclude

- do not create new plans
- do not create new goals or domains
- do not modify existing directive rows
- do not execute tasks
- do not change plan files

This skill only bridges the gap between "plan exists" and "factory knows."
