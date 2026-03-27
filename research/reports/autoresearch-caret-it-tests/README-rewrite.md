# autoresearch README hybrid proposal

This is not a full Caret^ rewrite.

The public README should stay mostly prose.

What Caret^ can tighten is the operator-facing handoff section.

## Suggested Tightening

Replace the current "Running the agent" block with something like this:

````markdown
## Running the agent

Load `program.md` as the live operator surface.

Keep these files in scope:
- `README.md`
- `prepare.py`
- `train.py`

Core boundaries:
- edit `train.py` only
- do not modify `prepare.py`
- do not change dependencies
- baseline first
- then iterate autonomously until interrupted

Starter prompt:

```text
Read `program.md`, `README.md`, `prepare.py`, and `train.py`.
Do setup first.
Establish the baseline.
Then start the experiment loop.
```
````

## Why Only This

The rest of the README is doing public-repo work:

- story
- context
- quick start
- design rationale
- platform notes
- fork references

That material should stay prose-forward.
