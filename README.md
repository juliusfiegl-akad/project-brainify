# Project Brainify

A Claude plugin that prepares and accompanies a project with a Karpathy-style LLM wiki
(requirements + project files → LLM-maintained wiki → schema in CLAUDE.md). Obsidian-compatible.

## Skills

| Skill | Does |
|-------|------|
| `/project-brainify:interview` | Interviews you about your idea (software or not) or an addition to a running project; writes an approved `brain/requirements/requirement_<name>.md` |
| `/project-brainify:wiki` | `ingest`: one requirements file → linked entity/concept pages. `sync`: changed project files → `project_files/` pages linked to the entities they implement |
| `/project-brainify:query` | Answers questions from the wiki with citations; files new insights back on request |
| `/project-brainify:lint` | Health check: fixes broken links and index drift, reports contradictions, orphans, gaps, plan/implementation drift |

## Layout created in your project

```
CLAUDE.md            # gets a "## Project Brain" section
brain/
  requirements/      # your sources, never edited by Claude
  wiki/
    index.md  log.md
    sources/  project_files/  entities/  concepts/  answers/
<everything else>    # project files: read by sync, never written
```

Existing structures and CLAUDE.md files are adopted, not overwritten. Every write asks first.

## Install

**claude.ai / Cowork / Desktop** (also syncs into Claude Code):
Customize → Plugins → Add → Add marketplace → enter `juliusfiegl-akad/project-brainify`, then add the plugin.

**Claude Code (CLI):**
```
/plugin marketplace add juliusfiegl-akad/project-brainify
/plugin install project-brainify@project-brainify
```

**Local test:** `claude --plugin-dir ./project-brainify`
