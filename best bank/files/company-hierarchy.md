# Best Bank — Company Hierarchy

> Org structure as of June 2026. For headcount by department, see
> [`data/headcount_by_dept.csv`](./data/headcount_by_dept.csv).
> For the people-and-products context behind these roles, see the
> [Company History](./company-history.md).

## Executive Leadership Team (ELT)

| Role | Name | Reports to | Notes |
|------|------|-----------|-------|
| Founder & CEO | **Eleanor Vance** | Board of Directors | Founded the bank in 2011 |
| President & COO | **David Okafor** | CEO | Joined 2018; runs Operations & Branch Network |
| CFO | **Priya Raman** | CEO | Owns [Financial Projections](./financial-projections.md) |
| CTO | **Samuel Chen** | CEO | Joined 2021; modernized the data stack |
| Chief Risk Officer | **Maria Delgado** | CEO | Owns **Sentinel** and credit risk |
| Chief Compliance Officer | **Angela Brooks** | CEO | BSA/AML, regulatory exams |
| Chief Marketing Officer | **James Whitfield** | CEO | Owns brand, growth, and [*The Best Brief*](./newsletter-2025-q3.md) |
| Chief Product Officer | **Lisa Tran** | CEO | Owns product roadmap and **Compass** |

## Org chart (summary)

```
                          Eleanor Vance — Founder & CEO
                                      |
  ┌─────────────┬─────────────┬───────┴───────┬─────────────┬─────────────┐
 COO           CFO           CTO             CRO            CCO           CPO
Okafor        Raman          Chen           Delgado        Brooks         Tran
  │             │             │               │              │             │
Operations    Finance      Engineering     Risk &         Compliance    Product
Branches      Accounting   - Platform      Fraud Ops      BSA/AML       - Best Checking
Cust. Support Treasury     - Data Eng.     - Sentinel     Audit         - Best Savings
Card Ops      FP&A         - Mobile/Web    Credit Risk    Legal         - Best Credit
                           - Security                                   - Compass
                                                                        Marketing*
* Marketing (CMO Whitfield) sits parallel to Product and partners closely with it.
```

## Engineering (CTO — Samuel Chen)

Engineering is the largest technical org and the home of the bank's internal tools.

| Team | Lead | Owns |
|------|------|------|
| Platform Engineering | **Kevin Mbeki** (VP) | **Vault** core ledger, infrastructure, CI/CD |
| Data Engineering | **Raj Patel** (Head of Data) | **Conduit**, **Reservoir**, **Lighthouse** |
| Mobile & Web | **Sofia Ramos** (VP) | Customer apps, online account opening |
| Security | **Daniel Cho** (Director) | AppSec, access management, encryption |

Data Engineering's flagship system is documented in
[Conduit — Internal Data Pipeline](./data-pipeline-conduit.md). Raj Patel's team also
maintains the analytics layer (**Lighthouse**) consumed by Finance and Risk.

## Product (CPO — Lisa Tran)

| Team | Lead | Product |
|------|------|---------|
| Deposits | **Hannah Lee** (Sr. PM) | [Best Checking](./service-best-checking.md), [Best Savings](./service-best-savings.md) |
| Lending & Cards | **Marcus Bell** (Sr. PM) | [Best Credit](./service-best-credit.md) |
| Platform & Data Products | **Olivia Grant** (PM) | **Compass** CRM, customer insights |

## Risk & Compliance (CRO — Maria Delgado / CCO — Angela Brooks)

- **Fraud Operations** — monitors **Sentinel** alerts; led by **Tomás Herrera** (Director).
- **Credit Risk** — underwriting models for Best Credit; led by **Nadia Fields** (Director).
- **BSA/AML & Compliance** — reports to Angela Brooks; led by **Robert Ellis** (Director).

## Finance (CFO — Priya Raman)

- **FP&A** — builds the [Financial Projections](./financial-projections.md); led by **Grace Kim** (Director).
- **Treasury** — manages liquidity and the deposit/loan mix.
- **Accounting** — consumes monthly extracts from **Reservoir** (see
  [`data/monthly_revenue_2025.csv`](./data/monthly_revenue_2025.csv)).

## Operations (COO — David Okafor)

- **Branch Network** — 14 branches/hubs (see [`data/branches.csv`](./data/branches.csv)).
- **Customer Support** — phone, chat, and in-app, staffed across two hubs.
- **Card Operations** — issuance and disputes for Best Credit, partnering with Fraud Ops.

---
*All names and reporting lines are synthetic and for demonstration only.*
