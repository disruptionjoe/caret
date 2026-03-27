# Intake Skill

^intake ^precision8 ^grip8
Capture raw input from Joe without judgment or routing. The job is simple: lose nothing, keep it scannable.

## Trigger

^when Joe shares:

- new information
- a task
- an idea
- a link
- a brain dump
- anything worth remembering

The router sends the work here.

## Capture

^capture

- keep Joe's words
- do not rephrase the core content
- one input = one file
- if one message contains multiple distinct items, create one file per item
- write files to `data/intake/`
- use `<timestamp>-<descriptive-slug>.md`
- make file names human-scannable at a glance

## Normalize

^normalize
If the intake contains multiple distinct concepts, add a preview header above the original text:

```text
# Intake: [Clear descriptive title]

**Summary:** [One line]

**What I see in here ([N] items):**
1. [save for reference] - [one-line description]
2. [worth exploring deeper] - [one-line description]
3. [concrete task] - [one-line description]
4. [system tweak] - [one-line description]

---

[Full original text below]
```

For simple single-concept intake, keep the header minimal:

```text
# Intake: [Clear descriptive title]

**Summary:** [One line]

---

[Full original text below]
```

## Header Rules

^rules

- the header is a preview, not a decision
- do not auto-extract and route during intake
- preserve the full original text under the header
- use natural labels such as:
  - save for reference
  - worth exploring deeper
  - concrete task
  - could become a plan
  - system tweak

## Close

^update
Increment `data/state.json` intake count. If the file does not exist, create it with `{"intake_count": 1}`.

^ack
Confirm in one line: "Logged." or equivalent.

^mobile
If this is a quick mobile capture such as "log this," stop after capture and confirmation.

^ask
Otherwise ask once: "Want me to review this now, or hold it?"

- if Joe says "now," hand off to the paired review skill
- if Joe says "hold" or gives no response, stop
