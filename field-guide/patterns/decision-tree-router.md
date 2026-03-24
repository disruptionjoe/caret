# Decision Tree Router

## Notation

```
^
  decision-tree-router
    ^ [first-match-wins ordering]
      ^^ [condition A] → load sub-skill-a
      ^^ [condition B] → load sub-skill-b
      ^^ [condition C] → load sub-skill-c
      ^^ [catch-all] → load default
```

## What it does

Routes an input message down a linear decision tree. Evaluates conditions top-to-bottom. Takes the first branch that matches. Loads only the sub-skill needed to handle that branch. Everything else stays unloaded. Returns early.

## When to use it

When you need determinism. When identical inputs must always produce identical routing. When you want to prevent condition-creep (each branch is responsible for one thing). When subsystems are independent enough that mutual visibility isn't needed. When you need clear accountability—which sub-skill was invoked, and why.

## When not to use it

When conditions overlap in ways that matter. When a single input should potentially trigger multiple sub-skills in parallel. When the tree grows beyond a human's ability to read top-to-bottom in one sitting. When you need to re-rank branches based on runtime context.

## Design notes

The router is a governance layer, not a compute layer. It makes no decisions about content. It only decides *who decides*. Ordering matters absolutely. A condition that matches early will always match early, even if a later branch would be more precise. This is a feature. It forces the designer to be explicit about priority.

First-match-wins prevents thrashing. If you have overlapping conditions, you must be deliberate about which one wins and why. Document the priority in a comment. Make the conditions mutually exclusive if possible; if not, document the fallthrough behavior.

The catch-all at the bottom must exist. A message that doesn't match any condition is a runtime error. Fail explicitly. Log which message hit the catch-all. Treat it as a signal that the tree is incomplete.

Each branch should be simple. If the condition is complex enough to need a multi-line comment, it's too complex. Move that logic into the sub-skill, or split the branch. Keep the router readable.

Load only what you need. If condition A selects sub-skill-a, do not load sub-skill-b. Lazy loading is the point. In an EA-OS context, this means keeping sub-skills as isolated files that load on demand. The router is the only file that needs to know all sub-skill names.

Testing is straightforward. Test each branch by feeding it an input that matches exactly. Verify that the right sub-skill loads and the others don't. Test the catch-all by feeding it an input that matches nothing. Verify it lands where you expect.

In a multi-agent system, the router is the top-level authority. It's where policy lives. Changes to routing policy are changes to the tree. Changes to branch behavior are changes to the sub-skill. Keep them separate. A sub-skill that changes its own routing behavior is subverting the system.

The router works best when sub-skills are truly independent. If sub-skill-a needs to know what sub-skill-b returned, you have a pipeline, not a router. A router is terminal: each message ends in exactly one sub-skill. If you need multi-step orchestration, use a different pattern.

First-match-wins also means the router has memory of its design choices baked in. Reordering the tree can change the behavior of all downstream items. Don't reorder casually. If you're tempted to reorder, you probably need to refactor the conditions instead.
