# The €100K Treasury Problem Sprint

> **Date:** 2026-08-28 23:58 CEST  
> **Status:** Active strategic validation sprint  
> **Evidence level:** hypothesis until individually researched

## Objective

Stop optimizing around elegant technology or small basis-point gains. Identify corporate treasury problems that plausibly cost a Belgian mid-market or large company **€100,000–€1,000,000+ per year**, then determine whether Ophir's existing intelligence architecture and/or regulated tokenized infrastructure can materially improve them.

## Core question

> **Which treasury problems are expensive enough that a CFO will care, and where does new digital/tokenized infrastructure create a material advantage over conventional solutions?**

Tokenization must earn its place. It is not a requirement.

## Current negative validation

Research so far has found useful but often modest economics:

- small spread improvements on €0.5–2m idle cash;
- tokenized MMFs can be neutralized by Belgian TOB depending on wrapper;
- FCP structures may reduce TOB but introduce reporting complexity and sometimes high fees;
- daily liquidity is valuable but not automatically worth six figures;
- payroll prefunding optimization for a single ~1,500-employee company appears more likely to create tens of thousands than hundreds of thousands of euros annually under ordinary assumptions;
- 24/7 settlement/programming is operationally attractive but requires a measurable cash/capital benefit to become a primary wedge.

These remain possible secondary Ophir features, but none is yet a proven killer wedge.

## €100K filter

A candidate primary use case should plausibly create at least one of:

- €100k+ annual financing-cost reduction;
- €100k+ annual working-capital release value;
- €100k+ annual FX/payment-cost reduction;
- €100k+ collateral/guarantee efficiency;
- €100k+ avoided treasury/admin/compliance labour or external-service cost;
- €100k+ avoided losses/penalties/risk cost;
- a strategic control benefit for which enterprises demonstrably pay equivalent software spend.

## Priority problem universe

### 1. Receivables / DSO optimization

Economic scale example:

```text
Revenue: €100m
DSO improvement: 5 days
Capital released: 100m × 5 / 365 ≈ €1.37m
At 5% funding cost: ≈ €68.5k/year
At 10 days: ≈ €137k/year
```

Research:
- construction/payment-cycle specifics;
- invoice approval delays;
- public-sector/project receivables;
- factoring/receivables finance;
- tokenized receivables and programmable settlement;
- whether Ophir can identify finance-vs-wait decisions without executing them.

### 2. Payables / DPO / dynamic discounting

Potential value:
- capture supplier early-payment discounts when IRR beats cash alternatives;
- extend payment timing where contractually appropriate;
- avoid paying too early due to poor treasury visibility;
- compare supply-chain-finance options.

Ophir role: identify opportunity and prepare decision; customer/provider executes.

### 3. Debt / credit-facility optimization

Examples:

```text
€20m average debt × 50 bp improvement = €100k/year
€10m × 100 bp = €100k/year
```

Research:
- unused commitment fees;
- overdraft versus revolver versus term loan;
- excess cash held while expensive debt remains outstanding;
- covenant-aware repayment decisions;
- tokenized commercial paper / digital debt for larger corporates.

### 4. FX optimization

Example:

```text
€25m annual FX flow × 40 bp avoidable spread = €100k/year
```

Research:
- bank spread opacity;
- timing/netting;
- multi-entity natural hedges;
- forward/hedging decision support;
- regulated tokenized deposits/stablecoin settlement reducing correspondent/prefunding costs;
- tax/accounting/hedge-accounting consequences.

### 5. Multi-entity cash concentration

For groups with many legal entities:
- idle cash in one entity while another draws expensive credit;
- unnecessary bank accounts;
- trapped cash;
- intercompany interest/tax/transfer-pricing constraints;
- cash-pool alternatives.

Potential six-figure value when balances/debt are large.

Tokenized deposits may eventually improve 24/7 cross-entity settlement, but Belgian corporate/tax/legal constraints must be mapped first.

### 6. Guarantees / collateral

Especially relevant to construction and infrastructure:
- bid bonds;
- performance guarantees;
- advance-payment guarantees;
- retention guarantees;
- letters of credit;
- collateral locked against guarantees;
- expiry tracking and unnecessary guarantee fees.

Potential value can come from:
- releasing collateral earlier;
- avoiding stale guarantees;
- reducing guarantee pricing;
- using eligible yield-bearing/tokenized collateral where legally/provider-supported.

### 7. Supply-chain finance

Large buyer/supplier ecosystems can create significant value through:
- approved-payables finance;
- supplier early payment;
- dynamic discounting;
- receivables finance;
- reduced supplier financing cost.

Investigate tokenized invoices/receivables only where they improve financing economics, settlement or collateral eligibility.

### 8. Tax / VAT liquidity

Research whether significant corporate balances are held conservatively for:
- VAT;
- payroll withholding;
- corporate tax prepayments;
- other statutory obligations.

Determine ownership/restrictions first. Optimize only company-owned cash that can legally be deployed.

### 9. Treasury counterparty / concentration optimization

Large uninsured bank balances create concentration risk. Potential Ophir value:
- aggregate exposure across entities/banks;
- limits;
- credit quality;
- deposit/fund diversification;
- policy alerts;
- after-tax liquidity alternatives.

Value may be risk reduction rather than direct yield; enterprise willingness-to-pay must be validated.

### 10. Treasury operations / compliance automation

Potential six-figure cost at larger groups when combining:
- bank reconciliation;
- cash forecasting;
- intercompany reconciliation;
- fund tax reporting;
- TOB/TACT workflows;
- journal entries;
- evidence/audit packs;
- instrument monitoring;
- treasury policy compliance.

Must benchmark against existing TMS products and actual finance FTE/external-adviser spend.

## Ophir boundary

Ophir remains primarily an intelligence/preparation/documentation product.

```text
Observe
 -> normalize
 -> forecast
 -> identify opportunity
 -> quantify economics
 -> legal/tax/accounting impact
 -> prepare action/instructions
 -> authorized company user decides
 -> bank/regulated provider executes
 -> Ophir reconciles/records outcome
```

No autonomous movement of customer money is required for the thesis.

For scheduled critical payments, a future provider integration may allow a user to authorize a provider-held instruction in advance. After provider acceptance, Ophir must not be a single point of failure for execution.

## Legal-tax gate

Every candidate must pass, in order:

1. **Ownership** — whose money/asset/obligation is it?
2. **Permitted use** — may the company legally optimize, invest, net, pledge or move it?
3. **Regulatory perimeter** — does Ophir remain software/information or enter regulated advice/payment/investment activity?
4. **Tax** — Belgian tax consequences and reporting.
5. **Accounting** — Belgian GAAP/IFRS and audit implications.
6. **Operational safety** — settlement/reliability/cutoff/fallback risk.
7. **Economics** — only then calculate realizable ROI.

## Validation template per problem

```text
Problem
Target company profile
Annual flow/balance at risk
Current process
Current cost/friction
Traditional best-practice solution
Tokenized/digital alternative
Direct € opportunity
Working-capital opportunity
Risk/control opportunity
Belgian legal constraints
Belgian tax/accounting constraints
Ophir role
Execution party
Data/API availability
Existing competitors
Implementation burden
Realistic annual customer value
Evidence confidence
Decision: KILL / SECONDARY / PRIORITY
```

## Research sequence

Priority order for initial deep dives:

1. guarantees/collateral — construction;
2. debt + idle cash optimization — multi-entity corporate;
3. receivables/DSO + financing — construction/mid-market;
4. FX/netting — internationally active corporate;
5. treasury operations/compliance automation;
6. supply-chain finance;
7. multi-entity cash concentration;
8. tax/VAT liquidity;
9. counterparty concentration;
10. payroll liquidity, retained as a specialist/platform case.

## Success criterion

By the end of the sprint, identify **at least two** use cases where:

- a realistic target customer has €100k+ annual economic value available;
- the value is supported by real market/company data rather than only a hypothetical percentage;
- Ophir can capture part of the value without becoming the custodian/execution venue;
- Belgian legal/tax/accounting constraints do not obviously destroy the use case;
- existing competitors leave a credible product wedge.

If none survive, reconsider Ophir's target segment or core thesis before building production software.
