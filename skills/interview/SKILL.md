---
name: interview
description: >
  This skill should be used when the user wants to start a new project, "interview me about my idea",
  "gather requirements", "set up the project brain", or wants to add something to an existing project
  ("add a requirement", "we need a new feature", "interview me about X"). Works for software and
  non-software projects. Produces one brain/requirements/requirement_<name>.md per interview after user approval.
---

# Interview

Turn a rough idea — a whole project or a single addition — into an approved requirements file in `brain/requirements/`.

Read `${CLAUDE_PLUGIN_ROOT}/shared/conventions.md` first and run its Bootstrap steps.

## Modes

| Mode     | When                                      | File                            |
|----------|-------------------------------------------|---------------------------------|
| initial  | no `requirement_*.md` in `brain/requirements/` | `requirement_<project_slug>.md` |
| addition | brain exists, user wants something new    | `requirement_<topic_slug>.md`   |

Name = `requirement_` + 2–4 snake_case words naming the thing, never a date or number
(`requirement_crm_tool`, `requirement_testing_framework`). Propose the name, let the user confirm.
Never overwrite; if taken, append `_v2`.

## Steps

1. Ask for the idea in one sentence. Decide mode and software / non-software.
2. addition only: read `wiki/index.md` and the pages the addition touches. Ask only about the delta
   and name the affected entities and concepts explicitly.
3. Interview in rounds, max 3 questions per round (use AskUserQuestion when available). Cover, in order:
   goal → users & stakeholders → scope and non-goals → constraints (time, budget, tech, legal) →
   structure (software: frontend, pages, backend, tables, functions, integrations;
   non-software: phases, roles, deliverables, resources) → risks → success criteria.
   Skip what the user already answered or the wiki already covers. Stop when every area has an answer
   or the user says it is enough.
4. Draft from `${CLAUDE_PLUGIN_ROOT}/shared/templates/requirements.md`
   (addition: fill `## Affects`, drop empty sections). Show it in full.
5. Ask for approval. Revise until approved. Only then write the file.
6. Append to `brain/wiki/log.md`. Suggest `/project-brainify:wiki` as next step.

## Rules

- One question at a time where answers depend on each other; otherwise batch up to 3.
- Record "unknown / to decide" explicitly — it is valuable data for the wiki.
- Never write to requirements without the user's explicit approval of the final text.
