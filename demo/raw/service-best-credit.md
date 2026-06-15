# Best Credit

> **Product line:** Lending & Cards · **Product owner:** Marcus Bell (Sr. PM), under CPO Lisa Tran.
> **Risk owner:** Credit Risk (Nadia Fields), under CRO Maria Delgado.
> **Launched:** Q1 2026 (see [launch announcement](./newsletter-2026-q1.md)).
> **System of record:** Vault (card subledger) · **Fraud scoring:** Sentinel.

## Overview

Best Credit is the bank's first credit product line, launched in
[Q1 2026](./company-history.md). It comprises a consumer credit card and a personal
line of credit, both underwritten in-house. Best Credit is the primary growth lever in
the 2026–2028 [Financial Projections](./financial-projections.md), expected to add
interest income on revolving balances and a step-up in card interchange.

The plan assumes ~12% of existing [Best Checking](./service-best-checking.md) customers
open a Best Credit account within 18 months.

## Products

### Best Credit Card

| Attribute | Detail |
|-----------|--------|
| Annual fee | $0 |
| Rewards | 2% cash back on everyday spend; 3% on the customer's top category |
| Intro APR | 0% on purchases for 12 months, then 18.99%–26.99% variable |
| Credit limits | $500 – $25,000, assigned by underwriting |
| Network | Major card network; interchange feeds [revenue](./financial-projections.md) |

### Best Line of Credit

| Attribute | Detail |
|-----------|--------|
| Amount | $2,000 – $50,000 |
| APR | 9.99%–22.99% variable |
| Draw period | Revolving; pay down and reuse |
| Best for | Customers who want flexible access without a card |

## Underwriting & credit risk

- Applications are scored by **Credit Risk** (Nadia Fields) using a model that
  consumes features from **Sentinel** and the customer's deposit history in
  **Reservoir** (via [Conduit](./data-pipeline-conduit.md)).
- Initial limits are deliberately conservative at launch; the
  [projections](./financial-projections.md) model credit losses at **2.8% of balances**.
- Existing Best Checking/Savings customers benefit from a "known customer" lift in
  approval odds, since the bank already sees their cash-flow behavior.

## Fraud & disputes

- Every card transaction is scored in real time by **Sentinel**; high-risk events
  route to Fraud Ops (Tomás Herrera).
- Disputes and chargebacks are handled by **Card Operations** under COO David Okafor.
- The [projections](./financial-projections.md) target net fraud losses below **10bps**
  of card volume by 2027, down from the 18bps observed in the 2025 Sentinel pilot.

## How it connects internally

- **Vault** holds the card subledger (balances, payments, interest).
- New card data domains (transactions, balances, disputes) are being added to
  [**Conduit**](./data-pipeline-conduit.md) in 2026 H2 per the pipeline roadmap.
- **Compass** surfaces the credit relationship alongside checking and savings for a
  full Customer-360.
- **Lighthouse** dashboards track adoption, balances, and loss rates for Product,
  Finance, and Risk.

## Go-to-market

The launch is led by CMO **James Whitfield**, targeting existing deposit customers
first (lowest acquisition cost, best risk profile). See the
[2026-Q1 newsletter](./newsletter-2026-q1.md) for the internal launch summary.

---
*Synthetic product documentation for demonstration only. Rates and APRs are illustrative.*
