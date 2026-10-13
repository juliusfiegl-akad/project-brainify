---
name: query
description: >
  This skill should be used when the user asks a question about the project ("what does the wiki say
  about X", "how are A and B connected", "ask the brain", "query the wiki") or wants an answer grounded
  in brain/wiki/ with citations. May enrich the wiki with new links or researched facts on request.
---

# Query

Answer from the wiki, cite pages, and file valuable answers back.

Read `${CLAUDE_PLUGIN_ROOT}/shared/conventions.md` first and run its Bootstrap steps.

## Steps

1. Read `wiki/index.md`. Pick candidate pages, read them, follow `[[links]]` as needed.
   Go to `brain/requirements/`, then the project files, only if the wiki is insufficient.
2. If the wiki still cannot answer: say so. Offer web research (WebSearch). Only research after a yes.
3. Answer concisely. Cite with `[[page]]` after each claim. Mark researched facts with their URL.
4. If the answer contains new synthesis — a connection between pages, a researched fact, a
   comparison — ask once: "File this into the wiki?" On yes:
   - new connection → add `## Related` links on both pages;
   - new fact → update the relevant page, add the URL to `sources`;
   - standalone synthesis → `wiki/answers/<slug>.md` with `type: answer`.
   Update `index.md`, append to `log.md`.

## Rules

- No silent writes. Every wiki change follows an explicit yes.
- Wiki beats requirements beats project files beats web: cite the highest-trust layer that answers.
- Do not restate the whole wiki; answer the question.
