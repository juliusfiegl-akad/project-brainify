## Project Brain

This project keeps a Karpathy-style LLM wiki in `brain/`.

- `brain/requirements/` — immutable sources (`requirement_<name>.md`, notes, documents). Humans add, nobody edits.
- Project root (everything else) — the running project. Skills read it, never write.
- `brain/wiki/` — LLM-maintained pages: `sources/`, `project_files/`, `entities/`, `concepts/`, `answers/`, plus `index.md` (catalog, read first) and `log.md` (append-only journal).
- Pages use frontmatter (`type`, `sources`, `updated`, `tags`) and Obsidian wikilinks `[[page]]`.
- Update existing pages before creating new ones. Mark contradictions, never silently overwrite.

Skills: `/project-brainify:interview` (idea → requirements), `/project-brainify:wiki` (ingest: requirements → wiki, sync: project files → wiki), `/project-brainify:query` (ask the wiki), `/project-brainify:lint` (health check).
