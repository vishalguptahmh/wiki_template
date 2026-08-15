---
title: LLM Wiki Pattern
type: concept
tags: [llm-wiki, knowledge-management, obsidian]
sources:
  - "[[raw/clippings/2026-08-16-llm-wiki-gist-karpathy]]"
created: 2026-08-16
updated: 2026-08-16
---

A pattern for personal knowledge bases where an LLM incrementally builds and maintains a persistent, interlinked wiki, rather than retrieving from raw documents fresh at every query (contrast [[Retrieval-Augmented Generation]]).

## Three layers

- **Raw sources** — curated, immutable source documents (articles, papers, notes). The LLM reads but never edits this layer. In this vault: `raw/`.
- **The wiki** — LLM-generated markdown: summaries, entity pages, concept pages, syntheses. The LLM owns this layer entirely and keeps it cross-referenced and current. In this vault: `wiki/`.
- **The schema** — a config document (e.g. `CLAUDE.md` or `AGENTS.md`) defining structure, conventions, and workflows the LLM follows. Co-evolved with the user over time.

## Why it differs from RAG

RAG re-derives an answer from scratch on every query by retrieving chunks. This pattern instead treats the wiki as a **compounding artifact**: each new source is read once, integrated into existing pages, and cross-referenced — so later queries read accumulated synthesis rather than re-assembling fragments.

## Operations

See [[Wiki Ingest-Query-Lint Workflow]] for the three maintenance operations (ingest, query, lint) and the role of `index.md`/`log.md` in navigating the growing wiki.

## Precursor

Related in spirit to the [[Memex]], Vannevar Bush's 1945 concept of a personal, curated, associative knowledge store — the pattern this vault implements largely solves the maintenance burden Bush's vision left unsolved.

## Notes

- Originated as a gist by [[Andrej Karpathy]], shared as an "idea file" meant to be adapted per-domain rather than followed as a fixed spec.
- This vault (`knowledgeBaseMine`) is itself a direct implementation of this pattern — `raw/`, `wiki/`, and `CLAUDE.md` map 1:1 onto the three layers described.
