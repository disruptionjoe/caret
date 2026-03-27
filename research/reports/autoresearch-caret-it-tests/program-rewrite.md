# autoresearch in Caret^

This version keeps the live operator spine in Caret^ and keeps commands, output shapes, and logging schema literal.

## Mission

^autonomy9 ^verification8 ^precision8
Run autonomous single-GPU research on `train.py`.

Optimize for lower `val_bpb` under the fixed 5-minute training budget.

Keep simpler code when gains are comparable.

## Setup

^setup
  Complete these before experimentation begins:

  1. Agree on a fresh run tag based on today's date, e.g. `mar5`.
  2. Create branch `autoresearch/<tag>` from current `master`.
  3. Read these files for full context:
     - `README.md`
     - `prepare.py`
     - `train.py`
  4. Verify `~/.cache/autoresearch/` contains data shards and a tokenizer.
     If missing, tell the human to run:

     ```bash
     uv run prepare.py
     ```

  5. Initialize `results.tsv` with header only.
  6. Confirm setup looks good.
  7. Start experimentation.

## Hard Boundaries

^grip9
- Edit only `train.py`.
- Do not modify `prepare.py`.
- Do not add packages or dependencies.
- Do not modify the evaluation harness.
- Treat `evaluate_bpb` in `prepare.py` as ground truth.

## What To Optimize

^depth7 ^scope6
Lower `val_bpb`.

The 5-minute budget is fixed, so training time is already controlled.

VRAM is a soft constraint:
- meaningful increases are acceptable
- dramatic blowups are not

Simplicity breaks ties:
- equal gain with simpler code wins
- tiny gain with ugly complexity usually loses
- equal or better results from deleting code is a strong win

The first run is always the unmodified baseline.

## Run Output

When the run succeeds, expect output shaped like this:

```text
---
val_bpb:          0.997900
training_seconds: 300.1
total_seconds:    325.9
peak_vram_mb:     45060.2
mfu_percent:      39.80
total_tokens_M:   499.6
num_steps:        953
num_params_M:     50.3
depth:            8
```

Extract key metrics with:

```bash
grep "^val_bpb:" run.log
```

## Results Log

^log
  Record every experiment in `results.tsv`.

  Use tab-separated values, not commas.

  Header:

  ```text
  commit	val_bpb	memory_gb	status	description
  ```

  Columns:
  1. short git commit hash
  2. `val_bpb`, or `0.000000` for crashes
  3. peak memory in GB rounded to one decimal, or `0.0` for crashes
  4. status: `keep`, `discard`, or `crash`
  5. short experiment description

  Example:

  ```text
  commit	val_bpb	memory_gb	status	description
  a1b2c3d	0.997900	44.0	keep	baseline
  b2c3d4e	0.993200	44.2	keep	increase LR to 0.04
  c3d4e5f	1.005000	44.0	discard	switch to GeLU activation
  d4e5f6g	0.000000	0.0	crash	double model width (OOM)
  ```

## Experiment Loop

^autonomy9
Once the loop begins, do not stop unless the human interrupts.

Do not ask whether to continue.

^loop
  1. Inspect current branch and commit.
  2. Edit `train.py` with one experimental idea.
  3. Commit the change.
  4. Run:

     ```bash
     uv run train.py > run.log 2>&1
     ```

  5. Extract:

     ```bash
     grep "^val_bpb:\|^peak_vram_mb:" run.log
     ```

  6. If grep is empty, inspect:

     ```bash
     tail -n 50 run.log
     ```

     Fix obvious mistakes and rerun only if the idea still looks sound.

  7. Append the result to `results.tsv`.
  8. If `val_bpb` improved, keep the commit and continue from there.
  9. If `val_bpb` is equal or worse, revert to the previous good commit.

## Failure Rules

^precision8
- If a run exceeds 10 minutes, kill it and treat it as failure.
- If a run crashes from something trivial, fix and rerun.
- If the idea is fundamentally broken, log `crash`, revert, and move on.
- Rewinds are allowed, but should be rare.

## Operating Stance

^autonomy9 ^depth8
You are an autonomous researcher.

Keep generating ideas.
Re-read the in-scope files when you stall.
Combine near-misses.
Try simpler wins before decorative complexity.
Try radical changes when the search is flat.

The loop runs until the human stops it.
