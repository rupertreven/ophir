# Use Case — Debt + Idle Cash Optimization v1

> **Date:** 2026-08-29 00:04 CEST  
> **Status:** Initial deep dive / `PUBLIC_SOURCE_RESEARCH` + economic model  
> **Target:** Belgian mid-market and large multi-entity companies

## Executive conclusion

This is the first €100K sprint candidate with a **structurally plausible six-figure value proposition at ordinary mid-market balance-sheet scale**.

The core inefficiency is simple:

> A group can simultaneously hold low-yield cash in one account/entity while paying materially higher interest on overdrafts, revolving facilities or other short-term debt elsewhere.

The gross spread can easily be several percentage points. At €3m–€5m of avoidable simultaneous cash/debt exposure, annual economic leakage can reach €100k+ without requiring exotic tokenized products.

Ophir's value is not to transfer or repay automatically. It identifies the overlap, models legal/tax/covenant constraints, quantifies the after-tax benefit, and prepares the treasury action for human execution.

Tokenized infrastructure is optional/future: faster cross-entity settlement or tokenized deposits may reduce timing friction, but the initial wedge is treasury intelligence.

---

## 1. Problem

Typical fragmented group:

```text
Entity A — Bank 1 current account       +€4.0m cash
Entity B — Bank 2 overdraft             -€2.5m debt
Entity C — Bank 3 current account       +€1.2m cash
Entity D — revolving facility           -€6.0m debt
```

A consolidated group view may reveal that the company is paying borrowing rates while substantial group cash earns overnight/deposit rates.

Reasons this persists:

- legal entities are managed separately;
- different ERPs/banks;
- project ring-fencing;
- intercompany lending rules;
- tax/transfer-pricing concerns;
- covenant restrictions;
- cash ownership/operational buffers;
- poor forecast confidence;
- treasury team lacks real-time consolidated visibility;
- debt and cash are managed in separate workflows.

Ophir must not assume all group cash is freely transferable.

---

## 2. Current-rate context

ECB/NBB monetary-financial data in 2026 show the general structural spread between low-remunerated corporate overnight cash and corporate borrowing rates remains material.

For Ophir, public averages are only discovery data. The production calculation must use the customer's **actual account remuneration and facility pricing**:

```text
actual cash interest
actual overdraft rate
actual revolver margin + reference rate
commitment fees
break costs
minimum cash policy
intercompany tax cost
```

This makes bank connectivity economically valuable even without payment initiation.

---

## 3. Core economic examples

### Scenario A — same legal entity

Company has:

```text
Average excess operating cash:          €3m
Cash yield:                              0.30%
Average revolver/overdraft debt:         €3m
Debt cost:                               4.00%
```

Gross avoidable spread:

```text
€3m × (4.00% - 0.30%) = €111,000/year
```

This clears the €100K filter with only €3m overlap.

If debt cost is 5.0% and cash yield 0.25%:

```text
€3m × 4.75% = €142,500/year
```

### Scenario B — €10m fragmented balance sheet

```text
Idle cash:                               €5m @ 0.30%
Short-term debt:                         €5m @ 4.25%
Spread:                                  3.95%
Gross economic leakage:                  €197,500/year
```

Even if only 60% of that overlap is safely actionable after buffers/covenants:

```text
€3m × 3.95% = €118,500/year
```

### Scenario C — optimization versus daily MMF rather than debt repayment

If cash cannot legally/operationally be used to repay debt, Ophir can compare:

```text
Current cash yield                       0.30%
Eligible daily-liquid fund               1.80%
Incremental yield                        1.50%
€5m actionable cash                      × 1.50%
Value                                    €75,000/year
```

Useful, but debt/cash netting is economically stronger whenever permitted.

---

## 4. Why this can be much larger in multi-entity groups

Suppose a construction group has 25 entities and 40 bank accounts.

Ophir sees:

```text
Group cash                               €18m
Required operating buffers               €8m
Potentially deployable                   €10m

Short-term debt / overdrafts             €12m
Weighted debt cost                       4.2%
Weighted cash yield                      0.4%
```

Naively the spread on €10m is:

```text
€10m × 3.8% = €380,000/year
```

But **this is not yet realizable value**. Each € must pass legal/tax/operational gates.

If only €4m is genuinely movable/repayable:

```text
€4m × 3.8% = €152,000/year
```

Still six figures.

---

## 5. Belgian legal / tax gate

This is where Ophir becomes more than a dashboard.

### Same legal entity

Usually the cleanest case:
- own cash;
- own bank debt;
- check contractual prepayment/repayment conditions;
- preserve minimum liquidity;
- check facility availability/redraw economics;
- check covenant implications.

### Different group entities

Cash cannot simply be treated as group property.

Potential mechanisms include:
- intercompany loan;
- cash pooling;
- dividend/distribution where legally possible;
- capital transaction;
- central treasury structure.

Each can create:
- corporate-law constraints;
- transfer-pricing requirements;
- arm's-length intercompany interest;
- withholding/tax issues depending on facts;
- accounting entries;
- documentation;
- insolvency/corporate-interest considerations;
- lender covenant/security restrictions.

Ophir should therefore classify balances:

```text
SAME_ENTITY_ACTIONABLE
INTERCOMPANY_POTENTIALLY_ACTIONABLE
RING_FENCED
COVENANT_RESTRICTED
PROJECT_RESTRICTED
TAX_REVIEW_REQUIRED
UNKNOWN
```

Never show the full consolidated spread as 'savings' unless the legal route is validated.

---

## 6. Tax treatment concept

Debt interest and investment/cash income affect Belgian corporate tax differently depending on the instrument and entity.

Production ROI must model:

- tax deductibility of borrowing interest;
- Belgian interest limitation rules where relevant;
- tax on investment/cash income;
- intercompany pricing;
- withholding where applicable;
- transaction/instrument taxes for investment alternatives;
- accounting period timing.

Therefore:

```text
Gross debt-interest avoided
- lost cash/investment income
+/- corporate tax impact
- intercompany/tax friction
- break/prepayment fees
= Net Treasury Benefit
```

The simple spread is a screening metric, not the final recommendation.

---

## 7. Product flow

### Data

```text
Ponto/open banking
        │
        ├── balances
        ├── actual interest credits
        └── overdraft/debt transactions where visible

ERP/accounting
        │
        ├── entity ownership
        ├── AP/AR
        ├── intercompany balances
        └── forecast inputs

Debt facility register
        │
        ├── principal
        ├── rate/index/margin
        ├── maturity
        ├── commitment fee
        ├── redraw
        ├── prepayment rules
        └── covenants
```

### Intelligence

Ophir continuously calculates:

```text
cash by entity
minimum buffer
forecast low point
cash remuneration
short-term debt outstanding
marginal debt cost
cash/debt overlap
legal actionability
break-even period
post-tax savings
```

### Example alert

```text
TREASURY OPPORTUNITY

Entity: BuildCo NV
Average surplus above 45-day policy buffer: €3,400,000
Revolver outstanding:                         €4,100,000
Revolver marginal cost:                            4.15%
Current cash yield:                                0.28%

Potentially actionable overlap:              €3,400,000
Gross annual spread:                              3.87%
Gross annual opportunity:                    €131,580

Prepayment/redraw:                           permitted
Liquidity stress case:                      passed
Tax model:                                   review required
Accounting:                                  straightforward

Certified Net Treasury Benefit:             pending tax validation

[View calculation]
[Prepare repayment instructions]
```

Ophir does not submit the repayment.

---

## 8. Stronger feature: marginal euro routing

Instead of asking 'where should we invest €1m?', Ophir asks:

> **What is the highest-value legal use of the next €1 of corporate cash?**

Possible ordering:

1. avoid overdraft at 6%;
2. repay revolver at 4.2%;
3. capture supplier discount with 12% implied annual IRR;
4. maintain required liquidity buffer;
5. hold daily-liquid treasury asset at 1.8%;
6. term deposit at 2.0% if cash is lockable.

This is more economically powerful than a yield leaderboard.

Ophir should calculate a transparent **marginal cash value curve** subject to legal/entity/liquidity constraints.

---

## 9. Tokenization relevance

### Current wedge

None required.

### Potential future advantages

- tokenized bank deposits could permit faster/24-7 movement between participating treasury entities/banks;
- tokenized regulated MMFs could serve as a liquid holding state when debt cannot be repaid;
- yield-bearing collateral may reduce opportunity cost where facilities accept it;
- programmable settlement may reduce buffer requirements.

But these only matter if provider acceptance and Belgian legal/tax treatment make them superior.

Ophir should remain instrument/rail-neutral.

---

## 10. Competitive question

Treasury-management systems already provide cash visibility, forecasting, pooling and debt modules. Ophir therefore needs a differentiated wedge.

Candidate differentiation:

> **Jurisdiction-aware marginal capital optimizer for mid-market companies.**

Not merely:

> 'You have €18m cash and €12m debt.'

But:

> '€4.2m of that cash is legally and operationally actionable; here are the three highest-value uses after Belgian tax, liquidity policy, facility rules and accounting consequences.'

That combines the tax/accounting/regulatory knowledge graph already being designed with treasury data.

---

## 11. €100K verdict

`PRIORITY CANDIDATE`

Reasons:

- six-figure value appears at only €3m–€5m of overlapping cash/debt;
- problem exists without requiring tokenization adoption;
- bank/accounting data architecture already fits;
- advice can be prepared without Ophir executing money movement;
- Belgian entity/tax complexity creates potential differentiation;
- value can be measured directly in euros.

Main risks:

- good corporate treasury teams already eliminate most same-entity overlap;
- existing TMS/cash-pooling solutions may solve large-group cases;
- intercompany legal/tax constraints can make apparent group cash non-actionable;
- Ponto/accounting APIs may not expose complete facility pricing/covenant data, requiring document ingestion/manual setup.

## 12. Required market validation

Interview/data sample from 10 Belgian companies with €50m–€1bn revenue:

- number of entities;
- number of banks/accounts;
- average daily cash;
- overnight cash remuneration;
- average short-term debt/overdraft;
- marginal debt cost;
- simultaneous positive cash + debt frequency;
- existing cash pooling;
- treasury FTEs/TMS;
- amount legally ring-fenced;
- frequency of manual intercompany funding;
- annual commitment/overdraft fees;
- whether treasury can quantify current avoidable spread.

### Kill criterion

If professionally managed Belgian mid-market companies almost universally have effective pooling/netting and <€1m actionable overlap, downgrade the use case.

### Promote criterion

If typical target companies show €3m+ actionable simultaneous cash/debt at >3 percentage-point spread or equivalent facility inefficiency, this becomes a credible primary Ophir wedge.
