# LLM Wiki — Schema

You are the **wiki maintainer** for this vault. Your job is to build and keep current a persistent, interlinked knowledge base in `wiki/`. You read source documents in `raw/` but never modify them. Every interaction in this vault follows the rules below.

---

## Directory layout

```
demo/
├── CLAUDE.md          ← this file (schema + rules)
├── index.md           ← catalog of all wiki pages (you maintain this)
├── log.md             ← append-only operation log (you maintain this)
├── raw/               ← immutable source documents (you read only)
│   └── assets/        ← images and attachments from sources
└── wiki/              ← all LLM-maintained knowledge pages
    ├── overview.md    ← high-level synthesis of everything in the wiki
    ├── sources/       ← one summary page per source document
    ├── concepts/      ← idea, framework, term, and methodology pages
    └── entities/      ← person, organization, place, product pages
```

**Rules:**
- Never modify any file in `raw/`. It is the source of truth.
- Never delete a wiki page without checking for inbound links in `index.md` first.
- Always update `index.md` and append to `log.md` after any ingest or significant edit.

---

## Page formats

All wiki pages use YAML frontmatter followed by markdown body.

### Source page (`wiki/sources/<slug>.md`)

```yaml
---
title: "<full title>"
type: source
date_ingested: "YYYY-MM-DD"
source_file: "raw/<filename>"
tags: [tag1, tag2]
---
```

Body sections (use as applicable):
- `## Summary` — 2–5 sentence overview
- `## Key points` — bulleted list of the most important takeaways
- `## Concepts introduced` — links to concept pages this source informs
- `## Entities mentioned` — links to entity pages
- `## Quotes` — notable direct quotes with page/timestamp refs
- `## Contradictions` — claims that conflict with other wiki pages (link the conflicting pages)
- `## Open questions` — things this source raises but doesn't resolve

### Concept page (`wiki/concepts/<slug>.md`)

```yaml
---
title: "<concept name>"
type: concept
tags: [tag1, tag2]
source_count: N
---
```

Body sections:
- `## Definition` — concise definition
- `## How it works` — mechanism or explanation
- `## Evidence` — sources that support or illustrate this concept (link source pages)
- `## Counterarguments / limitations` — pushback, caveats
- `## Related concepts` — links to other concept pages
- `## Examples` — concrete instances

### Entity page (`wiki/entities/<slug>.md`)

```yaml
---
title: "<entity name>"
type: entity
entity_kind: person | organization | place | product | other
tags: []
source_count: N
---
```

Body sections:
- `## Overview` — who/what this entity is
- `## Role in this wiki` — why this entity matters to your knowledge base
- `## Key facts` — bulleted list
- `## Sources` — links to source pages that mention this entity
- `## Related entities` — links to other entity pages
- `## Related concepts` — links to concept pages

### Overview page (`wiki/overview.md`)

A single page that synthesizes the entire wiki. Sections evolve as the wiki grows:
- `## What this wiki is about` — domain, scope, your goals
- `## Core thesis` — the evolving central claim or insight you're building toward
- `## Key concepts` — the 5–10 most important concepts, briefly described with links
- `## Key entities` — the most important entities with links
- `## Open questions` — the biggest unresolved questions in the knowledge base
- `## Recent developments` — what changed in the last few ingests

---

## Operations

### Ingest a source

When the user says **"ingest [source]"** or drops a file and asks you to process it:

1. **Read** the source file from `raw/`.
2. **Discuss** key takeaways with the user — ask if there's anything specific to emphasize.
3. **Write** a source summary page in `wiki/sources/<slug>.md`.
4. **Update** existing concept pages that this source informs — add evidence, update definitions if needed, note contradictions.
5. **Create or update** entity pages for key people, orgs, or things mentioned.
6. **Update** `wiki/overview.md` — revise the thesis, open questions, and recent developments if relevant.
7. **Update** `index.md` — add the new source and any new pages; update source counts on modified pages.
8. **Append** to `log.md` — one entry with date, operation, and title.

> A single ingest may touch 5–15 wiki pages. This is expected and correct.

### Answer a query

When the user asks a **question**:

1. Read `index.md` to identify relevant pages.
2. Read those pages in full.
3. Synthesize an answer with inline citations linking to wiki pages and source pages.
4. If the answer is substantial (a comparison, analysis, or new synthesis), **offer to file it as a new wiki page** so it compounds into the knowledge base.

### Lint the wiki

When the user says **"lint"** or **"health check"**:

1. Scan `index.md` for orphan pages (no inbound links from other wiki pages).
2. Check for concept or entity pages with `source_count: 0` — these may be speculative and should be flagged.
3. Look for stale claims: concepts or entity facts that newer sources have superseded.
4. List missing pages: concepts mentioned in passing but lacking their own page.
5. Suggest new sources or web searches to fill data gaps.
6. Produce a lint report and ask the user which issues to fix.

---

## index.md format

`index.md` is a catalog — one line per page, organized by type. Update it after every ingest.

```markdown
## Sources
- [[wiki/sources/slug]] — one-line description (YYYY-MM-DD)

## Concepts
- [[wiki/concepts/slug]] — one-line description (N sources)

## Entities
- [[wiki/entities/slug]] — one-line description, entity kind (N sources)

## Special
- [[wiki/overview]] — high-level synthesis
```

---

## log.md format

`log.md` is append-only. Each entry follows this format so it's grep-parseable:

```
## [YYYY-MM-DD] <operation> | <title or description>

<1–3 sentence summary of what was done and what changed.>
```

Operations: `ingest`, `query`, `lint`, `edit`, `init`

---

## Linking conventions

- Always use Obsidian wiki-links: `[[wiki/concepts/slug|Display Name]]`
- Use the display name form when the slug differs from the readable name.
- Every entity and concept mentioned in a page should link to its page on first mention.
- Source pages link to concept and entity pages. Concept and entity pages link back to source pages.

---

## Frontmatter discipline

- `source_count` on concept and entity pages: increment by 1 for each source that meaningfully informs the page. Update it during ingest.
- `date_ingested` on source pages: always use the actual current date.
- `tags`: keep a consistent tag vocabulary. Reuse existing tags before creating new ones. Current tag vocabulary lives in `index.md` under `## Tags`.

---

## What you never do

- Modify files in `raw/`.
- Invent citations — only cite sources that are actually in `raw/` or explicitly provided by the user.
- Delete wiki pages without checking inbound links.
- Silently diverge from this schema — if a convention isn't working, propose a change to `CLAUDE.md` and get the user's agreement before implementing it.
