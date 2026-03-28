# Decision Tree Router

## Notation

```
^^^router ^grip9
  ^^skills/condition-a.md
  ^^skills/condition-b.md
  ^^skills/condition-c.md
  ^^skills/default.md
```

First match wins. The router reads input, selects one branch, loads it. The rest stay unloaded.

## What it does

Routes input down a single path. Top-to-bottom. First branch that matches executes. All others stay unloaded. Returns immediately. Deterministic. No backtracking.

## When to use it

When routing must be repeatable. Same input, same path, always. When subsystems are independent enough to never need visibility into each other. When you want clear accountability—exactly one actor per message. When you need to prevent condition-creep and keep each branch responsible for one thing.

## When not to use it

When a single input should spawn multiple parallel paths. When conditions overlap in ways that matter—early match might shadow better late match. When the tree becomes too large to hold in your head. When runtime context should re-rank branches dynamically.

## Design notes

The router is governance. Not compute. It decides *who decides*, not what they decide about. Ordering is policy. Early match always wins. This forces you to be explicit about priority. If conditions overlap, document it. Better: make them mutually exclusive.

First-match-wins prevents thrashing. You must know your conditions well enough to order them. Treat the catch-all as a mandatory backstop—if something doesn't match, it's a signal the tree is incomplete. Log it. Fix it.

Keep conditions simple. If a condition needs a multi-line comment, it's too complex. Push that logic into the sub-skill. The router reads like a checklist, not like prose.

Load only what you need. If branch A fires, branch B never loads. Lazy loading. In distributed systems, this means sub-skills as isolated files that arrive on demand. The router is the only artifact that needs to know all names.

Reordering the tree changes behavior downstream. Don't reorder casually. If you're tempted to reorder, refactor the conditions instead. The tree has design choices baked into its order.

Testing is deterministic. Feed known inputs. Verify the right sub-skill loads. Verify the others don't. Feed an input that matches nothing. Verify the catch-all fires. No surprises.

Sub-skills should be truly independent. If sub-skill-a needs to read what sub-skill-b returned, you have a pipeline, not a router. A router is terminal: one message → one sub-skill. If you need multi-step orchestration, use a different pattern.

Contrast with `capture-before-route`: a router makes decisions fast and early, accepting that some edge cases may be misclassified. Capture-before-route preserves raw input first, accepting latency. The router is hot. Capture is cool.
