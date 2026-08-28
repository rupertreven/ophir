# FCP / Belgian-Efficient Cash Instrument Search Sprint v1

> **Date:** 2026-08-28 23:16 CEST  
> **Status:** Active research sprint  
> **Evidence level:** `PUBLIC_SOURCE_RESEARCH` / candidate discovery

## Objective

Find regulated EUR short-term cash instruments that can be economically superior for a Belgian corporation after Belgian tax, fees, liquidity and administrative burden — with priority on contractual/FCP or other wrappers that may avoid the short-horizon TOB drag identified in capitalisation SICAV shares.

## Search criteria

A high-quality candidate should satisfy as many as possible:

1. EUR denominated;
2. MMF / short-duration government or high-grade cash strategy;
3. EU/EEA regulated;
4. accessible to Belgian corporate investors;
5. legal wrapper with favourable Belgian TOB treatment;
6. daily liquidity, ideally T+0/T+1;
7. competitive net-of-product-fee yield;
8. low/minimal subscription/redemption fees;
9. API, embedded, digital dealing or machine-readable position data;
10. tokenized/DLT representation preferred but not required;
11. stablecoin settlement optional bonus;
12. custody/account structure whose Belgian TACT impact is understood/manageable;
13. sufficient documentation to automate Belgian tax/accounting treatment.

## Candidate categories

### Category A — contractual/FCP MMFs
Highest priority because Belgian TOB treatment may differ materially from capitalisation SICAV shares. Must separately model fiscal transparency and underlying-income reporting burden.

### Category B — distributing SICAV/share classes
Investigate whether distribution structure changes redemption TOB/tax economics enough to outperform accumulating capitalisation shares.

### Category C — Irish contractual/unit-trust/common-contractual structures
Investigate exact legal form and Belgian classification. Do not infer treatment from domicile alone.

### Category D — direct short-term government securities / tokenized government debt
Compare direct instrument transaction tax, custody, minimum ticket, liquidity and accounting with MMFs.

### Category E — bank/tokenized deposits
Potentially simpler tax/accounting treatment and no fund-wrapper friction. Investigate availability to Belgian corporates and API/programmatic access.

## Required candidate dossier fields

```text
provider
fund/instrument
isin_or_identifier
legal_wrapper
fund_domicile
currency
accumulating_or_distributing
Belgian_corporate_eligible
regulatory_status
strategy
current_yield
as_of_date
fees
minimum_ticket
subscription_liquidity
redemption_liquidity
subscription_fee
redemption_fee
Belgian_TOB_subscription
Belgian_TOB_redemption
Belgian_TACT
Belgian_CIT
withholding
accounting_complexity
API_access
embedded_access
tokenized
stablecoin_settlement
custody_model
source_urls
validation_status
```

## Economic test

Every candidate is run through the same scenarios:

- EUR 100k / 500k / 1m / 2m;
- 30 / 92 / 180 / 365 days;
- benchmark bank rate supplied by customer or current public/negotiated quote;
- after-tax and after-transaction-cost outcome;
- break-even holding period versus bank deposit.

## Key hypothesis

A lower-yielding contractual/FCP product may beat a higher-yielding SICAV product over short horizons if Belgian transaction-tax drag is materially lower.

Example concept:

```text
SICAV headline yield     2.57%
FCP headline yield       2.25%

but

SICAV exit TOB           up to material capped amount
FCP transaction TOB      potentially much lower / absent

=> FCP can produce higher 92-day after-tax cash outcome
```

This must be proven per exact instrument; it is not a generic tax rule.

## Research questions that can invalidate FCP advantage

1. Does fiscal transparency create corporate-tax treatment that eliminates the apparent advantage?
2. Is underlying-income reporting prohibitively complex or costly?
3. Are suitable FCPs unavailable to ordinary Belgian SMEs?
4. Are minimum tickets too high?
5. Is API/digital access absent?
6. Does custody introduce TACT or other costs?
7. Do negotiated Belgian bank rates already match the after-tax outcome?

## Product consequence

If a complex but tax-efficient wrapper wins, Ophir's moat strengthens because the system can automate:

- instrument classification;
- underlying income/tax reporting;
- journal entries;
- evidence collection;
- filing instructions;
- break-even calculations.

The complexity becomes product value rather than merely friction.

## Definition of success

This sprint succeeds if it finds at least one instrument that is:

- realistically accessible to a Belgian corporation;
- daily liquid;
- economically competitive with corporate deposits;
- structurally better after Belgian tax for at least one common holding horizon;
- technically integrable or at minimum observable through reliable digital data.

Tokenization is not required for sprint success. Ophir remains rail-neutral.
