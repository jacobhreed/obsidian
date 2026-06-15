---
title: "Reservoir (Analytics Warehouse)"
type: entity
entity_kind: product
tags: [system, data, warehouse, reservoir, snowflake]
source_count: 5
---

## Overview

Reservoir is Best Bank's analytics data warehouse (built on Snowflake). It is the destination for all Conduit-processed data and the source for Lighthouse dashboards, Finance extracts, and Sentinel underwriting features.

## Key facts

- **Platform:** Snowflake
- **Owner:** Raj Patel (Data Engineering)
- **Three layers:** `raw` (immutable, 90-day retention) → `staging` (cleaned, typed, deduped) → `marts` (business-conformed)
- **Core marts:** `mart_accounts`, `mart_transactions`, `mart_customer_360`, `mart_revenue_daily`, `mart_fraud_signals`
- PII is tokenized at ingestion — Reservoir stores only masked values; unmasked access requires Compliance (Robert Ellis)
- `mart_accounts` → nightly export to `accounts_summary.csv`
- `mart_revenue_daily` → backs `monthly_revenue_2025.csv` and FP&A projections
- dbt manages all transformations; column-level lineage traces every mart back to source tables

## Sources

- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — full architecture and mart definitions
- [[wiki/sources/accounts-summary|Accounts Summary]] — `mart_accounts` export
- [[wiki/sources/monthly-revenue-2025|Monthly Revenue 2025]] — `mart_revenue_daily` export
- [[wiki/sources/financial-projections|Financial Projections]] — downstream consumer
- [[wiki/sources/service-best-credit|Best Credit Docs]] — deposit history used in underwriting

## Related entities

- [[wiki/entities/conduit|Conduit]] — writes to Reservoir
- [[wiki/entities/lighthouse|Lighthouse]] — reads from Reservoir `marts`
- [[wiki/entities/sentinel|Sentinel]] — reads `mart_fraud_signals` for underwriting

## Related concepts

- [[wiki/concepts/data-architecture|Data Architecture]]
