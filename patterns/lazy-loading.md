# Lazy Loading

## Notation

```
^^route:skills/index.md
  ^^^skills/matched-skill.md ^depth7
```

The index is consulted. Only the matched skill is loaded. Everything else stays on disk, unread.

## What it does

System maintains a manifest of available modules. Router reads the manifest, maps input to one skill name. Loads exactly that skill. Everything else remains unread. The current task sees only what it needs. No clutter.

## When to use it

When you have many skills and context is scarce. When each input maps cleanly to one owner-skill. When you can predict which skill runs next based on input alone. When skill files are independent and have no hidden cross-dependencies.

Use this for modular architectures. Coaching system with multiple modes in separate skills. Factory with shift-specific handlers. Any system where current work = exactly one skill.

The pattern shines when you have 50 skills and only 3 will ever run in a single session. Load those 3. Leave 47 on disk.

## When not to use it

When the current task needs coordination across multiple skills. When routing requires reading multiple skills to decide which one is best. When skills share state that lives in code, not in messages.

Don't use lazy loading for tightly coupled systems. Don't use it when the decision of which module to invoke requires understanding the input deeply—that's hidden coupling and defeats the pattern.

## Design notes

The core trade-off is context economy versus cross-skill awareness. Lazy loading buys context room by sacrificing visibility into what other skills exist or what they can do.

The pattern works because routing is deterministic. Input + simple rules = exactly one skill. If routing becomes fuzzy—"maybe A, maybe B, need to investigate"—the pattern breaks. Build a different architecture then.

The index must be separate from skill files. YAML or JSON. Lists every skill and its path. Router reads only this file first. Tiny. Fast. One filesystem lookup per session.

Keep indices shallow. Flat lists with descriptive names beat nested trees. O(n) lookup. n is usually small. Trees are slower mentally and in code.

Skill files should be independent. No cross-skill imports. No module-to-module dependencies baked into code. If skill A needs to call skill B, route through the index. Friction, yes. Good friction. Prevents accidental coupling.

Keep metadata in the index. Not just path—description, owner, version, last_modified. Let the router make smarter decisions. Let maintenance systems understand what they're loading.

Preload the index. Read it once at startup. Hold it in memory. Reread only if you suspect the filesystem changed. Moves cost to initialization time, where one extra read is negligible.

Nest lazy loading within skills. Large skills can have their own index of sub-tasks. Load only the sub-task needed for this turn. Pattern scales. Nested lazy loading becomes aggressive context minimization—the system loads one skill, the skill loads one sub-task.

The pattern imposes discipline: write modular code. If every skill is useful standalone, lazy loading works perfectly. If every skill secretly depends on three others, you end up loading everything anyway. The pattern fails on hidden dependencies.

Contrast with `capture-before-route`: lazy loading optimizes context at load time. Capture-before-route optimizes information flow across time. Lazy loading is about what you load now. Capture is about what you store for later.

This is not micro-services. This is micro-context. Code lives on one machine. It loads in pieces. The goal is clarity and context economy, not distribution.
