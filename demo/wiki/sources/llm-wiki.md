---
title: "LLM Wiki"
type: source
date_ingested: "2026-06-15"
source_file: "llm-wiki.md"
tags: [knowledge-management, llm, wiki, methodology]
---

## Summary

The LLM Wiki pattern replaces retrieval-augmented generation (RAG) with a persistent, incrementally maintained wiki. Instead of re-deriving knowledge at query time from raw documents, an LLM reads new sources and integrates them into an evolving collection of interlinked markdown pages — updating entity pages, revising concept summaries, and flagging contradictions. The wiki compounds with every source added and every question asked.

## Key points

- RAG re-discovers knowledge from scratch on every query; an LLM Wiki compiles it once and keeps it current
- The wiki is a **persistent, compounding artifact** — cross-references and synthesis are already there when you ask a question
- The human curates sources and asks questions; the LLM does all the bookkeeping (cross-referencing, filing, updating)
- Three layers: raw sources (immutable), wiki (LLM-written markdown), schema (CLAUDE.md)
- Three operations: **ingest** (add a source), **query** (ask against the wiki), **lint** (health-check for stale claims, orphans, gaps)
- `index.md` (content catalog) + `log.md` (chronological record) are the two navigation aids
- Good query answers can be filed back into the wiki as new pages — explorations compound too
- Works for personal tracking, research, reading books, team wikis, competitive analysis, and more

## Concepts introduced

- [[wiki/concepts/incremental-wiki|Incremental Wiki Building]]
- [[wiki/concepts/rag-vs-wiki|RAG vs. Persistent Wiki]]
- [[wiki/concepts/three-layer-architecture|Three-Layer Wiki Architecture]]
- [[wiki/concepts/wiki-operations|Wiki Operations (Ingest / Query / Lint)]]

## Entities mentioned

- [[wiki/entities/vannevar-bush|Vannevar Bush]] — cited as intellectual ancestor (Memex, 1945)
- [[wiki/entities/obsidian|Obsidian]] — recommended IDE for browsing the wiki
- [[wiki/entities/qmd|qmd]] — optional CLI/MCP search engine for larger wikis

## Open questions

- At what scale does `index.md` break down and require a proper search engine?
- What's the right human-in-the-loop ratio for batch vs. one-at-a-time ingestion?
- How do you handle sources in formats other than markdown (PDFs, audio transcripts, images)?
