# Exact Targets

Names are light. Exact targets are sharp.

Use names when the harness can resolve them cleanly.
Use exact targets when you want less guessing.

## Named Targets

```text
^^critic
^^^researcher,planner
```

This is convenient. It depends on harness-side resolution.

## Exact Persona Files

```text
^^personas/critic.md
^^review:personas/critic.md,personas/researcher.md
```

This is more explicit. It lowers ambiguity about which asset should be loaded.

## Exact Skill Files

```text
^^skills/editor.md
^^^skills/research.md
```

Targets do not have to be persona labels. Skill files are valid targets too.

## Mixed Precision

```text
^^review:personas/critic.md,ux-designer
```

This is valid. One target is exact. One target still depends on harness resolution.
