---
title: "RAG vs. Persistent Wiki"
type: concept
tags: [knowledge-management, llm, rag, methodology]
source_count: 1
---

## Definition

The contrast between two approaches to LLM-powered knowledge retrieval: **Retrieval-Augmented Generation (RAG)**, which re-derives answers from raw documents at query time, and a **Persistent Wiki**, which compiles and maintains synthesized knowledge incrementally.

## How it works

| Dimension | RAG | Persistent Wiki |
|---|---|---|
| When synthesis happens | Every query | Once at ingest, updated on each new source |
| What accumulates | Nothing (raw docs only) | Cross-references, summaries, contradiction flags |
| Multi-document synthesis | Fragile (must retrieve right chunks) | Pre-built into wiki pages |
| Infrastructure needed | Embedding store, retrieval pipeline | Markdown files + schema + LLM |
| Human effort | Low to set up, passive after | Active curation and direction |

## Evidence

- [[wiki/sources/llm-wiki|LLM Wiki]] — primary source for this comparison

## Counterarguments / limitations

- RAG scales more easily to very large corpora (millions of documents)
- A persistent wiki requires ongoing LLM involvement to stay healthy — it can go stale if you stop maintaining it
- The two approaches aren't mutually exclusive — a wiki with a search engine (qmd) hybridizes both

## Related concepts

- [[wiki/concepts/incremental-wiki|Incremental Wiki Building]] — the alternative to RAG described here
- [[wiki/concepts/three-layer-architecture|Three-Layer Wiki Architecture]]
