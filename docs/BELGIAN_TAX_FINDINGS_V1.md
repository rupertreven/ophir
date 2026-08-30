# Belgian Tax Findings v1

> Status: public-source research; not filing-grade legal/tax advice.
> Date: 28 August 2026.
> Scope: initial Belgian corporate treatment questions relevant to Ophir's regulated fund use case.

## Principle

Every material finding is written to Git. This file records the current evidence separately from the research plan so unresolved points are visible and cannot accidentally be treated as validated rules.

## 1. Annual tax on securities accounts (TACT)

Belgian federal tax guidance currently states that the annual tax on securities accounts applies when the average value of taxable financial instruments held on a securities account exceeds EUR 1,000,000. Legal persons are within scope. The rate is 0.30% under the 2026 regime.

For a foreign intermediary without the relevant Belgian fiscal representation/collection arrangement, filing/payment obligations can fall on the account holder.

### Ophir consequence

A EUR 2m corporate fund position cannot be modelled by simply subtracting `0.30% × EUR 2m` without first establishing:

- whether the Spiko holding is legally held on a securities account for Belgian TACT purposes;
- which account/intermediary is relevant;
- the average taxable value over the statutory reference period;
- aggregation/account structure;
- whether the intermediary handles Belgian tax;
- the precise holding duration and valuation dates.

**Status:** applicability to the actual Spiko custody/account structure = `NEEDS_REVIEW`.

## 2. Belgian tax on stock-exchange transactions (TOB)

Belgian federal guidance confirms that a Belgian resident/legal person can have a TOB declaration/payment obligation for transactions executed through a foreign professional intermediary when the tax has not otherwise been paid.

Current headline rate/cap categories include:

- 0.12%, capped at EUR 1,300 per transaction;
- 0.35%, capped at EUR 1,600 per transaction;
- 1.32%, capped at EUR 4,000 per transaction.

The applicable category depends on the exact instrument and transaction. Purchase/sale and certain redemptions of investment-company/capitalisation shares require specific classification.

### Ophir consequence

For each supported fund share class we must determine independently:

1. TOB on subscription/acquisition;
2. TOB on redemption;
3. applicable rate and cap;
4. taxpayer/intermediary responsibility;
5. whether Spiko/another intermediary withholds/remits Belgian TOB;
6. whether the Belgian company must self-declare;
7. exact filing deadline/form/payment mechanics.

No generic `fund = 0.12%` rule is acceptable.

**Status for FR001400ODL1:** `NEEDS_REVIEW`.

**Status for FR0014015LD3:** `NEEDS_REVIEW`.

## 3. DivTax / filing workflow opportunity

Belgian federal tax administration provides electronic workflows through MyMinfin/DivTax for relevant taxes including TOB and the annual tax on securities accounts. Mandate mechanisms exist for professional representatives.

### Product implication

A conservative Ophir workflow can be:

```text
Ophir detects taxable event
 -> deterministic calculation from validated rule
 -> prepares filing-ready declaration data/document
 -> accountant/tax professional reviews
 -> professional/customer files through official Belgian channel
 -> filing/payment evidence returned to Ophir
 -> obligation marked FILED_EXTERNALLY / PAID
```

This is strategically preferable to Ophir becoming the customer's tax representative in v1.

Potential future integration should investigate whether machine-readable export/import or professional workflow automation is available around DivTax/MyMinfin, while respecting official authentication/mandate boundaries.

## 4. Current EUR 2m / 92-day case

Current indicative public-data scenario:

- corporate term-deposit benchmark: 1.65% p.a.;
- Spiko EU T-Bills: 2.13% annualised 30-day yield;
- Spiko Smart Cash EUR: 2.57% annualised 30-day yield.

Approximate gross 92-day returns:

- deposit: EUR 8.3k;
- EU T-Bills: EUR 10.7k;
- Smart Cash: EUR 13.0k.

EU T-Bills gross uplift vs deposit: about EUR 2.4k.

Applying only a simple 25% Belgian corporate-income-tax assumption gives an indicative uplift of about EUR 1.8k after corporate tax. This is **not a certified net benefit**.

### Why certification is blocked

The following remain unresolved for the exact share class/holding structure:

- TOB subscription treatment;
- TOB redemption treatment;
- TACT applicability and attributable amount;
- withholding-tax mechanics;
- exact corporate-income-tax treatment;
- Belgian GAAP classification/valuation;
- provider/intermediary Belgian tax handling.

Because the gross uplift is only a few thousand euros over 92 days, any material transaction/account tax can erase the advantage. This is therefore not a peripheral tax question; it is a product/business-case gating variable.

## 5. Next exact questions

### FR001400ODL1 — Spiko EU T-Bills

- legal form and exact share-class characteristics;
- Belgian registration/availability;
- subscription TOB category;
- redemption TOB category;
- whether accumulation/redemption characteristics affect rate;
- custody/securities-account structure for a Belgian corporate investor;
- TACT treatment;
- withholding/corporate-tax treatment;
- Belgian GAAP entries.

### FR0014015LD3 — Spiko Smart Cash EUR

Same questions, separately. Do not infer treatment from the T-Bills fund merely because both are Spiko products.

## 6. Source set to preserve in instrument dossiers

Primary/public sources currently used in this workstream include:

- Belgian Federal Public Service Finance — TOB guidance and rate/cap information;
- Belgian Federal Public Service Finance — annual tax on securities accounts / DivTax guidance;
- Belgian Federal Public Service Finance — mandate/e-services information;
- Spiko official fund data/product documentation for instrument facts.

Every production rule will ultimately store exact source URL/reference, retrieved/effective date, validation status and reviewer.

## 7. Rule-engine safety requirement

Until professional validation is complete, these findings must map to rule status `PUBLIC_SOURCE_RESEARCH` or `NEEDS_REVIEW`, never `PROFESSIONAL_REVIEWED` or `COUNSEL_VALIDATED`.

The UI must therefore say, for example:

> Indicative post-CIT benefit: +EUR 1.8k. Belgian transaction/account taxes pending validation. Certified Net Treasury Benefit unavailable.

rather than presenting a false precise net return.
