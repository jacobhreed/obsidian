---
title: "Monthly Revenue 2025"
type: source
date_ingested: "2026-06-15"
source_file: "raw/monthly_revenue_2025.csv"
tags: [best-bank, data, revenue, finance, 2025]
---

## Summary

Month-by-month revenue breakdown for all of 2025, sourced from `mart_revenue_daily` in Reservoir. Four streams: NII, card interchange, account/service fees, other income. Shows steady growth from $18.2M (January) to $21.2M (December), total $236.0M for the year.

## Key data

| Period | NII | Interchange | Fees | Other | Total |
|--------|-----|-------------|------|-------|-------|
| Jan 2025 | $13.29M | $2.18M | $1.64M | $1.09M | $18.20M |
| Jun 2025 | $14.31M | $2.35M | $1.76M | $1.18M | $19.60M |
| Sep 2025 | $14.82M | $2.44M | $1.83M | $1.21M | $20.30M |
| Dec 2025 | $15.48M | $2.54M | $1.91M | $1.27M | $21.20M |
| **Full year** | **$172.3M** | **$28.3M** | **$21.3M** | **$14.1M** | **$236.0M** |

## Key points

- Revenue grew consistently each month — no dips or flat periods in 2025
- NII is dominant (73% of revenue), driven by deposit base and spread
- Card interchange ($28.3M) is currently 100% from debit/existing products; Best Credit card volume will add to this starting 2026
- Monthly run rate reached $20M+ by August, consistent with Q3 newsletter's reported figures
- Full-year total of $236.0M matches financial projections document exactly

## Concepts introduced

- [[wiki/concepts/revenue-model|Revenue Model]]

## Entities mentioned

- [[wiki/entities/reservoir|Reservoir]] — `mart_revenue_daily` backs this data
- [[wiki/entities/conduit|Conduit]] — pipeline that produces this extract
- [[wiki/entities/best-checking|Best Checking]] — debit interchange source
- [[wiki/entities/best-savings|Best Savings]] — NII contribution
