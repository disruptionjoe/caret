# Round 2: Priority Skill

## Source

- original: local private skill `priority.md`
- rewrite: `priority-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The start-of-day flow compressed far better than expected because the source repeated step framing and operational intent around every section.
- The JSON note schema stayed literal, which kept the rewrite from hiding implementation detail.
- The main harness assumptions are the tool calls for calendar and email and the ability to gather post-note context in parallel.

## Adoption Call

`adopt`

This round showed that even a dense operational skill can compress hard if the rewrite preserves schemas and concrete file behavior. The right move is not "more prose because it is complex." The right move is "notation for flow, prose for payload."

## Compression Report

- original tokens: `1539`
- rewritten tokens: `774`
- tokens saved: `765`
- percentage shorter: `49.7%`
- projected savings over 1,000 runs: `765000`

## Example Compression

Before:

```text
### Step 1.5: Today's calendar and email

Calendar - Use `gcal_list_events` on Joe's primary calendar for today.
Email - Use `gmail_search_messages` to check for anything urgent.
```

After:

```text
^calendar
Use `gcal_list_events` for Joe's primary calendar today.

^email
Use `gmail_search_messages` for recent unread inbox messages.
```

Why it compresses:

Repeated step narration collapses into direct operating signals, while the real tool-level detail stays visible.

## Log Note

This report file is the completion record for the run.

This rewrite is 49.7% shorter. At roughly 765 tokens saved per run, using it 1,000 times saves about 765000 tokens.
