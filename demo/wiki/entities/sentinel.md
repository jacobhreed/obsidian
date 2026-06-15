---
title: "Sentinel (Risk & Fraud Engine)"
type: entity
entity_kind: product
tags: [system, risk, fraud, sentinel, engineering]
source_count: 6
---

## Overview

Sentinel is Best Bank's real-time risk scoring engine. It scores every transaction for fraud, provides features for credit underwriting, and streams events into Conduit. Piloted in 2024, it became a core Conduit consumer in Q3 2025.

## Role in this wiki

Sentinel is the risk layer that sits across all of Best Bank's products. For Best Checking and Savings it is the fraud guard. For Best Credit it does double duty: real-time fraud scoring on card swipes AND the underwriting feature store.

## Key facts

- **Owner:** Chief Risk Officer Maria Delgado; day-to-day operations by Fraud Ops lead Tomás Herrera
- Piloted 2024; became core production system Q3 2025 (Conduit GA)
- Real-time alert latency: < 2 minutes (P1 SLA in Conduit)
- Sentinel alert → Fraud Ops (Tomás Herrera) for review
- For Best Credit: Nadia Fields (Credit Risk) uses Sentinel features + Reservoir deposit history for underwriting
- 2025 pilot: net fraud losses at **18bps** of card volume
- 2027 target: **<10bps** net fraud losses (per Financial Projections)
- If Sentinel features go stale, system falls back to "last-good" scored values

## Sources

- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — integration, SLAs, failover
- [[wiki/sources/company-history|Company History]] — pilot in 2024
- [[wiki/sources/newsletter-2025-q3|Newsletter 2025 Q3]] — Sentinel → core Conduit consumer
- [[wiki/sources/service-best-credit|Best Credit Docs]] — underwriting and card fraud
- [[wiki/sources/financial-projections|Financial Projections]] — fraud loss targets
- [[wiki/sources/newsletter-2026-q1|Newsletter 2026 Q1]] — fraud-ready from day one for Best Credit

## Related entities

- [[wiki/entities/conduit|Conduit]] — Sentinel events stream into Conduit
- [[wiki/entities/reservoir|Reservoir]] — `mart_fraud_signals` mart; also provides deposit history for underwriting
- [[wiki/entities/best-credit|Best Credit]] — primary new consumer (fraud + underwriting)
- [[wiki/entities/leadership-team|Leadership Team]] — Maria Delgado (CRO), Tomás Herrera (Fraud Ops), Nadia Fields (Credit Risk)

## Related concepts

- [[wiki/concepts/data-architecture|Data Architecture]]
