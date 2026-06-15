---
title: "Three-Layer Wiki Architecture"
type: concept
tags: [knowledge-management, llm, architecture]
source_count: 1
---

## Definition

The structural design of an LLM Wiki system, consisting of three distinct layers with different ownership and mutability rules.

## How it works

**Layer 1 — Raw sources** (`raw/`)
- Your curated source documents: articles, papers, transcripts, images
- **Immutable** — the LLM reads from these but never modifies them
- Source of truth; everything in the wiki is ultimately traceable here

**Layer 2 — The wiki** (`wiki/`)
- LLM-generated and LLM-maintained markdown files
- Summaries, entity pages, concept pages, comparisons, synthesis, overview
- **LLM owns this layer entirely** — creates pages, updates them, maintains cross-references
- You read it; the LLM writes it

**Layer 3 — The schema** (`CLAUDE.md`)
- The configuration document that tells the LLM how the wiki is structured, what conventions to follow, and what workflows to execute
- **Co-owned** — you and the LLM evolve it together as you discover what works
- Without this layer the LLM is a generic chatbot, not a disciplined wiki maintainer

## Evidence

- [[wiki/sources/llm-wiki|LLM Wiki]] — defines this architecture

## Related concepts

- [[wiki/concepts/incremental-wiki|Incremental Wiki Building]] — the pattern this architecture enables
- [[wiki/concepts/wiki-operations|Wiki Operations]] — the workflows that operate across layers
