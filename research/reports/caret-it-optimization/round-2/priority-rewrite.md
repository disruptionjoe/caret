# Priority Skill

^priority ^precision8 ^grip8
Surface what matters most right now. Start-of-day. What's next. What just unlocked.

## Trigger

^when

- Joe opens a session
- Joe says hello
- Joe asks "what's next"
- Joe asks "what matters most"
- Joe reports completing something

## CCF Scoring

^score each surfaced item across:

- containment: what leaks or causes damage if ignored
- coherence: what aligns with Joe's stated goals and strategy
- flow: what creates momentum, unblock, or visible progress

Score each dimension `1-3` and present tags like `C3 Co2 F1`.

## Start-of-Day Flow

^start-of-day
Present in this exact order.

### Step 0: Daily Note

^respond-immediately
Do not read files, call APIs, or check state before this step.

Ask casually:

- how did you sleep
- what do you remember eating yesterday
- did you make it to the gym
- what is your weight today, if tracking
- anything else notable: mood, energy, wins, friction

After Joe responds:

^gather in parallel

- today's note
- calendar
- email
- `data/state.json`
- active plans
- `data/profile/joe.md`
- `data/profile/memory.md`

Store the note in `data/notes/<date>.json`:

```json
{
  "date": "2026-03-18",
  "sleep": "...",
  "food": "...",
  "gym": true,
  "weight": null,
  "notes": "..."
}
```

If Joe skips or says nothing, save a minimal entry and move on.

### Step 1: Well-Being Check

^wellbeing

- check whether health, finances, or relationships are leaking
- surface any active well-being items
- if the note reveals something important, mention it briefly
- if nothing is active and the note looks fine, say one line and move on

### Step 1.5: Calendar And Email

^calendar
Use `gcal_list_events` for Joe's primary calendar today. Show time and title. Flag conflicts or back-to-backs. If clear, say so.

^email
Use `gmail_search_messages` for recent unread inbox messages. Surface up to three urgent items. If quiet, say so.

Keep this section tight.

### Step 2: Project Landscape

^landscape
For each active domain, show one summary sentence of what needs to happen next.

- if on hold -> say `On hold`
- if active plans exist -> surface the 1-2 highest CCF items
- if no items exist -> say `Nothing active`
- if any plan has `draft_status: "drafted"` -> flag it because drafted items are blocked on Joe

### Step 3: Unreviewed Intake

^intake
If there are unprocessed items in `data/intake/`, mention the count and offer triage.

### Step 4: Let Joe Lead

^handoff
Do not force a closing question. Present the landscape and let Joe choose what to engage with.

## Progress Report Handling

^when Joe says something is done

- find the matching item in `data/plans/` or `data/reviewed/`
- move it to `data/archive/` with `status: completed` and a timestamp
- update `data/state.json`
- surface the next most important item by CCF

## Rules

^rules

- never show more than 5 items unless Joe asks
- always show CCF scores
- if there are pending-strategy items, surface them in coaching mode rather than pretending they are actionable
- keep the greeting tight
- if nothing is active, say so plainly
