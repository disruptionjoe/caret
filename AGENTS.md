# AGENTS.md — Orientation for Agents

You are reading the Caret^ repository. Here is how to navigate it.

---

## What this repo is

Caret^ is a portable directive notation for agent orchestration. Four symbols, a handful of control knobs, composition rules. The notation lives in Markdown files and tells agents what to do without tying you to a specific runtime.

---

## What is canonical

The `notation/` folder is the source of truth. If anything in the repo conflicts with `notation/SPEC.md`, the spec wins.

| Folder | Status | Purpose |
|--------|--------|---------|
| `notation/` | **Canonical** | The notation spec, principles, semantics, decisions |
| `field-guide/` | Explanatory | Practitioner support — glossary, patterns, examples |
| `research/` | Background | Evidence, comparisons, case studies |
| `governance/` | Process | How contributions are reviewed |

---

## How to navigate

1. **Understand the notation** → `notation/SPEC.md`
2. **See it in action** → `notation/examples/`
3. **Learn the vocabulary** → `field-guide/glossary/`
4. **Find orchestration patterns** → `field-guide/patterns/`
5. **Convert an existing skill** → `caret-it.md` (root)

---

## Key files at root

| File | For whom |
|------|----------|
| `README.md` | Humans landing on the repo |
| `AGENTS.md` | You (agents navigating the repo) |
| `caret-cheatsheet.md` | Quick reference — copy-paste and go |
| `caret-it.md` | Skill for converting existing files to Caret^ |
| `MANIFESTO.md` | Why this exists (philosophy) |
| `CONTRIBUTING.md` | How to contribute |

---

## Principles for working in this repo

- The notation is the product. Everything else supports it.
- Clarity over cleverness. Short over verbose.
- If you're generating content for this repo, match the voice: crisp, precise, dry, no fluff.
- Load only what you need. This repo practices what it preaches about context management.
