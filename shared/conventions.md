# Project Brainify — Conventions

Shared rules for all project-brainify skills. Read once per session, do not repeat in skills.

## Layers

| Layer         | Path                  | Who writes        | Purpose                                                   |
|---------------|-----------------------|-------------------|-----------------------------------------------------------|
| Schema        | `CLAUDE.md`           | user + skills     | Documents structure and wiki rules                        |
| Requirements  | `brain/requirements/` | user, interview   | Immutable sources: `requirement_<name>.md`, notes, documents. Never edit. |
| Project files | project root          | project only      | The running project: code, deliverables, docs. Skills read, never write. |
| Wiki          | `brain/wiki/`         | skills only       | Synthesized, linked markdown pages                        |

Project root = everything outside `brain/` and `CLAUDE.md`. A document that should feed the wiki
belongs in `brain/requirements/`, not in the project root.

## Wiki layout

```
brain/wiki/
  index.md        # catalog: every page, one line each, grouped by type
  log.md          # append-only journal: ## [YYYY-MM-DD] <op> | <title>
  sources/        # one page per requirements file
  project_files/  # one page per module, component, deliverable — what actually exists
  entities/       # concrete things: components, pages, tables, roles, tools, phases
  concepts/       # cross-cutting themes: auth, data model, budget, risk
  answers/        # filed query answers worth keeping
```

## Page rules

- Filename: kebab-case, `.md`. Title = H1.
- Frontmatter: `type` (source|project_file|entity|concept|answer), `sources` (list), `updated` (date), `tags`.
  `project_file` pages: `sources` are project paths pinned to a state — `src/auth/login.ts@a1b2c3`
  (git) or `deliverables/plan.docx@2026-10-13` (mtime) — plus `implements` (entities they realize). Wikilinks in frontmatter are quoted: `"[[entity]]"`.
- Links: Obsidian wikilinks `[[page-name]]`. Every page links to ≥1 source and ≥1 neighbour.
- Update existing pages instead of creating duplicates. Check `index.md` first.
- Contradictions: keep both claims, mark `> ⚠ Conflict:` with source names.
- Wiki language follows the raw material. All skill output (questions, drafts, reports) follows the language of the user's prompt.

## Bootstrap (every skill, first step)

1. Look for `brain/` (or an equivalent `requirements/` + `wiki/` pair, older `raw/` counts). If present, adopt it — note deviating names in CLAUDE.md. If absent, propose the layout above; create only after user confirms.
2. Look for `CLAUDE.md` in project root. If absent, propose creating it from `templates/claude-md-section.md`. If present but missing a `## Project Brain` section (or incomplete), propose appending that section. Never touch other content. If complete, do nothing.
3. Read `CLAUDE.md` and `brain/wiki/index.md` before any other work.

## Logging

Append one line to `log.md` per operation: `## [date] interview|ingest|sync|query|lint | <short title>`.
`sync` lines also record the synced state (`@<commit>` or `@<date>`).
