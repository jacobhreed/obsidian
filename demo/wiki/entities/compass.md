---
title: "Compass (CRM / Customer-360)"
type: entity
entity_kind: product
tags: [system, crm, product, customer]
source_count: 4
---

## Overview

Compass is Best Bank's CRM system, launched in 2022 (alongside Lighthouse). It provides a Customer-360 view — every customer's full relationship: checking, savings, credit, and interaction history — used by Customer Support and Sales.

## Key facts

- **Launched:** 2022
- **Owner:** CPO Lisa Tran; PM Olivia Grant (Platform & Data Products)
- Data source: pulls from Reservoir via Conduit (`mart_customer_360` mart)
- Compass is fed by Conduit (hourly REST API pull); Vault account data flows in via Conduit
- Customer-360 links a customer's savings goals, checking activity, and (since 2026) Best Credit relationship
- Used by: Customer Support (call centers in Charlotte and Atlanta hubs), RMs for commercial clients, Sales

## Sources

- [[wiki/sources/company-history|Company History]] — launched 2022
- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — Compass as a Conduit source (hourly REST API)
- [[wiki/sources/service-best-checking|Best Checking Docs]] — Compass for Customer-360
- [[wiki/sources/service-best-savings|Best Savings Docs]] — savings goals visible in Compass

## Related entities

- [[wiki/entities/conduit|Conduit]] — Compass both feeds Conduit (CRM data) and consumes it (customer 360)
- [[wiki/entities/reservoir|Reservoir]] — `mart_customer_360` is the source for Compass enrichment
- [[wiki/entities/lighthouse|Lighthouse]] — parallel BI tool; Compass is for operations, Lighthouse for analytics

## Related concepts

- [[wiki/concepts/data-architecture|Data Architecture]]
