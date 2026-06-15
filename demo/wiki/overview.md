---
title: "Best Bank Wiki — Overview"
type: special
---

## What this wiki is about

Best Bank, N.A. — a digital-first regional bank founded in Charlotte, NC in 2011. This wiki covers the company's history, products, technology, people, financials, and operations. Sources include internal documentation, product specs, newsletters, and data exports.

## Core thesis

Best Bank is executing a deliberate three-stage strategy: acquire customers through a no-friction checking account, deepen the relationship with savings, and extend into credit. The Q1 2026 Best Credit launch is the pivotal moment — it changes the revenue mix from NII-dominant to a more balanced NII + interchange + revolving interest model, and the 2026–2028 projections assume it drives 18%+ annual revenue growth.

The data stack (Vault → Conduit → Reservoir → Lighthouse) is the operational backbone that makes this scalable. Conduit's GA in Q3 2025 ended chronic data inconsistency and is now expected to contribute to a declining efficiency ratio (62% → 56% by 2028).

## Key concepts

- [[wiki/concepts/product-funnel|Product Funnel]] — Checking → Savings → Credit is the core strategy; each stage builds on the last
- [[wiki/concepts/revenue-model|Revenue Model]] — NII-dominated today; Best Credit shifts the mix toward interchange and revolving interest
- [[wiki/concepts/data-architecture|Data Architecture]] — Vault→Conduit→Reservoir→Lighthouse; the single source of truth since Q3 2025
- [[wiki/concepts/culture-values|Culture & Values]] — "Clarity over cleverness / Trust is the balance sheet / Small bank feel, big bank reliability"

## Key entities

**Products**
- [[wiki/entities/best-checking|Best Checking]] — 520K accounts, $2.2B; founding product and acquisition funnel entry
- [[wiki/entities/best-savings|Best Savings]] — 280K accounts, $2.0B; NIM engine
- [[wiki/entities/best-credit|Best Credit]] — launched Q1 2026; primary growth lever through 2028

**Systems**
- [[wiki/entities/vault|Vault]] — core banking ledger (2014); source of truth for all accounts
- [[wiki/entities/conduit|Conduit]] — data pipeline (GA Q3 2025); unifies all data flows
- [[wiki/entities/sentinel|Sentinel]] — risk/fraud engine; also provides underwriting features for Best Credit
- [[wiki/entities/compass|Compass]] — CRM / Customer-360 (2022)
- [[wiki/entities/reservoir|Reservoir]] — Snowflake analytics warehouse
- [[wiki/entities/lighthouse|Lighthouse]] — BI dashboards (2022)

**People**
- [[wiki/entities/eleanor-vance|Eleanor Vance]] — Founder & CEO; the culture and founding story
- [[wiki/entities/leadership-team|Leadership Team]] — full ELT and key team leads

**Other**
- [[wiki/entities/branch-network|Branch Network]] — 14 locations across Southeast; 2 consolidating in 2026
- [[wiki/entities/commercial-clients|Commercial Clients]] — 15 named business clients, 4 RMs

## Open questions

- Will Best Credit's 12% checking-customer adoption rate materialize? Early conversion data (Q2–Q3 2026) will be the first real signal
- How much rate sensitivity does the deposit base have? The plan assumes Fed funds stays within 50bps of current; a significant cut would compress NIM materially
- Are the Buckhead and Columbia branch consolidations the start of a broader rationalization, or a one-time adjustment?
- When does the `index.md` approach break down and require a search engine (qmd or similar)?

## Recent developments

- **2026-Q1:** Best Credit launched. Branch consolidations (Buckhead, Columbia) confirmed
- **2025-Q3:** Conduit went GA; Sentinel became a core production consumer
- **2025:** Record year — $236M revenue, $47.2M net income, $4.2B deposits
- **2026-06-15:** Initial wiki build — all 15 founding sources ingested
