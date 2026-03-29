# Hat Before Worker

## Notation

```
^^analyst ^depth7
```

vs.

```
^^^analyst ^depth7
```

Default to `^^`. Reach for `^^^` only when the work requires independent reasoning that the current worker cannot provide without contamination.

## What it does

Forces a deliberate choice between mode shift and worker spawn. Most tasks that feel like they need a new agent actually need a new lens on the same agent. The hat swap (`^^`) keeps context, keeps memory, keeps cost low. The worker spawn (`^^^`) creates a separate responsibility boundary — useful, but expensive and context-destroying.

The pattern says: try the hat first. If the current worker with a new perspective can handle it, you just saved a spawn, a context rebuild, and a coordination problem.

## When to use it

When you're about to spawn a new worker and haven't asked whether a mode shift would do the job.

Specific triggers:

- Review tasks where the reviewer doesn't need independence from the creator's context
- Perspective shifts within a single workflow (researcher → writer → editor)
- Skill loading where the skill augments the current worker rather than replacing it
- Any time the spawned worker would need to re-read most of what the current worker already knows

## When not to use it

When independent reasoning matters. Fresh-eyes review (`^^^^`) requires a clean context boundary — a hat swap defeats the purpose. When the new perspective must not be contaminated by what the current worker believes, spawn the worker.

Also wrong when the spawned worker needs to run in parallel. Hat swaps are sequential. If you need three perspectives working simultaneously, you need three workers.

And wrong when the current context window is already overloaded. Spawning a new worker with a targeted context load may outperform a mode shift on a bloated window.

## Design notes

The trade-off is efficiency versus independence. A hat swap is cheaper, faster, and preserves context. A worker spawn is more expensive but guarantees a separate reasoning path.

Most systems default to spawning because it feels safer. "Give it its own agent." But spawning is the expensive choice. Every spawn carries overhead: context loading, coordination, result integration, potential voice drift. The hat swap avoids all of that.

The heuristic: if you would brief the new worker on everything the current worker already knows, use a hat. If the new worker needs to not know what the current worker knows, use a spawn.

`^^` is "same person, different hat." The analyst puts on a reviewer hat, does the review, takes the hat off. Context intact.

`^^^` is "different person." The reviewer has never seen the analyst's reasoning. That independence is the point.

Relationship to **Disposable Specialists**: specialists are spawned workers. This pattern asks whether you need a specialist at all, or just a specialist's lens.

Relationship to **Context Refresh**: when context contamination is the concern, `^^^^` (fresh-eyes boundary) is the right tool. Hat Before Worker handles the cases where contamination is not a risk.

Relationship to **Layered Authority**: authority layers often use mode shifts for coordination (`^^coordinator`) and spawns for execution (`^^^worker`). This pattern reinforces that split.
