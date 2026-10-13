# Contributing to Ai-Native-OS

AI-Native OS is built **incrementally** and to **production quality**. This guide explains how to add
or extend content so the system stays consistent.

---

## Golden rules

1. **Never write placeholder text.** If you cannot write a section for real, leave it out and note it under *Future Improvements*.
2. **Follow the conventions in [STRUCTURE.md](STRUCTURE.md).** Departments, agents, and documents all have a fixed shape.
3. **Prefer depth over breadth.** Finish one thing completely before starting the next.
4. **Keep terminology consistent** with [GLOSSARY.md](GLOSSARY.md).
5. **Cross-link** every new file to the parts of the system it touches, using relative paths.

---

## Adding a new department

1. Copy [`templates/department-template/`](handbook/templates/department-template/) to `<department>/`.
2. Fill in every file. Start with `README.md`, `mission.md`, `principles.md`, then the operational files.
3. Create the department's agents under `agents/<department>/` from [`agents/agent-template.md`](ai/agents/agent-template.md), and index them in `<department>/agents.md`.
4. Add the department to the repository map in the root [README.md](README.md) and to [STRUCTURE.md](STRUCTURE.md).

## Adding a new agent

1. Copy [`agents/agent-template.md`](ai/agents/agent-template.md) to `agents/<division>/<agent-name>.md`.
2. Complete all **11 sections** — an agent spec is incomplete if any section is missing.
3. Register it in [`agents/README.md`](ai/agents/README.md) and the owning department's `agents.md`.

## Adding a starter kit

1. Create `starter-kits/<company-type>/`.
2. Write a `README.md` that explains what it **inherits** from the AI-Native OS core and what it **overrides or adds**.
3. Only include the domain-specific deltas — do not duplicate core content; link to it.

---

## Style

- **Markdown** throughout. Use tables for structured comparisons, fenced code blocks for diagrams/trees.
- **Headings** are sentence-descriptive and unique within a file.
- **Lists over prose** for procedures, checklists, and criteria.
- **Relative links** only (`../orchestration/README.md`), never absolute paths or external mirrors of internal content.

---

## Bilingual documentation

Every `README.md` in this repository is a **triplet**:

| File | Role |
|---|---|
| `README.md` | English source — the source of truth |
| `README.zh.md` | Chinese counterpart |
| `README.i18n.yaml` | Consistency record — the git blob hash of both files |

`node --experimental-strip-types scripts/run-gates.ts` (also run in CI) enforces the triplet through
[scripts/verify-translation-pairing.ts](scripts/verify-translation-pairing.ts): both counterparts must
exist, the record must match the current English source, and the Chinese file must keep the source's
**structural signature** — heading levels, code blocks (language + line count), table dimensions, and
list item counts.

To add or change a bilingual README:

1. Edit `README.md` (or its counterpart) as usual.
2. Translate: `README.zh.md` mirrors the source one structure element at a time. Prose is Chinese; code,
   commands, paths, identifiers, and link targets stay exactly as they are in the source.
3. Keep the language switcher: line 3 is `English | [中文](README.zh.md)` in the English file and
   `[English](README.md) | 中文` in the Chinese one.
4. Same-file anchors (`#anchor`) are the only links that change — they point at the translated heading's
   slug (lowercase, spaces become `-`, so headings carry no punctuation).
5. Re-record and verify: `python scripts/i18n-record.py` (add `--only <path>` to limit it), then run the
   gate again.

Scope and configuration live in [docs-constraint.yaml](docs-constraint.yaml); the gates themselves are
dependency-free scripts in `scripts/`, run with `node --experimental-strip-types` (Node 22+), so
`run-gates.ts` needs nothing installed.

---

## Review before merge

Every change should satisfy:

- [ ] Follows the standard structure for its type (department / agent / document).
- [ ] No placeholder or filler text.
- [ ] All internal links resolve.
- [ ] Bilingual counterpart and its `.i18n.yaml` record are up to date (READMEs only).
- [ ] Terminology matches the glossary.
- [ ] Cross-links to related areas are present.
- [ ] The root README map and STRUCTURE.md are updated if a new top-level area was added.
