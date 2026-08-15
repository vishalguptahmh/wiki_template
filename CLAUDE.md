# CLAUDE.md — Personal vault

You are operating inside my Obsidian vault. This file is read every session
and defines how you should behave.

## Zone structure

The vault has three zones with strictly different rules:

### Zone 1 — `raw/` (READ-ONLY)
Sources I curated: clipped articles, paper PDFs, books read,
my daily notes, fleeting thoughts.
- You NEVER edit files in raw/.
- You NEVER rename or move files in raw/.
- You only read, cite, and reference via [[wikilinks]].

### Zone 2 — `wiki/` (LLM-MAINTAINED)
Wiki generated and maintained by you. Concepts, entities, syntheses, indices.
- You own this zone. Create, edit, refactor freely.
- I rarely edit wiki/ by hand. If I ask for change, regenerate carefully.
- Every page in wiki/ MUST have frontmatter with: title, type, tags, sources.
- Every page MUST have at least 1 wikilink to another relevant page.

### Zone 3 — `dev/` (COLLABORATIVE)
Technical notes from my work: ADRs, debriefs, projects, snippets.
- We work together here.
- NEVER edit an existing ADR without explicit confirmation ("can I edit ADR-007?").
- You may SUGGEST rephrasings, find related ADRs, propose wikilinks.

## Wikilink conventions

- ALWAYS use [[wikilinks]] for internal links. NEVER `[text](file.md)`.
- For concepts: [[LLM Wiki Pattern]], [[Optimistic Locking]] (Title Case).
- For entities (people/companies): [[Andrej Karpathy]], [[Anthropic]].
- For projects: [[ECOM-API]], [[Master-Thesis]].
- Tags in frontmatter, comma-separated, kebab-case: `tags: [llm-wiki, knowledge-management]`.

## Frontmatter conventions

Every page you create must have this minimum frontmatter:

​```yaml
---
title: <title>
type: concept | entity | synthesis | adr | debrief | project | reading
tags: [tag1, tag2]
sources:
  - "[[raw/clippings/example]]"
created: 2026-05-01
updated: 2026-05-01
---
​```

For ADRs, add: `status: proposed | accepted | superseded`, `decision-date`.
For debriefs, add: `incident-date`, `severity`.

## Ingestion workflow (when I request /wiki-ingest)

1. Identify the source. If URL, use the `defuddle` skill to extract clean content.
2. Save raw content to `raw/clippings/YYYY-MM-DD-slug.md` with frontmatter
   including original URL and capture date.
3. Identify 3-7 key concepts and 1-3 entities.
4. For each new concept: create page in `wiki/concepts/Concept.md`.
5. For each existing concept: update the page with new source in "Sources" section
   and new nuance in "Notes" section. NEVER rewrite the entire page.
6. Create/update bidirectional wikilinks between the clipping and the concepts.
7. Update `wiki/index.md` if something is genuinely new.
8. Append an entry to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <title>`, listing raw source, concepts/entities created or updated, and whether the index changed.
9. Report what was done as a list — concepts created/updated, links added.

## Lint workflow (when I request /wiki-lint)

Health-check the wiki without editing anything unless I confirm the fixes:

1. Scan `wiki/` for: orphan pages (no inbound `[[wikilinks]]`), contradictions between pages, stale claims superseded by newer sources, concepts mentioned repeatedly but lacking their own page, missing frontmatter fields.
2. Cross-check `wiki/index.md` against the actual files in `wiki/` — flag anything indexed-but-missing or existing-but-unindexed.
3. Present findings as a list grouped by issue type. Do not fix automatically — propose fixes and wait for confirmation (same >5-file rule applies).
4. If I confirm, apply fixes and append a `## [YYYY-MM-DD] lint | <summary>` entry to `wiki/log.md`.

## Strict limits

- NEVER delete files without explicit confirmation.
- NEVER run `git add`, `git commit`, or `git push`. I handle all version control manually.
- You may SUGGEST a commit message when a logical unit of work is done, but don't execute it.
- NEVER edit CLAUDE.md itself (ask me).
- If an operation affects more than 5 files, SHOW the plan before executing.
- If unsure which zone a file belongs to, ASK.

## Available skills

Skills loaded in `.claude/skills/`:
- `obsidian-markdown` — Obsidian native syntax (ALWAYS use)
- `obsidian-bases` — databases via .base
- `json-canvas` — visual whiteboards
- `obsidian-cli` — automation via obsdmd command
- `defuddle` — clean web content extraction

Before creating `.canvas` or `.base` files, consult the corresponding skill.
Before fetching a URL, consult `defuddle`.