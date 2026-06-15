---
title: "Conduit — Internal Data Pipeline"
type: source
date_ingested: "2026-06-15"
source_file: "raw/data-pipeline-conduit.md"
tags: [best-bank, engineering, data, conduit, pipeline, reservoir, architecture]
---

## Summary

Technical documentation for Conduit, Best Bank's central data pipeline (GA Q3 2025). Conduit extracts from Vault, Compass, Sentinel, and app telemetry; transforms via dbt; and loads into Reservoir (Snowflake). It is the single data source for Lighthouse dashboards, Finance extracts, and Sentinel feature scoring.

## Key points

- **Stack:** Debezium CDC → Kafka (bus) → Airflow (orchestration) → Reservoir/Snowflake (warehouse) → dbt (transforms) → Lighthouse (serving)
- **Sources:** Vault (CDC, near-real-time), Compass (REST API hourly), Sentinel (event stream, real-time), App/Web telemetry (Kafka)
- **Reservoir layers:** `raw` (immutable, 90-day retention) → `staging` (cleaned, deduped) → `marts` (business-conformed)
- **Core marts:** `mart_accounts`, `mart_transactions`, `mart_customer_360`, `mart_revenue_daily`, `mart_fraud_signals`
- **SLAs:** CDC < 5min lag; nightly dbt build complete by 05:00 ET; Sentinel features < 2min lag (P1 alert)
- **PII:** Tokenized at ingestion; Reservoir stores only masked values; unmasked access requires Compliance approval (Robert Ellis)
- **Lineage:** dbt column-level lineage; dbt tests (uniqueness, not-null, referential integrity) block promotion to `marts` if failing
- **Before Conduit:** teams pulled directly from Vault production DB with ad-hoc scripts — inconsistent numbers, load on production
- **Roadmap:** 2026 H1 — move remaining batch jobs to streaming; 2026 H2 — add Best Credit card data domains; 2027 — self-serve dataset publishing

## Concepts introduced

- [[wiki/concepts/data-architecture|Data Architecture]]

## Entities mentioned

- [[wiki/entities/conduit|Conduit]] — this document's primary subject
- [[wiki/entities/vault|Vault]] — primary source system
- [[wiki/entities/compass|Compass]] — source system
- [[wiki/entities/sentinel|Sentinel]] — source system + consumer
- [[wiki/entities/reservoir|Reservoir]] — destination warehouse
- [[wiki/entities/lighthouse|Lighthouse]] — primary serving layer
- [[wiki/entities/leadership-team|Leadership Team]] — Raj Patel (owner), Kevin Mbeki (Vault CDC), Tomás Herrera (Sentinel), Robert Ellis (PII compliance)
