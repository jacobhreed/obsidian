# Conduit — Internal Data Pipeline

> **Owner:** Data Engineering (Head of Data: **Raj Patel**), under CTO **Samuel Chen**.
> **Status:** GA since Q3 2025 (see [launch announcement](./newsletter-2025-q3.md)).
> **On-call:** `#data-oncall` in Beacon · PagerDuty rotation "conduit-primary".

## What Conduit is

**Conduit** is Best Bank's central data pipeline. It extracts data from the bank's
operational systems, transforms and standardizes it, and loads it into **Reservoir**,
the analytics warehouse. Conduit is the single source feeding **Lighthouse** dashboards,
Finance's [projections](./financial-projections.md), and Risk's **Sentinel** scoring
features.

Before Conduit (pre-2025), each team pulled data directly from production databases
with ad-hoc scripts, causing load on **Vault** and inconsistent numbers across reports.
Conduit replaced that with one governed, observable pipeline.

## Architecture

```
   SOURCES                 INGESTION            TRANSFORM            SERVE
 ┌──────────┐           ┌─────────────┐      ┌──────────┐      ┌──────────────┐
 │  Vault   │──CDC─────▶│             │      │          │      │  Lighthouse  │
 │ (ledger) │           │   Conduit   │      │  dbt     │      │  (BI/dash)   │
 ├──────────┤           │  Ingestion  │─────▶│ models   │─────▶├──────────────┤
 │ Compass  │──API──────▶│  (Airflow + │      │ (staging │      │  Reservoir   │
 │  (CRM)   │           │  Kafka)     │      │  → marts)│      │  (warehouse) │
 ├──────────┤           │             │      │          │      ├──────────────┤
 │ Sentinel │──events──▶│             │      │          │      │  Finance /   │
 │ (risk)   │           └─────────────┘      └──────────┘      │  Risk extracts│
 ├──────────┤                                                  └──────────────┘
 │ App/Web  │──events──▶ (Kafka topics: txn, login, openacct)
 │ telemetry│
 └──────────┘
```

### Components

| Layer | Technology | Notes |
|-------|-----------|-------|
| Change data capture | Debezium → Kafka | Streams row-level changes from **Vault** |
| Streaming bus | Apache Kafka | Topics for transactions, logins, account opens |
| Orchestration | Apache Airflow | Batch DAGs + micro-batch triggers |
| Warehouse | **Reservoir** (Snowflake) | Layered: `raw` → `staging` → `marts` |
| Transformation | dbt | Versioned models, tests, lineage docs |
| Serving | **Lighthouse** | Looker-style semantic layer on `marts` |

## Data sources

| Source system | Connection | Cadence | Owner |
|---------------|-----------|---------|-------|
| **Vault** (core ledger) | CDC (Debezium) | Near-real-time | Platform Eng (Kevin Mbeki) |
| **Compass** (CRM) | REST API pull | Hourly | Product (Olivia Grant) |
| **Sentinel** (risk engine) | Event stream | Real-time | Risk (Tomás Herrera) |
| App / web telemetry | Kafka producers | Real-time | Mobile & Web (Sofia Ramos) |

## Warehouse layers in Reservoir

1. **`raw`** — landing zone, schema-on-read, immutable. Retained 90 days.
2. **`staging`** — cleaned, typed, deduplicated. One staging model per source table.
3. **`marts`** — business-conformed models consumed by Lighthouse and extracts.

### Core marts

| Mart | Grain | Primary consumers |
|------|-------|-------------------|
| `mart_accounts` | one row per account | Finance, Product |
| `mart_transactions` | one row per posted txn | Risk, Finance |
| `mart_customer_360` | one row per customer | Compass, Marketing |
| `mart_revenue_daily` | day × revenue stream | FP&A → [projections](./financial-projections.md) |
| `mart_fraud_signals` | account × scored event | Sentinel feature store |

The product-level rollup published from `mart_accounts` is exported nightly to
[`data/accounts_summary.csv`](./data/accounts_summary.csv); `mart_revenue_daily`
backs [`data/monthly_revenue_2025.csv`](./data/monthly_revenue_2025.csv).

## Scheduling & SLAs

| Pipeline | Trigger | SLA | Alert channel |
|----------|---------|-----|---------------|
| Ledger CDC → `raw` | Streaming | < 5 min lag | `#data-oncall` |
| Nightly dbt build | 02:00 ET daily | Complete by 05:00 ET | PagerDuty |
| Compass hourly sync | Top of hour | < 15 min | `#data-oncall` |
| Sentinel feature export | Streaming | < 2 min lag | PagerDuty (P1) |

If the nightly build misses its 05:00 ET SLA, **Lighthouse** dashboards display a
"data delayed" banner and FP&A is notified before market open.

## Data governance

- **PII handling.** Customer PII (SSN, full PAN) is tokenized at ingestion; Reservoir
  stores only masked values. Access to unmasked fields requires Compliance approval
  (Robert Ellis) and is logged.
- **Lineage.** dbt exposes column-level lineage; every mart traces back to source.
- **Data quality.** dbt tests run on every build (uniqueness, not-null, referential
  integrity, accepted-value checks). Failures block promotion to `marts`.
- **Ownership.** Each mart has a named owner in the dbt `meta` block and an SLA tier.

## Common runbooks

| Incident | First step | Escalation |
|----------|-----------|-----------|
| Nightly build failed | Check Airflow logs for failing dbt model | Raj Patel |
| CDC lag > 5 min | Verify Kafka consumer health | Platform Eng |
| Sentinel features stale | Confirm event stream; risk falls back to last-good | Tomás Herrera (Risk) |
| Numbers mismatch vs Vault | Reconcile `mart_revenue_daily` to ledger | FP&A + Data Eng |

## Roadmap

- **2026 H1:** Migrate remaining batch sources to streaming (reduce nightly window).
- **2026 H2:** Add Best Credit data domains (card txns, balances, disputes) now that
  [Best Credit](./service-best-credit.md) has launched.
- **2027:** Self-serve dataset publishing for analysts via governed dbt templates.

---
*Related: [Company Hierarchy](./company-hierarchy.md) (Engineering org) ·
[Financial Projections](./financial-projections.md) (a key downstream consumer).*
