# Executive Assistant Heartbeat

## Scenario

An automated agent runs on a schedule, advancing projects across multiple domains. It reads a directive for instructions, executes work in the correct voice for each domain, logs everything, and never publishes anything. A separate reporting agent communicates with the human. The heartbeat agent operates within strict boundaries.

This is not hypothetical. This is the system that produced the document you are reading.

## Notation

```
^^^heartbeat
  ^govern.readonly "HEARTBEAT.md"
  ^schedule "every 6 hours"

  ^gate.active_hours
    ^check time.between 0600, 2200

  ^^^chief.of.staff
    ^context.selected "chief-of-staff.md", "registry.md", "decisions.md"

  ^each domain in directive.domains
    ^each project in domain.projects where status == "agent-ready"

      ^^cos.assign project
        ^output voice, style, identity

      ^^executor
        ^context.selected project.next_step, project.notes
        ^voice cos.assignment.voice
        ^output "data/drafts/{project.slug}-draft.{ext}"

      ^log project, action, files

  ^gate.human "report"
```

## Annotation

```
^^^heartbeat                    → anchored; remembers what was done in prior runs
  ^govern.readonly "HEARTBEAT"  → directive: reads the governing document but NEVER modifies it
  ^schedule "every 6 hours"     → directive: execution frequency

  ^gate.active_hours            → checkpoint: only run during specified window
    ^check time.between ...     → automated time check

  ^^^chief.of.staff             → anchored routing agent; knows voice assignments and past decisions
    ^context.selected ...       → loaded with routing framework and decision history

  ^each domain ...              → iteration over directive structure
    ^each project ... where ... → filtered iteration; only agent-ready work

      ^^cos.assign project      → ephemeral: CoS determines voice/style for this specific project
        ^output voice, ...      → returns routing assignment

      ^^executor                → ephemeral: does the actual work
        ^context.selected ...   → receives only what this project needs
        ^voice ...              → applies the assigned voice
        ^output ...             → produces draft file with naming convention

      ^log ...                  → directive: append to structured log

  ^gate.human "report"          → final gate: human reviews via separate report agent
```

## Runtime behavior

1. The heartbeat activates on schedule. It checks active hours — if outside the window, it logs a quiet entry and stops.
2. It reads the governing directive (read-only — it cannot modify its own instructions).
3. The Chief of Staff agent loads with routing context: voice registry, decision history, standing rules.
4. For each domain with agent-ready projects, the CoS assigns voice, style, and identity.
5. An ephemeral executor receives the assignment, relevant project context, and the voice guide. It produces a draft file and terminates.
6. Each action is logged in a structured append-only log.
7. A separate report agent (not shown) reads the log and communicates with the human. The heartbeat never talks to the human directly.

## Variations

**Without CoS:** Remove the `^^^chief.of.staff` layer. The heartbeat applies voice directly from a lookup table. Simpler. Loses the ability to make routing decisions based on accumulated history.

**With priority ordering:** Add `^sort projects by domain.priority` before the each-loop. The heartbeat advances high-priority projects first. Useful when token budget is limited and not all projects can be touched per run.

**Multi-executor parallel:** Replace `^^executor` with `^^{domain.agent_count}` to spawn multiple executors per domain. Faster for domains with many agent-ready projects. Riskier — parallel executors may produce conflicting drafts.
