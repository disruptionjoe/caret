# Onboard to Caret^

Ten minutes. Then you are using it.

The goal is simple:

- get Caret^ working today
- avoid loading the whole repo into the hot path
- make the cheatsheet the thing your platform actually honors
- give you one clean default install path before you branch into platform specifics

## The Recommendation

Use one of these three paths:

1. Best: make Caret^ a platform-level skill or instruction layer that points at `/caret-cheatsheet.md`
2. Good: make Caret^ a platform-level skill by pasting the full cheatsheet into that skill
3. Fine: paste `/caret-cheatsheet.md` directly into a chat or project and start using it

If you think you will use Caret^ more than once or twice, skip the one-off paste and do the platform-level setup.

## Path A: Quick Start

This takes about 2 minutes.

1. Open `/caret-cheatsheet.md`.
2. Paste it into your current agent session, project instructions, or chat setup.
3. Try one lens, one worker, and one fresh-eyes test.

Use these:

```text
^^reviewer ^depth7
  Review this paragraph for weak claims.
```

```text
^^^planner ^depth8
  Give me a 3-step plan to launch this feature.
```

```text
^^^^
Treat the next paragraph as fresh context.
^^^^
```

4. If the model handles those cleanly, you are live.

## Path B: Platform-Level Setup

This is the recommended path.

This takes about 10 minutes.

### Step 1: Keep the Repo Reachable

Make sure your platform, harness repo, or skill system can reach this repo or at least a local copy of:

- `/caret-cheatsheet.md`
- optionally `/notation/` for deeper interpretation

Do not start by loading the whole repo into the live instruction path.

Start with the cheatsheet. Keep the rest nearby.

### Step 2: Create a Primary Caret^ Skill

In your platform's primary skill or instruction layer, create a file or section for Caret^.

Examples:

- a Claude-style `SKILL.md`
- a Codex or agent shared instruction file
- a project-level instruction block
- a harness repo module that loads before task-specific skills

If you want the recommended starting point, use `/platform/caret-core-starter.md`.

If you need a platform-shaped wrapper after that, use `/platform/README.md`.

### Step 3: Load The Core Starter

Open `/platform/caret-core-starter.md`.

Use the starter block there as your base install.

If your platform can load external files, point that block at the local `caret-cheatsheet.md`.

If your platform cannot load external files, paste the full contents of `/caret-cheatsheet.md` directly under that block.

If your platform needs a platform-specific wrapper shape, adapt from `/platform/README.md` after the core starter is in place.

If your platform uses plugins or connectors to mount docs, check `/platform/plugin-loader-starter.md` before you improvise.

### Step 4: Load It Early

Make sure Caret^ is loaded before task-specific skills.

That is the whole game.

Caret^ should be the signal layer your platform already knows how to read, not a specialty add-on that only appears later in the stack.

### Step 5: Smoke Test It

Run these three tests:

```text
^^reviewer ^depth7
  Review this paragraph for weak claims.
```

```text
^^^planner ^depth8
  Give me a 3-step plan to launch this feature.
```

```text
^^skills/editor.md
  Tighten this draft without changing the meaning.
```

You are looking for three things:

- `^^` stays in the same worker
- `^^^` creates a separate worker boundary
- exact file targets behave more precisely than loose names

### Step 6: Keep Literal Text Literal

Make sure your platform does not treat fenced code blocks as live instruction.

That check matters.

Many notation systems get sloppy here.

Caret^ should not.

## If You Are Doing Harness Setup

Point your harness repo or platform-level skill at the cheatsheet first.

Then keep the rest of the repo in support order:

1. `/caret-cheatsheet.md`
2. `/notation/`
3. `/glossary/`
4. `/examples/`
5. `/patterns/`
6. `/research/`

This keeps the live signal layer small and the supporting material available without making the runtime path bloated.

## What Not To Do

- do not load drafts, archives, and research into the primary live instruction path
- do not treat examples or patterns as more authoritative than the cheatsheet
- do not start by inventing platform-specific syntax extensions
- do not paste the whole repo into a platform skill if the cheatsheet is enough
- do not mix stale Caret semantics with the current canon

## The Fast Mental Model

Remember this and you are most of the way there:

- `^` tells the system what kind of pressure or operation you want
- `^^` changes the hat
- `^^^` changes the worker
- `^^^^` resets the context boundary

Small core. Clear intent. No wasted motion.

## After You Are Live

Use these next:

1. `/caret-cheatsheet.md`
2. `/examples/README.md`
3. `/platform/caret-core-starter.md`
4. `/Caret-it-skill.md`
5. `/platform/README.md` if you need a platform-specific wrapper

That order keeps the canon in front and the experiments behind it.
