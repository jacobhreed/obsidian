# Best Savings

> **Product line:** Deposits · **Product owner:** Hannah Lee (Sr. PM), under CPO Lisa Tran.
> **System of record:** Vault · **Analytics:** Lighthouse `mart_accounts`.
> Balance rollups: [`data/accounts_summary.csv`](./data/accounts_summary.csv).

## Overview

Best Savings, launched in [2013](./company-history.md), is the bank's interest-bearing
savings line. It is the largest contributor to the deposit base that funds net interest
income in the [Financial Projections](./financial-projections.md).

As of year-end 2025, Best Savings held roughly **280,000 accounts** and **$2.0B in
balances** across high-yield savings and CDs.

## Products & rates

> Rates are illustrative APYs for the demo and tiered by balance. Treasury (under CFO
> Priya Raman) sets pricing; changes are tracked in **Lighthouse**.

### High-Yield Savings

| Balance tier | Illustrative APY |
|--------------|-----------------:|
| $0 – $9,999 | 3.25% |
| $10,000 – $49,999 | 3.75% |
| $50,000+ | 4.10% |

- No monthly fee, no minimum to open.
- Up to 6 withdrawals per statement cycle (standard savings behavior).
- Automatic "round-up" sweeps from a linked [Best Checking](./service-best-checking.md)
  account.

### Certificates of Deposit (CDs)

| Term | Illustrative APY | Min. deposit |
|------|-----------------:|-------------:|
| 6 months | 3.90% | $1,000 |
| 12 months | 4.25% | $1,000 |
| 24 months | 4.40% | $1,000 |
| 48 months | 4.15% | $1,000 |

- Early withdrawal penalty: 90–180 days of interest depending on term.
- Auto-renew at maturity unless changed (10-day grace window).

## Key features

- **Goal buckets.** Customers can split one savings account into named goals
  (e.g., "Emergency", "Vacation") — a top-requested feature shipped in 2024.
- **Round-ups.** Spare change from Best Checking purchases sweeps into savings.
- **Rate transparency.** Full rate sheet shown in-app, reflecting the "Clarity over
  cleverness" value.

## How it connects internally

- Balances and interest accruals are booked in **Vault** and flow through
  [**Conduit**](./data-pipeline-conduit.md) into **Reservoir** (`mart_accounts`,
  `mart_revenue_daily`).
- Net interest income from savings is a core input to the
  [Financial Projections](./financial-projections.md) — a 100bps rate move materially
  affects both APYs paid and NIM.
- **Compass** links a customer's savings goals to their broader relationship for Support.

## Risk note

A rate-driven shift of deposits out of low-cost checking into higher-APY savings/CDs is
tracked by Treasury as a margin risk in the
[projections risk table](./financial-projections.md). Tiered pricing is the primary
mitigation.

---
*Synthetic product documentation for demonstration only.*
