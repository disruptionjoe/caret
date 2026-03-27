<p align="center">
  <img src="assets/caret-logo.svg" alt="Caret^ logo" width="160" />
</p>

# Why Use Caret^

Because most agent workflows are carrying far more prose than they can afford.

Not more clarity.
More drag.

More narrated steps.
More repeated tone-setting.
More headings explaining what the next heading is about to explain.
More giant prompt blocks trying to force discipline through sheer bulk.

Caret^ is the counter-move.

It gives you a small semantic layer for the parts of a workflow that actually repeat:

- hats
- worker boundaries
- gates
- routes
- pressure
- verification
- sequence

That means less ceremony around the work and more signal inside the work.

## The Short Version

Use Caret^ if you keep writing the same operating intent over and over.

Things like:

- review this more carefully
- use this lens
- split this into a separate worker
- treat this as fresh context
- tighten the route logic
- increase verification

That is where Caret^ earns its keep.

If your file is mostly payload, story, schema, or public explanation, keep prose.

Caret^ is not here to replace writing.
It is here to stop workflow prose from eating the workflow.

## What The Data Says

This repo did not stop at theory.
It ran the conversion model against real skills and external repos.

Across 9 local skills in the optimization loop, the rewrites came out **44.2% shorter overall** while preserving the live workflow spine.

See:
- `/research/reports/caret-it-optimization/README.md`

Across 3 large skills from `gstack`, hybrid rewrites reduced the workflow layer by **95.8% overall** once the shared runtime contract was separated from the skill-specific flow.

See:
- `/research/reports/gstack-caret-it-tests/README.md`

And the `autoresearch` pass showed the limit case clearly:

- the operator program (`program.md`) was a strong Caret^ fit
- the public README should stay mostly prose

See:
- `/research/reports/autoresearch-caret-it-tests/README.md`

That is the real argument for Caret^.

Not "everything should become notation."

The real argument is:

use notation where workflow repeats,
keep prose where prose is still doing real work.

## What This Looks Like

Here is the kind of compression Caret^ is built for.

Before:

```text
What you CAN do:
- Modify `train.py` - this is the only file you edit.

What you CANNOT do:
- Modify `prepare.py`.
- Do not add packages or dependencies.
- Do not modify the evaluation harness.
```

After:

```text
^grip9
- Edit only `train.py`.
- Do not modify `prepare.py`.
- Do not add packages or dependencies.
- Do not modify the evaluation harness.
```

Nothing important disappeared.

The rules just stopped introducing themselves like they were arriving at a panel discussion.

## What You Get

When Caret^ is used well, a workflow gets:

- shorter
- easier to scan
- clearer about where scope starts and stops
- cleaner about hat versus worker
- less repetitive without becoming vague

That matters in chats.
It matters in platform skills.
It matters in long-running harnesses where every extra paragraph becomes permanent tax.

## What You Do Not Get

You do not get magic.

Caret^ does not secretly make a weak harness strong.
It does not replace judgment.
It does not mean every Markdown file should become symbols and fragments.

If the file is mostly:

- a public explainer
- a schema
- an example payload
- a legal or safety warning
- a narrative document

then prose should stay prose.

Good Caret^ use is not maximal.
It is selective.

## Why It Feels Better

Most prompt systems are trying to solve chaos by adding mass.

Caret^ solves it by adding shape.

That is a different philosophy.

You do not need more words to say:

- go deeper
- hold the line
- use this lens
- split the worker
- start fresh

You need a cleaner way to say them.

That is the whole bet.

Small marks.
Hard edges.
Clear intent.

If that sounds like the kind of system you want, start with:

1. `/caret-cheatsheet.md`
2. `/onboard-to-caret.md`
3. `/platform/caret-core-starter.md`
