---
name: wiki
description: >
  This skill should be used when the user says "ingest", "build the wiki", "add this to the wiki",
  "synthesize the requirements" (mode ingest: one requirements file → linked wiki pages), or
  "sync the wiki", "update the wiki from the code", "what changed in the project" (mode sync:
  project files → project_files pages). One requirements file or one sync per run.
---

# Wiki (ingest | sync)

Keep the wiki in step with the two things that feed it: requirements and the running project.

Read `${CLAUDE_PLUGIN_ROOT}/shared/conventions.md` first and run its Bootstrap steps.

## Mode ingest — requirements → sources, entities, concepts

1. Pick the source: the file the user names, else the newest unprocessed file in `brain/requirements/`
   (compare against `wiki/sources/`). One file per run.
2. Read `wiki/index.md`, then the source in full.
3. Write `wiki/sources/<name>.md`: summary, key claims, open questions.
4. Extract entities — concrete building blocks by project type:
   software: frontend, pages, backend, tables, functions, integrations, roles;
   non-software: phases, roles, deliverables, resources, locations.
   Extract concepts — cross-cutting themes (auth, data model, budget, risk, timeline).
5. For each: if a page exists, update it and add the new source to its frontmatter;
   else create it from `${CLAUDE_PLUGIN_ROOT}/shared/templates/page.md`.
   Link every page to its source and its neighbours with `[[wikilinks]]`.
6. Update `index.md` (every new or changed page, grouped by type) and append to `log.md`.
7. Report: pages created / updated, contradictions found, suggested next sources.

## Mode sync — project root → project_files

1. Find the last sync state in `log.md` (`@<commit>` or `@<date>`). None → full walk.
2. List what changed: git → `git diff --name-only <last>..HEAD`; no git → files with mtime after `<last>`.
   Ignore `brain/`, `CLAUDE.md`, dependencies, build output.
3. Group changes into units a reader cares about (software: module, component, table, API;
   non-software: deliverable, folder, phase artifact). One `wiki/project_files/<unit>.md` per unit:
   what it is, what it does, where it lives, open TODOs found inside. Pin `sources` to the current state.
4. Match each unit to planned entities. Set `implements: ["[[entity]]"]`; add a backlink on the entity.
   No matching entity → note `> ⚠ Unplanned:` on the page. Entity planned differently → `> ⚠ Conflict:`.
5. Update `index.md`, append `## [date] sync | <n> units @<state>` to `log.md`.
6. Report: units created / updated, unplanned, conflicts, entities still without a project file.

## Rules

- Never write outside `brain/wiki/`. Requirements and project files are read-only for this skill.
- Prefer updating over creating. Search index and filenames before adding a page.
- Contradictions: keep both claims with a `> ⚠ Conflict:` note, do not resolve silently.
- Keep pages short: summary, details, related. Depth belongs in the source page or the file itself.
