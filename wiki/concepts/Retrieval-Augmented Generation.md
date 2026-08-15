---
title: Retrieval-Augmented Generation
type: concept
tags: [llm-wiki, rag, knowledge-management]
sources:
  - "[[raw/clippings/2026-08-16-llm-wiki-gist-karpathy]]"
created: 2026-08-16
updated: 2026-08-16
---

The dominant pattern for LLM-plus-documents systems: a collection of files is indexed, and at query time relevant chunks are retrieved and fed to the LLM to generate an answer. Used by NotebookLM, ChatGPT file uploads, and most document-QA systems.

## Limitation motivating the [[LLM Wiki Pattern]]

RAG re-discovers knowledge from scratch on every question — nothing accumulates between queries. A question that requires synthesizing five documents forces the system to re-find and re-piece-together the same fragments every time it's asked. The [[LLM Wiki Pattern]] was proposed by [[Andrej Karpathy]] as an alternative: compile knowledge into a persistent, cross-referenced wiki once, then keep it current, rather than re-deriving synthesis per query.

## Notes

- This vault deliberately avoids RAG infrastructure at its current scale, relying instead on `wiki/index.md` as a navigable catalog — see [[Wiki Ingest-Query-Lint Workflow]].
