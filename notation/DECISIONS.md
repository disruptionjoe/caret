# Notation Decisions Log

Design decisions specific to the notation. Newest first.

For project-level decisions (naming, structure, governance), see the project decisions log.

---

## ND-001 — Control knobs are ordinal, not categorical

**Date:** 2026-03-24
**Status:** Decided
**Decision:** Knobs like `^depth`, `^temp`, and `^grip` use a 0–9 ordinal scale, not categorical labels like `high`/`medium`/`low`.
**Rationale:** Numbers compose better, compare better, and are more precise. `^depth7` is unambiguous. `^depth.high` invites the question "how high?" The ordinal scale also enables machine comparison between agent configurations.

---

## ND-002 — `^grip` is orthogonal to `^temp`

**Date:** 2026-03-24
**Status:** Decided
**Decision:** Prescriptiveness (`^grip`) and creative range (`^temp`) are separate, composable knobs.
**Rationale:** You can be creative and non-prescriptive (`^temp7 ^grip2` = "here are three unconventional options, no recommendation"). Or conservative and highly prescriptive (`^temp2 ^grip9` = "do exactly this standard thing"). Collapsing them into one control loses a full dimension of agent behavior.

---

<!-- Future decisions go here -->
