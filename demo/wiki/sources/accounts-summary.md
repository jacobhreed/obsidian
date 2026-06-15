---
title: "Accounts Summary (YE 2025)"
type: source
date_ingested: "2026-06-15"
source_file: "raw/accounts_summary.csv"
tags: [best-bank, data, accounts, balances, deposits]
---

## Summary

Product-level account and balance snapshot as of 2025-12-31. Sourced nightly from `mart_accounts` in Reservoir via Conduit. Covers all active account tiers across Best Checking and Best Savings.

## Key data

| Product | Tier | Accounts | Total Balances | Avg Balance | APY |
|---------|------|----------|---------------|-------------|-----|
| Best Checking | Base | 430,000 | $1.05B | $2,442 | 0% |
| Best Checking | Plus | 78,000 | $620M | $7,949 | 0% |
| Best Checking | Business | 12,000 | $530M | $44,167 | 0% |
| Best Savings | High-Yield | 240,000 | $1.35B | $5,625 | 3.60% |
| Best Savings | CD | 40,000 | $650M | $16,250 | 4.20% |
| **Total** | | **800,000** | **$4.20B** | | |

## Key points

- Checking: 520K total accounts, $2.20B balances (50.4% of deposit base)
- Savings: 280K total accounts, $2.00B balances (47.6%)
- CD holders have the highest average balance ($16,250), nearly 3× savings avg ($5,625)
- Business Checking has the highest average balance across all tiers ($44,167)
- Total deposit base matches the $4.2B figure cited across financial documents

## Entities mentioned

- [[wiki/entities/best-checking|Best Checking]] — 520K accounts, $2.2B
- [[wiki/entities/best-savings|Best Savings]] — 280K accounts, $2.0B
- [[wiki/entities/reservoir|Reservoir]] — `mart_accounts` mart that backs this export
- [[wiki/entities/conduit|Conduit]] — pipeline producing this nightly extract
