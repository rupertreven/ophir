# Use Case — Receivables / DSO / Financing v1

> **Date:** 2026-08-29 00:08 CEST  
> **Status:** Initial deep dive / economic model + Belgian legal-tax gate  
> **Target:** Belgian construction, staffing, services and mid-market companies

## Executive conclusion

Receivables is a genuine six-figure treasury problem at moderate revenue scale, but Ophir must distinguish **three different sources of value**:

1. reducing avoidable collection/approval delay;
2. choosing intelligently between waiting and financing a receivable;
3. reducing the cost of receivables financing through competition/data/structure.

The first can release substantial working capital but is partly an AR/collections problem rather than pure treasury. The second fits Ophir particularly well: given cash forecast, debt cost, invoice quality, expected payment date and available financing quotes, determine whether financing a specific receivable creates positive net value.

Tokenized receivables are potentially relevant later if they broaden the financing market, improve transfer/settlement, or make invoices programmable/verifiable. They are not required for the initial value proposition.

---

## 1. Economic scale

For annual revenue `R`, reducing DSO by `d` days releases approximately:

```text
working capital released = R × d / 365
```

### €100m revenue company

```text
5 days DSO  -> €1.37m released
10 days     -> €2.74m released
15 days     -> €4.11m released
```

At a 5% marginal funding cost:

```text
5 days      -> ~€68.5k annual financing value
10 days     -> ~€137k
15 days     -> ~€205k
```

Thus a 10-day avoidable delay at €100m revenue clears the €100K filter.

### €250m construction group

```text
5 days      -> €3.42m working capital
10 days     -> €6.85m
```

At 5% funding cost:

```text
5 days      -> ~€171k/year
10 days     -> ~€342k/year
```

This is economically material.

---

## 2. Construction-specific receivables problem

Construction receivables are not ordinary SaaS invoices. Payment may depend on:

- progress claims / vorderingsstaten;
- architect/client approval;
- measurement/quantity disputes;
- retention;
- provisional/final acceptance;
- variation/change-order approval;
- public procurement payment rules;
- contractual certification;
- subcontractor documentation;
- invoice formalities;
- project disputes.

A generic 'send reminders faster' product is insufficient.

Ophir's construction wedge could be **cash-conversion intelligence tied to project milestones and receivable enforceability**.

---

## 3. Three opportunity classes

### A. Avoidable operational delay

Example:

```text
Invoice amount:                         €1,000,000
Contractual payment due:                30 days
Actual payment:                         48 days
Avoidable delay:                        18 days
Marginal funding cost:                  5%

Cost of delay:
€1m × 18 / 365 × 5% ≈ €2,466
```

Across 100 such invoices/year, material value emerges.

Ophir identifies root causes:

```text
invoice submitted late
missing attachment
approval not requested
approval completed but invoice not issued
invoice disputed
retention incorrectly applied
payment overdue
```

### B. Finance-versus-wait decision

Suppose:

```text
Approved receivable:                    €2m
Expected payment:                       60 days
Company overdraft cost:                 5.5%
Factor/receivable finance quote:         4.2% annualised + fees
```

If financing the receivable replaces more expensive borrowing, it may create positive value.

Ophir should calculate:

```text
cost to wait
vs
all-in financing cost
vs
liquidity/risk benefit
```

and prepare the financing option for customer execution.

### C. Financing-price optimization

If a company finances €20m average receivables and Ophir/provider competition reduces all-in financing cost by 50 bp:

```text
€20m × 0.50% = €100k/year
```

This clears the €100K filter without changing DSO.

---

## 4. Belgian legal gate

### Payment terms

Belgian B2B payment rules implement EU late-payment principles and restrict abusive/excessive payment terms. Public authorities are subject to specific procurement/payment frameworks.

Ophir should model contractual/statutory due dates but must not infer enforceability from invoice date alone.

### Assignment / factoring

Receivables financing can involve assignment/pledge/subrogation structures. Required checks can include:

- contractual assignment restrictions;
- debtor notification;
- existing bank security/pledge over receivables;
- priority/conflict with other lenders;
- recourse/non-recourse structure;
- insolvency effects;
- public-sector receivable restrictions/processes.

Ophir can surface and prepare facts, but provider/counsel owns the financing transaction/legal perfection.

### Construction disputes

A disputed progress claim should not be presented as equivalent to an approved undisputed receivable.

Use states such as:

```text
DRAFT_CLAIM
SUBMITTED
CERTIFICATION_PENDING
CERTIFIED
INVOICED
DISPUTED
UNDISPUTED_DUE
OVERDUE
RETENTION
FINANCE_ELIGIBILITY_UNKNOWN
```

---

## 5. Belgian tax/accounting gate

Need to model separately:

- ordinary trade receivable;
- retention receivable;
- assigned/factored receivable;
- factoring fees/interest;
- bad-debt provisions/write-offs;
- VAT timing/corrections;
- late-payment interest;
- recourse obligations;
- derecognition versus secured borrowing treatment.

Exact accounting depends on transaction structure and accounting framework. Automated journal treatment requires professional validation.

---

## 6. Ophir product flow

```text
ERP / project system / e-invoicing
          │
          ├── contract
          ├── progress claim
          ├── certification
          ├── invoice
          ├── due date
          └── dispute/retention

Bank data
          │
          └── actual payment date

Debt facilities
          │
          └── marginal funding cost

Receivables finance providers
          │
          └── quote/eligibility data

          ▼
OPHIR RECEIVABLE INTELLIGENCE
          │
          ├── true DSO by stage/root cause
          ├── avoidable-delay cost
          ├── cash forecast impact
          ├── finance-vs-wait calculation
          ├── financing-price comparison
          └── accounting/tax consequences
```

---

## 7. Example alert

```text
RECEIVABLE OPPORTUNITY

Project: Data Center North
Certified invoice:                         €2,400,000
Due date:                                  18 Sep 2026
Expected payment based on debtor history:  12 Oct 2026
Expected delay beyond due date:            24 days

Marginal revolver cost:                    5.10%
Expected financing cost:                   4.35%

Cost of waiting (24d funding):             ~€8,049
Indicative finance cost equivalent:        ~€6,865
Potential economic benefit:                ~€1,184

Assignment restriction:                    review required
Existing receivables pledge:               detected
Tax/accounting treatment:                  provider structure required

[View calculation]
[Prepare financing dossier]
```

Ophir does not assign the invoice or execute financing.

---

## 8. Stronger portfolio view

The product becomes much more powerful at portfolio level:

```text
€32m receivables outstanding
€11m certification pending
€14m certified/invoiced
€4m overdue undisputed
€3m disputed/retention

Avoidable approval/invoice delay:          6.8 days
Capital trapped by avoidable delay:        €4.7m
Estimated annual funding cost:             €235k

Receivables eligible for financing:        €8.4m
Current financing spread vs alternatives:  62 bp
Potential annual saving:                   €52k
```

Combined opportunity can exceed €250k/year in larger groups.

---

## 9. Tokenization relevance

### Potential future value

Tokenized receivables could theoretically provide:

- standardized ownership/assignment record;
- faster settlement;
- broader financing marketplace;
- fractional/institutional funding access;
- programmable payment waterfall;
- integration with verified invoice/project data;
- collateral use.

### Reality check

Tokenization creates no value if:

- debtor quality/approval remains uncertain;
- legal assignment is unclear;
- financing rate is not lower;
- investors require the same underwriting anyway;
- Belgian tax/accounting complexity rises.

Therefore Ophir should compare conventional factoring/receivables finance and tokenized alternatives neutrally.

---

## 10. Why this fits Ophir architecture

The architecture already requires:

- bank connectivity;
- accounting/ERP data;
- legal-entity model;
- cash forecast;
- rules engine;
- instrument/provider intelligence;
- document preparation;
- human decision/provider execution;
- reconciliation.

Receivables adds project/contract states and financing quotes rather than requiring a new platform thesis.

---

## 11. Competitive risk

AR automation, collections software, factoring platforms, ERP modules and TMS products already address pieces of the problem.

Ophir differentiation must not be 'better collections dashboard'.

Candidate wedge:

> **Treasury decision engine connecting project receivable state to marginal funding cost and financing alternatives.**

For construction:

> **Which receivable should I accelerate, finance, dispute-escalate or simply wait for — and what is each day costing me?**

---

## 12. €100K verdict

`PRIORITY CANDIDATE`, especially for construction/mid-market groups with €100m+ revenue.

Why:

- 10 DSO days on €100m revenue corresponds to €2.74m working capital;
- at 5% marginal funding cost this is ~€137k/year;
- larger construction groups reach several hundred thousand euros quickly;
- financing spread optimization can independently clear €100k at €20m financed receivables × 50 bp;
- Ophir can provide decision intelligence without executing financing.

Risks:

- improving DSO is partly operational/process change, not software-only;
- many delays are contractual/dispute-driven and not avoidable;
- financing eligibility and price require provider data;
- incumbents exist;
- tokenization is not yet demonstrated as a superior financing rail.

## 13. Market validation required

For 5–10 Belgian construction/service groups collect:

- revenue;
- DSO;
- receivables by lifecycle state;
- average certification delay;
- invoice issuance delay after certification;
- overdue undisputed balance;
- retention balance;
- disputed balance;
- marginal debt cost;
- current factoring/receivables financing volume/rate;
- current AR software/process;
- finance FTE time;
- current bank receivables pledges;
- historical write-offs.

### Promote criterion

Promote if target customers show >€2m of realistically avoidable/financeable working capital and >€100k annual funding/process value.

### Kill/downgrade criterion

Downgrade if most DSO is structurally contractual/non-actionable or existing ERP/AR/TMS processes already capture the economically actionable portion.
