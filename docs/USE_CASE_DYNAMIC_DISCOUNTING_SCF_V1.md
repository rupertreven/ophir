# Use Case — Dynamic Discounting & Supply-Chain Finance v1

> **Date:** 2026-08-29 09:38 CEST  
> **Status:** Initial deep dive / economic model + legal-tax gate  
> **Target:** Belgian corporates with material supplier spend

## Executive conclusion

Dynamic discounting is one of the strongest mathematical uses of surplus corporate cash found so far. A small invoice discount for materially earlier payment can imply an annualized return far above bank deposits or MMFs.

Example: paying a €100 invoice at day 10 instead of day 40 for a 2% discount uses €98 of cash 30 days earlier to save €2. The simple annualized return on the accelerated cash is roughly:

```text
2 / 98 × 365 / 30 ≈ 24.8% p.a.
```

Even a 1% discount for 30 days early is roughly 12.3% annualized before tax/operational considerations.

This can clear the €100K filter at moderate supplier-spend scale. However, the opportunity exists only where suppliers will actually offer discounts and where early payment does not damage the buyer's own liquidity/covenants.

Ophir's ideal role is a **marginal cash allocator**: compare every early-payment offer with debt repayment, liquidity needs, MMFs/deposits and other uses of cash, then prepare the approved payment proposal. The customer/bank executes.

Supply-chain finance (SCF) is the complementary case when the buyer wants to preserve its own DPO while suppliers receive cash early from a bank/funder.

---

## 1. Dynamic discounting economics

### Example A — 2% for 30 days early

Invoice face value: €100
Early payment: €98
Cash accelerated: €98 for 30 days
Economic gain: €2

```text
period return = 2 / 98 = 2.0408%
annualized simple return ≈ 2.0408% × 365 / 30 = 24.8%
```

This dwarfs a ~2% money-market return.

### Example B — 1% for 30 days early

```text
1 / 99 × 365 / 30 ≈ 12.3% annualized
```

### Example C — 0.5% for 20 days early

```text
0.5 / 99.5 × 365 / 20 ≈ 9.17% annualized
```

Therefore even apparently small discounts can dominate other short-term uses of cash.

---

## 2. €100K scale

Suppose a company has €50m annual addressable supplier spend and suppliers accept an average 1% early-payment discount on only 25% of it:

```text
€50m × 25% × 1% = €125,000 gross annual discount value
```

At €100m spend and 20% adoption at 1%:

```text
€100m × 20% × 1% = €200,000
```

This clears the €100K filter without requiring large treasury balances all year.

But the company uses cash earlier. Ophir must subtract the opportunity/funding cost of those accelerated days.

Example:

```text
Annual invoices discounted:          €12.5m
Average acceleration:                30 days
Average accelerated capital:         ~€1.03m
Alternative cash value:              4.0% p.a. (e.g. debt repayment)
Opportunity cost:                    ~€41k/year
Gross discounts:                     €125k
Indicative economic benefit:         ~€84k/year
```

At a 2% average discount the economics become much stronger.

---

## 3. Correct Ophir decision rule

Never say 'take every discount'.

For each approved invoice calculate:

```text
Discount return for accelerated days
vs
marginal debt repayment return
vs
cash investment return
vs
liquidity buffer value
vs
covenant/facility implications
```

Example:

```text
Supplier discount IRR equivalent     18.4%
Avoidable revolver cost               4.6%
Daily MMF yield                       1.9%
Term deposit                          2.1%

Liquidity stress test                PASS
Minimum cash after payment            €6.8m
Policy minimum                        €5.0m

=> early payment has highest economic value
```

This connects directly to the marginal-euro architecture from the debt/cash use case.

---

## 4. Dynamic discount curve

Rather than fixed `2/10 net 30`, suppliers can offer a curve:

```text
Pay today        1.50% discount
Pay +10 days     1.00%
Pay +20 days     0.50%
Pay +30 days     contractual full amount
```

Ophir can calculate the economically optimal payment date given the buyer's marginal value of cash.

The platform does not need to execute payment. It can produce:

```text
Recommended payment date
Discount captured
Implied annualized return
Liquidity impact
Accounting/tax impact
Payment instructions
```

---

## 5. Supply-chain finance complement

Dynamic discounting uses **buyer's own cash**.

SCF / reverse factoring typically allows:

1. buyer approves supplier invoice;
2. funder/bank pays supplier early;
3. buyer pays funder at agreed maturity;
4. supplier financing rate benefits from buyer credit quality.

Potential buyer value:

- preserve/extend DPO;
- improve supplier liquidity/resilience;
- negotiate better commercial terms;
- reduce supply disruption;
- centralize supplier-finance program.

Potential supplier value:

- cheaper funding;
- predictable cash conversion;
- optional early payment.

Ophir can compare:

```text
pay normally
vs
buyer-funded discount
vs
bank SCF
vs
receivables/factoring alternative
```

for each supplier/invoice cohort.

---

## 6. Belgian legal / tax / accounting gate

### Payment-term law

Belgian B2B payment-term rules and EU late-payment principles constrain payment practices. Dynamic discounting must be genuinely optional and contractually clear; it should not become a disguised mechanism forcing suppliers to surrender margin merely to receive payment within legally/contractually due periods.

### Commercial contract

Need to determine:

- agreed invoice amount;
- discount terms;
- VAT base/correction mechanics;
- credit note requirements where applicable;
- payment date;
- whether discount is financial/commercial under the exact structure;
- procurement/public-contract restrictions;
- supplier consent.

### Accounting/VAT

Discount treatment can affect:

- purchase cost;
- VAT taxable base/corrections;
- accounts payable clearing;
- financial income/discount accounts depending on accounting treatment;
- period recognition.

Belgian accountant validation required before automated postings.

### SCF accounting

Reverse factoring can create accounting presentation/classification questions: trade payable versus financing liability depending on program terms. This matters for balance-sheet ratios, cash-flow presentation and covenants.

Ophir must not optimize DPO by creating hidden financing/accounting distortion.

---

## 7. Construction relevance

Potentially strong because large contractors have large supplier/subcontractor spend.

However:

- subcontractor invoices may depend on progress certification;
- retention/claims complicate approved amount;
- public procurement/payment-chain rules may apply;
- supplier relationships are strategic;
- small subcontractors may value early cash highly.

This creates a possible win-win:

> financially strong contractor uses surplus cash to pay approved subcontractor invoices early in exchange for an optional discount that is cheaper than the subcontractor's alternative financing and more valuable than the contractor's MMF return.

Example economics:

```text
Approved subcontractor invoice        €500,000
Contractual payment                    45 days
Optional payment in 10 days
Discount                               1.0% = €5,000
Cash accelerated                       35 days
Implied simple annualized return       ~10.5%
```

If the contractor's marginal cash value is only 2–5%, there is room for mutual economic benefit.

---

## 8. Tokenization relevance

### Today

Not required. Conventional bank payment + ERP integration is sufficient for the core economics.

### Potential future

Tokenized deposits/programmed money could enable:

- conditional early payment immediately after invoice/project certification;
- 24/7 settlement;
- programmable discount curves;
- automatic split payments;
- SCF funding from broader regulated capital pools;
- tokenized approved-payables/receivables.

But the legal/commercial invoice approval remains the key event. Blockchain does not fix an uncertified/disputed invoice.

---

## 9. Ophir UX example

```text
EARLY PAYMENT OPPORTUNITIES

Available deployable cash             €4.2m
Minimum liquidity buffer              €5.0m (post-payments remains €6.1m)
Marginal debt cost                     4.30%
Daily treasury yield                   1.85%

Supplier        Amount      Days early   Discount   Annualized return
SteelCo         €820k       28           1.20%      ~15.9%
Electro NV      €310k       20           0.50%      ~9.2%
ConcreteCo      €1.1m       35           0.25%      ~2.4%

Priority:
1. SteelCo — attractive vs all alternatives
2. Electro NV — attractive
3. ConcreteCo — repay revolver instead

Estimated net economic value of selected offers: €X

[View calculations]
[Prepare payment plan]
```

---

## 10. Competitive landscape risk

Dynamic-discounting and SCF platforms already exist, as do bank programs and procurement/AP tools.

Ophir differentiation should not be 'we invented early payment'.

Potential wedge:

> **Treasury-wide marginal cash allocator that treats supplier discounts as one investable use of cash alongside debt repayment, deposits, MMFs and other opportunities.**

That is much more aligned with the emerging Ophir thesis.

---

## 11. €100K verdict

`PRIORITY CANDIDATE` where supplier spend is material and discount adoption is feasible.

Why:

- implied returns can be an order of magnitude above MMF yields;
- €50m addressable spend × 25% adoption × 1% discount = €125k gross;
- integrates directly with AP/ERP and cash forecast;
- no need for Ophir to execute payments;
- creates supplier as well as buyer value;
- tokenized rails can improve the mechanism later but are not required.

Risks:

- suppliers may not offer meaningful discounts;
- procurement teams may already negotiate payment discounts centrally;
- using cash early can be inferior to debt repayment;
- legal/VAT/accounting treatment must be correct;
- supplier power dynamics/reputation matter;
- existing platforms are mature.

---

## 12. Market validation

For target companies collect:

- annual supplier/AP spend;
- average DPO;
- percentage invoices approved well before due date;
- current early-payment discounts;
- supplier financing pain;
- current dynamic-discounting/SCF programs;
- available deployable cash;
- marginal debt cost;
- AP approval timing;
- procurement ownership of discount negotiations;
- supplier acceptance rates;
- ERP/API data availability.

### Promote criterion

Promote if target companies show >€10m/year of invoices eligible for optional discounts with expected net economic benefit >€100k/year after opportunity cost.

### Downgrade criterion

Downgrade if meaningful discounts are already fully captured by procurement/AP systems or supplier adoption is too low.
