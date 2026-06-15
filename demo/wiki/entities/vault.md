---
title: "Vault (Core Banking Ledger)"
type: entity
entity_kind: product
tags: [system, ledger, engineering, platform]
source_count: 6
---

## Overview

Vault is Best Bank's core banking ledger and the system of record for every account balance and transaction. Deployed in 2014 and still in use today — it is the foundational operational system of the bank.

## Role in this wiki

Vault is the source of truth for all financial data. Every other system (Conduit, Reservoir, Lighthouse, Sentinel) ultimately derives from it. Understanding Vault's role is prerequisite to understanding any data or financial discussion at Best Bank.

## Key facts

- Deployed 2014 — the bank's oldest technical system still in production
- System of record for: Best Checking balances, Best Savings (including CDs), Best Credit card subledger (added 2026)
- **Owned by:** Platform Engineering, led by Kevin Mbeki (VP)
- Vault row-level changes are streamed to Conduit via Debezium CDC (near-real-time)
- Before Conduit (pre-2025), teams ran ad-hoc scripts against Vault's production database directly — caused load and data inconsistency
- The name "Vault" reflects the bank's brand aesthetic and the idea of a trusted place for money

## Sources

- [[wiki/sources/company-history|Company History]] — deployment date (2014)
- [[wiki/sources/data-pipeline-conduit|Conduit Pipeline Docs]] — CDC connection details
- [[wiki/sources/service-best-checking|Best Checking Docs]]
- [[wiki/sources/service-best-savings|Best Savings Docs]]
- [[wiki/sources/service-best-credit|Best Credit Docs]]
- [[wiki/sources/company-hierarchy|Company Hierarchy]] — Platform Engineering ownership

## Related entities

- [[wiki/entities/conduit|Conduit]] — reads Vault via CDC; primary consumer of Vault changes
- [[wiki/entities/reservoir|Reservoir]] — Vault data lands here after transformation
- [[wiki/entities/sentinel|Sentinel]] — consumes transaction data for fraud scoring

## Related concepts

- [[wiki/concepts/data-architecture|Data Architecture]]
