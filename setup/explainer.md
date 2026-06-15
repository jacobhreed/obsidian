# LLM Wiki with Obsidian — Explainer

## What is Obsidian?

Obsidian is a desktop note-taking application that stores all notes as plain markdown files on your local machine. There is no proprietary format, no cloud lock-in — your vault is just a folder of `.md` files that you own.

A few features make it particularly well-suited as the IDE for an LLM-maintained wiki:

- **Wiki-links.** `[[page-name]]` creates a clickable link between notes. Obsidian resolves these automatically, letting you navigate a dense web of cross-references without managing URLs or relative paths.
- **Graph view.** A live force-directed graph shows every page and every link between them. As the wiki grows, hubs (heavily-linked pages like `conduit.md`) emerge visually; orphans (unlinked pages) stand out as isolated nodes. It is the best way to see the shape of the knowledge base at a glance.
- **Backlinks panel.** Every page shows a sidebar listing every other page that links to it — so you can navigate upstream ("what references Sentinel?") as easily as downstream.
- **Dataview plugin.** Queries the YAML frontmatter of every page and generates dynamic tables. If the LLM keeps `source_count` fields current, Dataview can render a live table of all concept pages sorted by source count.
- **Local-first, git-friendly.** Because the vault is just files, you get version history, branching, and collaboration through ordinary git — no special sync infrastructure required.

In practice: the LLM has the vault open in its working directory and edits files directly. You have Obsidian open on the same folder. The LLM writes; you browse the results in real time.

---

## How `llm-wiki.md` and `CLAUDE.md` interact

These two files operate at different levels of abstraction and serve different audiences.

### `llm-wiki.md` — The pattern

`llm-wiki.md` is an **idea document**. It describes the LLM Wiki pattern in the abstract: the core insight (compile knowledge incrementally rather than re-derive it at query time), the three-layer architecture (raw sources / wiki / schema), the three operations (ingest / query / lint), and the role of `index.md` and `log.md`. It is intentionally domain-agnostic — it says nothing about Best Bank, nothing about folder names, nothing about frontmatter fields.

Its job is to communicate the pattern to a human (or an LLM starting a new project) so they understand *why* the system is structured the way it is. It is the spec; it is not the implementation.

### `CLAUDE.md` — The implementation

`CLAUDE.md` is the **schema** — the concrete, opinionated instantiation of the pattern for this specific vault. It tells the LLM:

- Exactly what the folder structure is and what goes where
- The precise frontmatter fields for each page type (source, concept, entity)
- Step-by-step workflows for each operation (ingest, query, lint)
- The format rules for `index.md` and `log.md`
- Linking conventions (`[[wiki/concepts/slug|Display Name]]`)
- What the LLM is never allowed to do (modify `raw/`, invent citations, delete without checking inbound links)

`CLAUDE.md` is loaded into the LLM's context at the start of every session. It is what transforms a general-purpose LLM into a disciplined wiki maintainer with consistent behavior across sessions.

### How they work together

```
llm-wiki.md          CLAUDE.md               Wiki files
(the pattern)   →    (the schema)       →    (the output)
"here's why"         "here's how,            Maintained by the
                      exactly, for            LLM following the
                      this vault"             rules in CLAUDE.md
```

`llm-wiki.md` is written once and shared. `CLAUDE.md` is evolved collaboratively — as you discover what works (better page formats, new section types, refined workflows), you update the schema. The schema is the place where operational learning accumulates. `llm-wiki.md` never changes because the pattern doesn't change; `CLAUDE.md` grows with the project.

---

## LLM Wiki vs. Traditional RAG

### What RAG does

Retrieval-Augmented Generation (RAG) is the standard approach for "chat with your documents." The pipeline:

1. Documents are chunked into small passages and embedded into a vector store
2. At query time, the user's question is embedded and the nearest-neighbor chunks are retrieved
3. The retrieved chunks are stuffed into the LLM's context window alongside the question
4. The LLM generates an answer grounded in those chunks

Systems like NotebookLM, ChatGPT file uploads, and most enterprise "knowledge base" products work this way.

### The key difference

| Dimension | RAG | LLM Wiki |
|-----------|-----|----------|
| **When synthesis happens** | Every query, from scratch | Once at ingest; updated incrementally |
| **What accumulates** | Nothing — raw chunks only | Cross-references, summaries, contradiction flags, synthesis |
| **Multi-document reasoning** | Fragile — depends on retrieving the right chunks | Pre-built into wiki pages |
| **Contradiction detection** | Not handled | Explicit step in the ingest workflow |
| **Infrastructure** | Embedding model, vector store, retrieval pipeline | Markdown files + schema + LLM |
| **Latency per query** | Low (retrieve + generate) | Low (read index + read pages + generate) |
| **Scales to** | Millions of documents | Hundreds of sources before index gets unwieldy |
| **Human role** | Passive (upload and ask) | Active (curate, direct, guide emphasis) |
| **Output permanence** | Answers disappear into chat history | Answers can be filed back as wiki pages |

### Where RAG wins

- **Scale.** A vector store handles millions of documents; an `index.md` file does not. If your source corpus is large and you don't need deep synthesis, RAG is simpler and more scalable.
- **Setup cost.** Drop files in, embed, done. No schema to design, no wiki structure to maintain.
- **Latency.** RAG retrieves a handful of chunks and generates immediately. The LLM Wiki approach requires reading the index, potentially reading several wiki pages, then synthesizing — more round trips.
- **Passive ingestion.** If you want to ingest documents without thinking about them, RAG handles that automatically. The LLM Wiki assumes you're involved in each ingest.

### Where LLM Wiki wins

- **Compounding value.** Each new source makes the whole wiki richer — not just by adding one more document, but by updating cross-references, revising definitions, and flagging contradictions. RAG doesn't compound; it just accumulates.
- **Pre-built synthesis.** A wiki page on "revenue model" already synthesizes five sources. A RAG system retrieves chunks from those five sources separately and re-synthesizes on every question. The wiki answer is faster and more consistent.
- **Contradiction handling.** If two sources disagree, a wiki's ingest workflow surfaces that explicitly. RAG will happily retrieve both contradicting chunks and let the LLM figure it out mid-answer — inconsistently.
- **Exploration compounds.** When you ask a good question in a RAG system, the answer lives in the chat window and is gone. In an LLM Wiki, substantial query answers can be filed as new pages. Your analysis becomes part of the base.
- **Legibility.** The wiki is human-readable. You can browse it in Obsidian, follow links, check the graph view, read pages directly. A vector store is opaque — you can't browse embeddings.
- **No infrastructure.** No embedding pipeline, no vector database to host, no retrieval service to maintain. It's markdown files in a git repo.

### The honest trade-off

RAG is better for broad, passive, large-scale retrieval. The LLM Wiki is better for deep, active, compounding knowledge work — the kind where you're reading carefully over weeks or months and want the understanding to accumulate rather than reset on every query.

They are not mutually exclusive. A mature LLM Wiki can add a search tool (like [qmd](https://github.com/tobi/qmd)) that does hybrid BM25/vector search over the wiki pages themselves — at which point you get the compounding benefit of the wiki *and* the retrieval efficiency of RAG, with your own synthesized pages as the corpus instead of raw documents.
