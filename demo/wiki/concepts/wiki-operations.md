---
title: "Wiki Operations (Ingest / Query / Lint)"
type: concept
tags: [knowledge-management, llm, methodology, workflow]
source_count: 1
---

## Definition

The three recurring workflows that drive an LLM Wiki: **Ingest** (add a source), **Query** (ask against the wiki), and **Lint** (health-check and maintain).

## How it works

### Ingest
Triggered by: dropping a new source in `raw/` and telling the LLM to process it.

Flow: read source → discuss with user → write source page → update concept pages → update entity pages → update overview → update index → append to log. A single ingest may touch 10–15 wiki pages.

Two modes:
- **One-at-a-time (recommended)**: stay involved, guide emphasis, check summaries in real time
- **Batch**: less supervision, higher throughput, lower quality control

### Query
Triggered by: asking a question.

Flow: LLM reads `index.md` to find relevant pages → reads those pages → synthesizes answer with citations → offers to file substantial answers as new wiki pages.

Key insight: **good answers can be filed back as wiki pages.** Explorations compound in the knowledge base just like ingested sources do.

### Lint
Triggered by: asking for a "health check" or "lint."

Checks:
- Orphan pages (no inbound links)
- Concept/entity pages with `source_count: 0` (speculative, unfounded)
- Stale claims superseded by newer sources
- Concepts mentioned in passing but lacking their own page
- Data gaps that a web search could fill

Output: a lint report with suggested fixes.

## Evidence

- [[wiki/sources/llm-wiki|LLM Wiki]] — describes all three operations

## Related concepts

- [[wiki/concepts/incremental-wiki|Incremental Wiki Building]] — the accumulation model these operations drive
- [[wiki/concepts/three-layer-architecture|Three-Layer Wiki Architecture]] — structural context
