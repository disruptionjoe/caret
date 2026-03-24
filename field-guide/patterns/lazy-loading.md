# Lazy Loading

## Notation

```
^index: {skill: path}
^load: skill_name
```

The index is consulted. Only the named skill is loaded. Everything else remains on disk, unread.

## What it does

The system maintains a manifest of available modules. When needed, one module is loaded into working context. Everything else is ignored. The current task sees only what it needs. Nothing more lands in context.

The router reads the index, maps the request to the right skill, and loads exactly that skill file. Other skill files are never read. Other modules do not clutter the working memory.

## When to use it

When you have many skills and context is tight. When the current task has a clear owner—one skill that handles it best. When you can predict which skill will run next based on the current input.

Use this for modular systems. A coaching system with multiple coaching modes, each in its own skill file. A factory with different shift handlers. Any architecture where the current work maps to exactly one module.

The pattern shines when you have 50 skills and only 3 will ever be used in a single turn. Load those 3. Leave the other 47 on disk.

## When not to use it

When the current task needs coordination across multiple modules. When you cannot predict which skill is needed until you understand the input deeply. When skills need to share state that lives in code.

Do not use lazy loading for tightly coupled systems. Do not use it when the decision of which module to invoke requires reading all available modules.

## Design notes

The core trade-off is context economy versus cross-skill awareness. Lazy loading buys you context room by sacrificing the ability to know what other skills exist or what their signatures are.

This pattern works because _routing is deterministic_. The current input, combined with simple rules, maps to exactly one skill. If routing becomes fuzzy—"maybe skill A, maybe skill B, depends on what we read"—the pattern breaks. Then you need different architecture.

The index must be maintained separately from the skill files themselves. A YAML or JSON file that lists every available skill and where it lives on disk. The router reads only this file first. Tiny. Fast. Then one lookup into the filesystem.

Keep indices shallow. Nested categories are tempting. Resist them. A flat list with dot-notation names scales better than a tree. `coaching.empathy`, `coaching.feedback`, `factory.morning_shift`. Lookups are O(n) for a list, and n is usually small. O(log n) for a tree, but trees need more code and more mental overhead.

Skill files should be independent. No cross-skill requires statements in the code. If skill A needs to call skill B, handle that through the index and routing layer, not through imports. This is friction, but it is good friction. It prevents accidental coupling.

Keep metadata in the index. Not just the path—what does this skill do? When was it last modified? Who owns it? A simple `description` and `owner` field. Then the router or a maintenance system can make smarter decisions about which skill to load.

Preload the index. Read it once at startup, hold it in memory. Reread it only if you suspect the filesystem changed. This moves the cost of loading to initialization time, where one extra read is negligible.

Consider lazy loading within skills. A large skill file can have its own index of sub-tasks. Load only the sub-task needed for the current turn. The pattern scales. Nested lazy loading becomes aggressive context minimization—the skill loads only what it needs, the system loads only which skill is needed.

The pattern imposes a discipline: write modular code. If every skill is useful in isolation, lazy loading works perfectly. If every skill secretly depends on three others, the pattern collapses and you end up loading everything anyway.

Lazy loading pairs well with Async Handoff. The overnight factory uses lazy loading to load only the batch processor skill. The morning summary uses lazy loading to load only the summarizer skill. Different agents. Different context footprints. Same codebase.

This is not micro-services. This is micro-context. You keep the code on one machine, but you load it in pieces. The goal is clarity, not distribution.
