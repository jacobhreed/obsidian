---
title: "Data Architecture (Vault → Conduit → Reservoir → Lighthouse)"
type: concept
tags: [engineering, data, architecture, systems]
source_count: 5
---

## Definition

Best Bank's data stack is a four-layer pipeline: operational systems (Vault, Compass, Sentinel, App telemetry) → Conduit (ETL pipeline) → Reservoir (Snowflake warehouse) → Lighthouse (BI/dashboards). Conduit is the governed, single-source layer that ended the era of ad-hoc database queries.

## How it works

```
OPERATIONAL SYSTEMS          PIPELINE          WAREHOUSE           SERVING
┌────────────────┐
│ Vault (ledger) │──CDC──────┐
│ Compass (CRM)  │──API──────┤            ┌──────────────┐    ┌──────────────┐
│ Sentinel (risk)│──events───► Conduit    ├──► Reservoir ├───► Lighthouse   │
│ App telemetry  │──events───┤ (Airflow + │    (Snowflake│    │ (BI/dashb.)  │
└────────────────┘           │  Kafka +   │    dbt marts)│    └──────────────┘
                             │  dbt)      └──────────────┘    ┌──────────────┐
                             └────────────────────────────────► Finance/Risk  │
                                                              │  extracts     │
                                                              └──────────────┘
```

### Layer descriptions

| Layer | System | Technology | Cadence | Owner |
|-------|--------|-----------|---------|-------|
| Source: Ledger | Vault | Debezium CDC → Kafka | Near-real-time | Kevin Mbeki |
| Source: CRM | Compass | REST API pull | Hourly | Olivia Grant |
| Source: Risk | Sentinel | Kafka event stream | Real-time | Tomás Herrera |
| Pipeline | Conduit | Airflow + Kafka + dbt | Streaming + nightly batch | Raj Patel |
| Warehouse | Reservoir | Snowflake | Layers: raw → staging → marts | Raj Patel |
| Serving | Lighthouse | Looker-style semantic layer | On Reservoir `marts` | Raj Patel |

### Reservoir mart layer

| Mart | Grain | Consumers |
|------|-------|-----------|
| `mart_accounts` | 1 row/account | Finance, Product; → `accounts_summary.csv` |
| `mart_transactions` | 1 row/posted txn | Risk, Finance |
| `mart_customer_360` | 1 row/customer | Compass, Marketing |
| `mart_revenue_daily` | day × stream | FP&A → projections; → `monthly_revenue_2025.csv` |
| `mart_fraud_signals` | account × event | Sentinel feature store, Credit Risk (underwriting) |

## Why this matters

- Before Conduit (pre-Q3 2025), teams ran ad-hoc scripts on Vault's production DB — data inconsistency and load on production were chronic problems
- Conduit is named as a driver of operating efficiency in the financial projections — it reduces cost-to-serve and is expected to help the efficiency ratio drop from 62% (2025) to 56% (2028)
- PII is tokenized at ingestion; Reservoir never stores unmasked SSN/PAN — a compliance requirement enforced by the pipeline itself
- Lighthouse's "data delayed" banner triggers automatically if the 05:00 ET SLA is missed — FP&A gets warned before market open

## Evidence

- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — full technical reference
- [[wiki/sources/company-history|Company History]] — timeline of stack evolution (Vault 2014, Compass/Lighthouse 2022, Conduit 2025)
- [[wiki/sources/financial-projections|Financial Projections]] — data stack as operating leverage driver
- [[wiki/sources/accounts-summary|Accounts Summary]] — `mart_accounts` export
- [[wiki/sources/monthly-revenue-2025|Monthly Revenue 2025]] — `mart_revenue_daily` export

## Related entities

- [[wiki/entities/vault|Vault]]
- [[wiki/entities/conduit|Conduit]]
- [[wiki/entities/reservoir|Reservoir]]
- [[wiki/entities/lighthouse|Lighthouse]]
- [[wiki/entities/compass|Compass]]
- [[wiki/entities/sentinel|Sentinel]]
