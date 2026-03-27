# Round 3: Queue Sync

## Source

- original: `C:\Users\joe\JoeEA\ea-os\skills\queue-sync.md`
- rewrite: `C:\Users\joe\JoeEA\caret-repo\research\reports\caret-it-optimization\round-3\queue-sync-rewrite.md`
- token method: `ceiling(character_count / 4)`

## Findings

- The source compressed well because it repeats scan, classify, report, add, and log phases with heavy narration.
- The row-format logic stayed visible, which kept the rewrite operational rather than vague.
- The main harness assumption is accurate detection of already-queued plans and stable parsing of `ea-os/NIGHT-FACTORY.md`.

## Adoption Call

`adopt`

This is a strong fit for Caret^ because the file is really a sequence of operating phases. The notation makes those phases explicit without hiding the file-level mechanics.

## Compression Report

- original tokens: `1092`
- rewritten tokens: `551`
- tokens saved: `541`
- percentage shorter: `49.5%`
- projected savings over 1,000 runs: `541000`

## Example Compression

Before:

```text
### Step 2: Classify each unqueued plan

For each plan found, determine:
- Domain
- Goal
- Status
- Next Step
```

After:

```text
^classify each unqueued plan:
- domain
- goal
- status
- next step
```

Why it compresses:

The conversion removes the heading-plus-explanation scaffold and leaves only the working structure.

## Log Note

This report file is the completion record for the run.

This rewrite is 49.5% shorter. At roughly 541 tokens saved per run, using it 1,000 times saves about 541000 tokens.
