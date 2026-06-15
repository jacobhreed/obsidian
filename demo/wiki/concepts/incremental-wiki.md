---
title: "Incremental Wiki Building"
type: concept
tags: [knowledge-management, llm, methodology]
source_count: 1
---

## Definition

A knowledge-management pattern in which an LLM incrementally builds and maintains a persistent wiki by reading new sources and integrating them — rather than re-deriving knowledge from raw documents at query time (as in RAG).

## How it works

When a new source arrives, the LLM:
1. Reads the source
2. Creates a summary page
3. Updates existing concept and entity pages with new evidence, revised definitions, or contradictions
4. Updates the index and log

Over time the wiki accumulates synthesis, cross-references, and contradiction flags that no single source contains. Each new source makes the whole more valuable, not just adds another document to a pile.

## Evidence

- [[wiki/sources/llm-wiki|LLM Wiki]] — the originating document for this pattern

## Counterarguments / limitations

- Requires a capable LLM to maintain cross-references accurately at scale
- Schema discipline (this CLAUDE.md) is load-bearing — without it the LLM drifts
- At very high source counts, the index file may be too large to read efficiently (mitigated by a search tool like qmd)

## Related concepts

- [[wiki/concepts/rag-vs-wiki|RAG vs. Persistent Wiki]] — the contrast that motivates this pattern
- [[wiki/concepts/three-layer-architecture|Three-Layer Wiki Architecture]] — how the system is structured
- [[wiki/concepts/wiki-operations|Wiki Operations]] — the workflows that drive accumulation

## Examples

- Filing journal entries + articles about health to build a structured picture of yourself over time
- Reading a book chapter by chapter and building a companion wiki (character pages, theme pages)
- Maintaining a team internal wiki fed by Slack threads and meeting transcripts
