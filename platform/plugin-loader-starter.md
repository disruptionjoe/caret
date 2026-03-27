# Plugin / Connector Loader Starter

Use this only if your platform supports mounted docs, repo connectors, or plugin-style instruction loading with stable precedence.

Use `/platform/caret-core-starter.md` first.

This file is the plugin-loader wrapper around that core install.

If not, use a normal platform skill instead.

## When This Is Worth It

Use a plugin or connector layer when:

- it can mount `caret-cheatsheet.md` directly
- it can keep that mount read-only or clearly authoritative
- it can load the mount before task-specific tools or skills
- it can preserve literal code blocks as literal text

If your platform cannot guarantee those, skip this path.

## Starter Shape

```text
plugin: caret-core
mounts:
  - path: caret-cheatsheet.md
    role: primary_instruction
  - path: notation/
    role: canonical_support
  - path: glossary/
    role: optional_term_support

precedence:
  - local live repo canon
  - mounted canonical support
  - downstream examples and patterns
  - research and imported material

literalization:
  - fenced code blocks
  - quoted examples
  - copied external snippets

resolution:
  - exact file targets preferred when present
  - if mounted support conflicts with downstream examples, canon wins

activation:
  - load plugin before task-specific plugins or workflow modules
```

## Recommendation

Treat the plugin as a loader, not as the place where Caret^ itself gets reinvented.

The plugin should mount canon.
Not replace canon.
