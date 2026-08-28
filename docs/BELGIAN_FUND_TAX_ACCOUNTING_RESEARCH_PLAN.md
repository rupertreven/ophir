# Belgian Fund Tax & Accounting Research Plan

> Status: active research workstream
> Priority: highest current economic-validation blocker

## Objective

Turn Ophir's indicative gross-return comparison into a defensible **Belgian corporate Net Treasury Benefit** calculation.

The first two reference instruments are:

- Spiko EU T-Bills Money Market Fund — ISIN `FR001400ODL1`
- Spiko Smart Cash EUR — ISIN `FR0014015LD3`

The benchmark universe must also include Belgian corporate term deposits and comparable traditional/non-tokenized EUR money-market products.

## Why this matters

At current public figures, a €2m / 92-day example shows only a few thousand euros of gross uplift versus a publicly quoted Belgian corporate term deposit. Transaction taxes, securities-account taxes, withholding mechanics, corporate income tax treatment or accounting burden can therefore materially change — or even reverse — the economic conclusion.

Ophir must never show a 'net benefit' until all material applicable Belgian rules have been validated for the exact investor + instrument + transaction path.

## Research matrix per instrument

### 1. Legal/product classification
- exact legal fund/share-class structure;
- UCITS/MMF classification;
- domicile;
- accumulating/distributing;
- registered/marketed availability for Belgian corporate investors;
- tokenized ownership/settlement mechanics;
- distributor/investment-firm chain;
- securities-account/custody structure.

### 2. Subscription
Determine:
- whether Belgian TOB applies;
- applicable rate and cap;
- who is legally liable;
- whether foreign intermediary/provider collects it;
- whether Belgian company must self-declare/pay;
- exact declaration/form/field/payment process;
- whether EURC subscription changes any tax treatment;
- accounting recognition and initial measurement;
- documentary evidence required.

### 3. Holding period
Determine:
- corporate income-tax treatment of return/NAV increase;
- withholding-tax mechanics, if any;
- year-end valuation under Belgian GAAP;
- unrealised gain/loss treatment;
- accrued income treatment;
- annual tax on securities accounts applicability and account aggregation mechanics;
- reporting obligations;
- evidence needed for audit/accountant.

### 4. Redemption
Determine:
- whether TOB applies;
- rate/cap;
- realised gain/income characterization;
- withholding mechanics;
- corporate-income-tax base;
- accounting derecognition;
- treatment of fees;
- exact filing obligations;
- EUR versus stablecoin redemption differences.

### 5. Corporate tax
Build the actual tax bridge:

```text
Gross fund return
- product/transaction costs
+/- Belgian accounting/tax adjustments
- final Belgian corporate income tax impact
- transaction taxes
- securities-account tax attributable to scenario, if applicable
= after-tax cash benefit
```

Do not double-count withholding tax that is creditable against corporate income tax.

### 6. Belgian accounting
For every economic event document:
- Belgian GAAP classification;
- relevant Minimum Chart of Accounts mapping candidates;
- acquisition entry;
- valuation entry;
- income entry;
- redemption entry;
- realised gain/loss;
- supporting documents;
- accountant validation status.

## Comparison scenarios

Calculate consistently for:
- €100k / €500k / €1m / €2m;
- 30 / 90-92 / 180 / 365 days;
- normal bank-day liquidity need;
- weekend liquidity need;
- bank deposit vs traditional MMF vs tokenized MMF;
- fund subscription/redemption through fiat versus stablecoin rails where supported.

## Current reference scenario

€2,000,000 for 92 days.

Publicly observed rates/yields used in the initial 28 Aug 2026 snapshot:
- Belgian corporate 3-month term-deposit example: 1.65% p.a.;
- Spiko EU T-Bills 30-day annualised yield: 2.13%;
- Spiko Smart Cash EUR 30-day annualised yield: 2.57%.

Indicative simple-return results before instrument-specific Belgian tax validation:
- deposit: ~€8.3k gross;
- EU T-Bills: ~€10.7k gross;
- Smart Cash: ~€13.0k gross.

At a simple 25% corporate-income-tax assumption alone, the EU T-Bills uplift versus the deposit is roughly €1.8k after corporate tax. This is **not** an Ophir-certified net result because TOB, securities-account tax and exact fund tax/accounting treatment remain unresolved.

## Output required from this workstream

For each supported share class, create a machine-readable 'Belgian instrument dossier' containing:

```text
instrument_id
isin
legal_classification
fund_domicile
corporate_eligibility_BE
subscription_tax_rules[]
holding_tax_rules[]
redemption_tax_rules[]
securities_account_tax_rules[]
corporate_income_tax_rules[]
accounting_rules[]
filing_obligations[]
required_documents[]
source_references[]
effective_dates[]
validation_status
professional_reviewer
last_reviewed_at
```

## Validation standard

Three evidence levels:

1. `PUBLIC_SOURCE_RESEARCH` — sourced research, not filing-grade.
2. `PROFESSIONAL_REVIEWED` — Belgian accountant/tax professional has reviewed the treatment.
3. `COUNSEL_VALIDATED` — legal/regulatory perimeter validated where needed.

Ophir UI must expose the validation level. A tax amount must not be presented as filing-grade when only level 1 exists.

## Immediate next actions

1. Obtain current prospectus/KID/share-class documents for both Spiko ISINs.
2. Determine exact Belgian TOB treatment for subscription and redemption of each share class.
3. Determine whether/how annual securities-account tax can apply to the actual holding/custody structure.
4. Determine corporate-income-tax and withholding treatment.
5. Draft Belgian GAAP journal entries and have them professionally reviewed.
6. Identify exact Belgian forms/codes/deadlines for any self-declared tax.
7. Recalculate the €2m / 92-day scenario with all validated taxes/costs.
8. Repeat against at least three realistic Belgian bank corporate deposit quotes, because public website rates are an imperfect benchmark for €2m corporate treasury.
9. Compare with at least two traditional/non-tokenized EUR MMFs to isolate the economic value of tokenization itself.

## Decision criterion

The product thesis is strengthened if Ophir can show one or more of:
- persistent after-tax yield advantage;
- materially better liquidity for comparable risk;
- lower administrative/accounting/tax burden through automation;
- measurable value from 24/7 settlement/programmatic rails;
- improved diversification/counterparty management;
- enough combined annual customer value to support attractive SaaS pricing.

If the fund advantage disappears after tax and administration, Ophir should remain rail-neutral and recommend/compare conventional bank products rather than force tokenized instruments.
