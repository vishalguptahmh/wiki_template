---
title: Wiki Ingest-Query-Lint Workflow
type: concept
tags: [llm-wiki, knowledge-management, workflow]
sources:
  - "[[raw/clippings/2026-08-16-llm-wiki-gist-karpathy]]"
created: 2026-08-16
updated: 2026-08-16
---

The three maintenance operations that keep an [[LLM Wiki Pattern]] wiki current, as described by [[Andrej Karpathy]].

## Operations

- **Ingest** — drop a new source into raw, have the LLM read it, extract key points, write/update wiki pages, and update the index and log. A single source may touch 10-15 pages.
- **Query** — ask questions against the wiki; the LLM searches pages (via the index) and synthesizes a cited answer. Good answers can themselves be filed back into the wiki as new pages so explorations compound.
- **Lint** — periodic health check for contradictions between pages, stale claims, orphan pages, missing concept pages, and missing cross-references.

## Supporting files

- **index.md** — content-oriented catalog of every wiki page with a one-line summary; read first when answering a query, before drilling into individual pages. Works well up to ~100 sources / hundreds of pages without needing embedding-based search.
- **log.md** — append-only chronological record of ingests/queries/lints, with a consistent entry prefix (e.g. `## [YYYY-MM-DD] ingest | Title`) so it stays greppable.

## Notes

- This vault's `CLAUDE.md` implements "Ingest" as the `/wiki-ingest` workflow: identify source → save raw clipping → identify concepts/entities → create/update wiki pages → update index → report as a list.
- This vault does not yet have a `log.md` or a documented "Lint" workflow — a gap worth raising if the wiki grows past a handful of sources.
