---
title: "Conduit (Data Pipeline)"
type: entity
entity_kind: product
tags: [system, data, pipeline, engineering, conduit]
source_count: 8
---

## Overview

Conduit is Best Bank's central data pipeline, GA since Q3 2025. It extracts from all operational systems (Vault, Compass, Sentinel, App telemetry), transforms via dbt, and loads into Reservoir. It replaced a fragmented set of ad-hoc scripts with one governed, observable pipeline.

## Role in this wiki

Conduit is the data backbone that connects every part of the bank. Almost every data discussion — financial reporting, fraud scoring, product analytics, underwriting — passes through it. Its launch in Q3 2025 was the bank's most significant infrastructure event of the year.

## Key facts

- **Owner:** Raj Patel (Head of Data Engineering), under Samuel Chen (CTO)
- **On-call:** `#data-oncall` Beacon channel + PagerDuty "conduit-primary" rotation
- **Tech stack:** Debezium (CDC) → Kafka → Airflow → Snowflake/Reservoir → dbt → Lighthouse
- **SLAs:** Vault CDC < 5min lag; nightly dbt build by 05:00 ET; Sentinel features < 2min lag (P1)
- Before Conduit: three teams could pull the same number from Vault and get three different answers
- **PII:** Tokenized at ingestion; Reservoir stores only masked values
- **Roadmap:** 2026 H1 — batch → streaming; 2026 H2 — Best Credit card data domains; 2027 — self-serve publishing

## Sources

- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — full technical reference
- [[wiki/sources/newsletter-2025-q3|Newsletter 2025 Q3]] — GA launch announcement
- [[wiki/sources/newsletter-2025-q4|Newsletter 2025 Q4]] — named as 2025's defining infrastructure event
- [[wiki/sources/newsletter-2026-q1|Newsletter 2026 Q1]] — card data domain expansion
- [[wiki/sources/company-history|Company History]] — milestone (Q3 2025)
- [[wiki/sources/financial-projections|Financial Projections]] — operating leverage from Conduit
- [[wiki/sources/service-best-credit|Best Credit Docs]]
- [[wiki/sources/service-best-checking|Best Checking Docs]]

## Related entities

- [[wiki/entities/vault|Vault]] — primary source
- [[wiki/entities/reservoir|Reservoir]] — destination
- [[wiki/entities/sentinel|Sentinel]] — source + consumer
- [[wiki/entities/compass|Compass]] — source
- [[wiki/entities/lighthouse|Lighthouse]] — serving layer on top of Reservoir

## Related concepts

- [[wiki/concepts/data-architecture|Data Architecture]]
