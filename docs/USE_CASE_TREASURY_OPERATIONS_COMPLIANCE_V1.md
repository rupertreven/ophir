# Use Case — Treasury Operations & Compliance Automation v1

> **Date:** 2026-08-29 09:33 CEST  
> **Status:** Initial deep dive / economic model  
> **Target:** Belgian multi-entity mid-market and large corporates

## Executive conclusion

Treasury operations/compliance can plausibly exceed €100k/year in total cost for complex groups, but savings are diffuse rather than a single obvious arbitrage. The strongest Ophir proposition is not generic workflow automation; it is automating the **decision evidence and downstream administration** created by treasury decisions.

Examples:

- bank/account reconciliation;
- cash position consolidation;
- forecast exception investigation;
- debt/facility register maintenance;
- intercompany interest and documentation;
- fund/instrument tax treatment;
- TOB/TACT monitoring;
- journal-entry preparation;
- supporting-document/evidence packs;
- treasury policy compliance;
- audit support;
- provider/instrument data maintenance.

For a complex group, 1–2 finance/treasury FTE equivalents plus external tax/accounting/legal work can readily approach or exceed €100k/year. Ophir does not need to eliminate jobs to create value: reducing manual work, errors, audit effort and adviser dependency can support meaningful SaaS spend.

This use case is likely strongest as the **horizontal glue/moat** around the higher-value optimization modules rather than the initial standalone wedge.

---

## 1. Cost stack

A multi-entity treasury function may spend recurring effort on:

```text
daily cash positioning
bank portal exports
bank reconciliation
forecast updates
facility/interest calculations
intercompany balances
FX exposure reports
guarantee registers
fund/investment administration
accounting entries
tax declarations/reporting
policy checks
management reporting
audit evidence
external adviser questions
```

The cost includes:

- internal treasury/finance salaries;
- accounting team time;
- external accountant/tax adviser;
- bank/TMS fees;
- errors/penalties;
- delayed decisions;
- key-person dependency.

---

## 2. €100K economics

Illustrative loaded annual costs:

```text
0.75 treasury FTE equivalent       €60k
0.50 accounting/controller FTE     €40k
external tax/accounting support    €25k
manual audit/support burden        €15k
---------------------------------------
observable process cost           €140k/year
```

If Ophir removes/avoids 50% of the manual burden:

```text
potential productivity value      ~€70k/year
```

That alone may not clear €100k.

But combine it with avoided adviser work/errors and one optimization module:

```text
operations productivity            €70k
external adviser reduction         €20k
debt/cash optimization            €120k
---------------------------------------
total customer value              €210k/year
```

This suggests operations automation is a **value multiplier** rather than the primary wedge.

---

## 3. Where Ophir differs from generic automation

The hard part is not generating a CSV or journal entry. It is knowing **why** the entry/tax/reporting treatment is correct for the exact instrument/entity/event/date.

Ophir already proposes an effective-dated rules architecture:

```text
legal entity
+ instrument / facility / receivable
+ economic event
+ jurisdiction
+ date
          │
          ▼
validated rule
          │
          ├── tax treatment
          ├── accounting treatment
          ├── filing obligation
          ├── evidence requirement
          └── review level
```

That can turn optimization recommendations into administratively executable decisions.

---

## 4. High-value workflows

### A. Daily treasury close

Instead of manually assembling bank portals/spreadsheets:

```text
08:00
Group cash position                 €18.4m
Available liquidity                 €24.1m
Debt drawn                          €11.2m
Forecast 30d low point               €6.8m
Policy minimum                       €5.0m
Exceptions                              3
```

Only exceptions require human work.

### B. Reconciliation after externally executed action

Customer repays €2m revolver through its bank.

Ophir detects transaction and prepares:

- match to approved treasury action;
- facility balance update;
- interest forecast update;
- journal proposal;
- evidence link;
- realized savings tracking.

### C. Instrument tax/accounting package

For MMF/FCP/tokenized fund activity:

- transaction classification;
- Belgian TOB/TACT analysis;
- transparent-fund income breakdown where required;
- journal entries;
- filing-ready data;
- accountant review pack.

This is already a demonstrated specialist service category in Belgium.

### D. Intercompany treasury administration

For approved intercompany funding:

- agreement/rate reference;
- arm's-length pricing evidence;
- interest accrual schedule;
- balances;
- journal proposals;
- repayment calendar;
- audit evidence.

Legal/tax validation remains required.

### E. Treasury policy engine

Examples:

```text
No bank >35% of unrestricted cash
Minimum €5m group liquidity
No instrument below approved rating/risk class
No maturity beyond forecast liquidity horizon
FX hedge 70–90% of committed exposure
No facility covenant headroom below threshold
```

Ophir flags exceptions and documents approvals.

---

## 5. AI role

AI can materially reduce administrative burden, but authoritative calculations remain deterministic.

Good AI tasks:

- classify incoming documents for review;
- explain forecast deviations;
- summarize facility agreements with citations;
- draft accountant notes;
- identify missing evidence;
- answer 'why is this tax treatment applied?' using validated rules;
- create management narratives from deterministic metrics.

Bad AI tasks:

- invent tax codes;
- post unsupported journal entries;
- decide regulatory classification without rule/evidence;
- execute treasury actions;
- silently change policies.

---

## 6. Belgian legal/professional boundary

Automating accounting/tax work creates professional-perimeter and liability questions.

Safest v1 architecture:

```text
Ophir calculates/prepares
 -> validation status visible
 -> company/accountant reviews where required
 -> company/professional files/posts
```

The rules engine distinguishes:

- public-source research;
- professionally reviewed;
- counsel validated;
- needs review.

Ophir should not claim filing-grade certainty where validation is absent.

---

## 7. Competitive risk

This is a crowded space:

- ERP/accounting suites;
- TMS vendors;
- reconciliation tools;
- tax software;
- audit tools;
- consultants/accountants;
- RPA/AI automation.

Therefore 'automate treasury admin' is not a sufficient wedge.

Potential differentiation:

> **One evidence graph connecting the economic treasury decision to bank evidence, legal entity, tax rule, accounting treatment and realized outcome.**

The value is strongest when bundled with Ophir's optimization engine.

---

## 8. Product metric: realized value ledger

Ophir should track not only recommendations but realized economic value:

```text
Opportunity identified
Action approved externally
Execution observed
Expected value
Actual value
Tax/fees
Accounting completed
Evidence complete
```

Example:

```text
Revolver repayment opportunity
Expected annual saving             €131,580
Executed                           4 Sep 2026
Actual average balance reduction   €3.2m
Realized Q4 saving                 €31,440
Accounting                         complete
Tax review                         complete
Evidence                           complete
```

This makes ROI visible and supports value-based pricing.

---

## 9. €100K verdict

`CORE PLATFORM CAPABILITY / SECONDARY STANDALONE WEDGE`

It can create €100k+ value in complex organizations, but the standalone economic case is less clean than debt/cash, receivables or high-volume FX.

Its strategic importance is larger than its standalone ranking because it:

- reduces implementation friction for every other module;
- makes recommendations operationally usable;
- creates regulatory/accounting moat;
- records realized customer ROI;
- increases switching costs;
- enables one-founder/AI-assisted servicing of complex customers.

---

## 10. Market validation

Measure at target companies:

- treasury FTEs;
- finance/accounting FTE time spent on treasury;
- number of bank accounts/entities;
- TMS/ERP stack;
- monthly reconciliation hours;
- forecast preparation hours;
- annual audit support hours;
- external treasury/tax/accounting adviser spend;
- number of manual tax filings related to treasury instruments;
- number/value of errors or late filings;
- time to produce management treasury report;
- number of spreadsheets/manual registers.

### Promote as standalone wedge if

A target segment shows >€150k/year recurring manual/external treasury administration cost with >50% realistically automatable.

### Otherwise

Keep as the horizontal operating layer around higher-value optimization modules.
