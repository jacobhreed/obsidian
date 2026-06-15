# Best Bank — Financial Projections (2026–2028)

> Prepared by FP&A (Grace Kim, Director) under CFO **Priya Raman**.
> Source data extracted from **Reservoir** via the
> [Conduit pipeline](./data-pipeline-conduit.md) and reconciled against the
> general ledger in **Vault**. Actuals for 2025 are in
> [`data/monthly_revenue_2025.csv`](./data/monthly_revenue_2025.csv).
> *Forward-looking figures are estimates for demonstration only.*

## Executive summary

Best Bank closed 2025 with **$236.0M in total revenue** and an estimated
**$47.2M in net income** (~20% margin), on a deposit base of **$4.2B** and
**~850,000 active customers**. The 2026–2028 plan is anchored on three drivers:

1. **Continued deposit growth** in Best Checking and Best Savings.
2. **The Best Credit launch** (Q1 2026), adding interest income on revolving
   balances and a step-up in card interchange.
3. **Operating leverage** from the data stack — **Conduit**, **Lighthouse**, and
   **Sentinel** — reducing cost-to-serve and fraud losses.

## Revenue history & projection

| Year | Total revenue | YoY growth | Net income | Net margin |
|------|--------------:|-----------:|-----------:|-----------:|
| 2023 (actual) | $188.0M | — | $33.8M | 18.0% |
| 2024 (actual) | $210.0M | +11.7% | $40.0M | 19.0% |
| 2025 (actual) | $236.0M | +12.4% | $47.2M | 20.0% |
| **2026 (proj.)** | **$278.0M** | **+17.8%** | **$58.4M** | **21.0%** |
| **2027 (proj.)** | **$330.0M** | **+18.7%** | **$72.6M** | **22.0%** |
| **2028 (proj.)** | **$388.0M** | **+17.6%** | **$89.2M** | **23.0%** |

## Revenue by stream

| Stream | 2025 actual | 2026 proj. | 2028 proj. | Commentary |
|--------|------------:|-----------:|-----------:|------------|
| Net interest income | $172.3M | $196.0M | $262.0M | Driven by deposit growth + Best Credit balances |
| Card interchange | $28.3M | $40.0M | $62.0M | Step-up from Best Credit card spend |
| Account & service fees | $21.3M | $26.0M | $38.0M | Tied to active account growth |
| Other income | $14.1M | $16.0M | $26.0M | Wires, FX, treasury services |
| **Total** | **$236.0M** | **$278.0M** | **$388.0M** | |

## Balance sheet drivers

| Metric | 2025 | 2026 proj. | 2027 proj. | 2028 proj. |
|--------|-----:|-----------:|-----------:|-----------:|
| Total deposits | $4.2B | $4.9B | $5.7B | $6.5B |
| Active customers | 850K | 980K | 1.12M | 1.27M |
| Best Credit balances | — | $310M | $640M | $980M |
| Net interest margin (NIM) | 3.85% | 3.95% | 4.05% | 4.10% |

A product-level balance breakdown is maintained in
[`data/accounts_summary.csv`](./data/accounts_summary.csv).

## Key assumptions

- **Rate environment.** Plan assumes the Fed funds rate stays within a ~50bps band of
  current levels through 2027. A 100bps drop would compress NIM by ~25bps and reduce
  2027 NII by roughly $9M.
- **Best Credit adoption.** ~12% of existing checking customers open a Best Credit
  account within 18 months. Credit losses modeled at 2.8% of balances, monitored by
  Credit Risk (Nadia Fields) using **Sentinel** scores.
- **Cost-to-serve.** Automation from **Conduit** and self-serve **Lighthouse**
  dashboards is expected to hold operating expense growth below revenue growth,
  improving the efficiency ratio from 62% (2025) to ~56% (2028).
- **Fraud losses.** **Sentinel** is projected to reduce net fraud losses as a share
  of card volume from 18bps (2025 pilot) to under 10bps by 2027.

## Risks

| Risk | Owner | Mitigation |
|------|-------|-----------|
| Rate-driven deposit attrition | Treasury / Priya Raman | Tiered Best Savings pricing |
| Best Credit loss rates above plan | Credit Risk / Nadia Fields | Conservative initial credit limits; Sentinel scoring |
| Data pipeline reliability | Data Eng. / Raj Patel | Conduit SLAs & alerting (see pipeline doc) |
| Regulatory / exam findings | Compliance / Angela Brooks | Quarterly internal audit cadence |

## Investment priorities (2026)

1. **Best Credit go-to-market** — marketing spend led by CMO James Whitfield.
2. **Conduit hardening** — move remaining batch jobs to near-real-time streaming.
3. **Branch network optimization** — consolidate two underperforming locations
   (see [`data/branches.csv`](./data/branches.csv)).

---
*Related: [Company History](./company-history.md) · [Company Hierarchy](./company-hierarchy.md) ·
[2025-Q4 newsletter (year in review)](./newsletter-2025-q4.md)*
