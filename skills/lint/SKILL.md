---
name: lint
description: >
  This skill should be used when the user says "lint the wiki", "check the wiki", "wiki health check",
  "find contradictions", or "clean up the brain". Runs a maintenance pass over brain/wiki/, fixes
  mechanical issues, and reports everything that needs human judgement. Manual only, never scheduled.
---

# Lint

Keep the wiki consistent. Fix the mechanical, report the judgemental.

Read `${CLAUDE_PLUGIN_ROOT}/shared/conventions.md` first and run its Bootstrap steps.

## Checks

| Check            | Finds                                                    | Action  |
|------------------|----------------------------------------------------------|---------|
| Broken links     | `[[page]]` with no file                                  | fix     |
| Index drift      | pages missing from or extra in `index.md`                | fix     |
| Missing backlinks| A links B, B not linking A                               | fix     |
| Orphans          | pages with no inbound link                               | report  |
| Contradictions   | conflicting claims across pages, unmarked                | report  |
| Stale claims     | older source contradicted by newer `updated`             | report  |
| Missing pages    | term appearing in ≥2 pages without its own page          | report  |
| Data gaps        | open questions a web search could close                  | report  |
| Not ingested     | files in `requirements/` with no `sources/` page         | report  |
| Drift            | entity without `project_files/` page; `project_files/` page without entity; pinned state behind current | report  |

## Steps

1. Read every file under `wiki/`. Build the link graph (grep `\[\[.*?\]\]`).
2. Run all checks. Apply the `fix` rows directly.
3. Present `report` rows as a numbered list, each with a one-line proposed action.
   Let the user pick which to apply; apply only those.
4. Append a summary to `log.md`: counts fixed, counts reported, counts applied.

## Rules

- Never create, merge, or delete pages without approval. Never touch `requirements/` or project files.
- Keep the report short: one line per finding, grouped by check.
