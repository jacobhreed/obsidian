# Best Checking

> **Product line:** Deposits · **Product owner:** Hannah Lee (Sr. PM), under CPO Lisa Tran.
> **System of record:** Vault · **Analytics:** Lighthouse `mart_accounts`.
> Balance rollups: [`data/accounts_summary.csv`](./data/accounts_summary.csv).

## Overview

Best Checking is the bank's flagship everyday transaction account and its oldest
product, launched at [founding in 2011](./company-history.md). It is the primary
acquisition product — most customers open a checking account first, then add
[Best Savings](./service-best-savings.md) or, since 2026, [Best Credit](./service-best-credit.md).

As of year-end 2025, Best Checking accounted for roughly **520,000 accounts** and
**$2.2B in balances** (consumer base, plus tier, and business tiers combined).

## Account tiers

| Tier | Monthly fee | Fee waived if… | Highlights |
|------|------------:|----------------|-----------|
| **Best Checking** | $0 | Always free | No minimum balance, no monthly fee |
| **Best Checking+** | $12 | $1,500 avg balance OR $2,000 monthly deposit | Higher ATM rebates, early direct deposit |
| **Best Business Checking** | $15 | $5,000 avg balance | For commercial clients (see [`data/business_clients.csv`](./data/business_clients.csv)) |

## Key features

- **No overdraft trap.** Transactions that would overdraw are declined at no charge,
  rather than processed with a fee — a direct expression of the "Clarity over
  cleverness" value from [company culture](./company-history.md).
- **Early direct deposit.** Eligible deposits posted up to two days early (Best Checking+).
- **ATM network.** Fee-free access nationwide; Best Checking+ rebates out-of-network fees.
- **Real-time alerts.** Push notifications powered by app telemetry that also feeds
  [Conduit](./data-pipeline-conduit.md).
- **Bill pay & external transfers** included at no charge.

## Fees

| Item | Fee |
|------|----:|
| Monthly maintenance (base tier) | $0 |
| Overdraft | $0 (transaction declined) |
| Out-of-network ATM | $2.50 (rebated on Best Checking+) |
| Outgoing domestic wire | $15 |
| Outgoing international wire | $35 |
| Paper statement | $3/mo (e-statements free) |

## How it connects internally

- **Vault** is the ledger of record for every Best Checking transaction.
- Account and transaction data flow through [**Conduit**](./data-pipeline-conduit.md)
  into **Reservoir**, surfacing in **Lighthouse** for Product and Finance.
- **Sentinel** scores transactions in real time for fraud; suspicious activity routes
  to Fraud Ops (Tomás Herrera).
- **Compass** gives Support and Sales a Customer-360 view combining checking activity
  with the customer's other products.

## Cross-sell

Best Checking is the top of the funnel. The 2026 plan in the
[Financial Projections](./financial-projections.md) assumes ~12% of checking customers
adopt [Best Credit](./service-best-credit.md) within 18 months. The "Bring a Friend"
referral program — a descendant of the original 2011 referral offer — remains the
single largest acquisition channel.

---
*Synthetic product documentation for demonstration only.*
