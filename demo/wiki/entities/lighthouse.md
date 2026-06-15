---
title: "Lighthouse (BI / Dashboards)"
type: entity
entity_kind: product
tags: [system, bi, dashboards, analytics, lighthouse]
source_count: 5
---

## Overview

Lighthouse is Best Bank's business intelligence and dashboard layer, launched in 2022. It sits on top of Reservoir (`marts`) and provides self-serve reporting to Finance, Product, Risk, and Operations. It uses a Looker-style semantic layer.

## Key facts

- **Launched:** 2022 (alongside Compass)
- **Owner:** Raj Patel (Data Engineering); consumers include Finance, Product, Risk, and Marketing
- Semantic layer reads from Reservoir `marts` only — no direct Vault access
- If the nightly dbt build misses its 05:00 ET SLA, dashboards display a "data delayed" banner and FP&A is notified before market open
- Tracks CD/Savings rates set by Treasury (Priya Raman)
- Tracks Best Credit adoption rates, outstanding balances, and loss rates (Product + Finance + Risk)
- Before Conduit, Lighthouse dashboards could disagree depending on data source; Conduit unified this

## Sources

- [[wiki/sources/company-history|Company History]] — launched 2022
- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — serving layer architecture
- [[wiki/sources/service-best-savings|Best Savings Docs]] — rate tracking
- [[wiki/sources/service-best-credit|Best Credit Docs]] — adoption/loss-rate dashboards
- [[wiki/sources/financial-projections|Financial Projections]] — self-serve FP&A dashboards as efficiency driver

## Related entities

- [[wiki/entities/reservoir|Reservoir]] — reads `marts` from here
- [[wiki/entities/conduit|Conduit]] — upstream pipeline that populates Reservoir
- [[wiki/entities/compass|Compass]] — parallel operational tool; Lighthouse is analytics, Compass is CRM

## Related concepts

- [[wiki/concepts/data-architecture|Data Architecture]]
