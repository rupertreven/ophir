# Spiko Belgian Instrument Dossiers v0

> Status: `PUBLIC_SOURCE_RESEARCH` — not filing-grade.  
> Date: 28 August 2026.  
> Purpose: narrow the exact Belgian tax/accounting questions for Ophir's first two reference instruments.

## Executive finding

Public evidence now strongly suggests a potentially decisive fact for the initial €2m / 92-day use case:

- both reference share classes are **accumulating shares of a French SICAV**;
- Belgian official/public investor guidance states that subscription to a non-listed SICAV is not subject to TOB, while redemption of accumulating SICAV shares is generally subject to **1.32% TOB capped at €4,000 per transaction**;
- Belgian TOB rules apply to Belgian legal persons placing orders with foreign professional intermediaries where the tax is not otherwise paid;
- therefore a €2m redemption may face a €4,000 TOB cost if the general accumulating-SICAV redemption rule applies to the exact Spiko path.

This is not yet professional validation, but it is strong enough that Ophir must treat the €4,000 redemption TOB as the **base research hypothesis**, not as a remote sensitivity.

That single cost can erase the gross 92-day yield advantage of the EU T-Bills fund versus the current public Belgian term-deposit benchmark.

---

# Dossier A — Spiko EU T-Bills Money Market Fund

## Identity

- ISIN: `FR001400ODL1`
- Currency: EUR
- Legal vehicle: SPIKO SICAV, French-law SICAV
- UCITS: yes
- AMF classification: short-term VNAV money-market fund
- Income: accumulating / capitalization
- Minimum subscription: €1 according to current Spiko data/prospectus
- Current 30-day annualised yield (28 Aug snapshot, NAV dated 27 Aug): 2.13%
- Current AUM: ~€773m
- Management fee shown by Spiko data: 0.25%
- Subscription fee: 0%
- Redemption fee: 0%
- NAV: daily
- Benchmark/reference: capitalised €STR
- Investment objective/mandate: short-duration euro-area sovereign treasury-bill exposure under MMF rules
- Depositary/accounting partner described by Spiko: CACEIS

## Belgian TOB — current research hypothesis

### Subscription

Belgian public guidance distinguishes primary subscription from secondary-market acquisition. For non-listed SICAV shares, subscription is generally shown as **0% TOB**.

Working rule:

`SUBSCRIPTION_TOB = 0` subject to professional confirmation that the Spiko subscription is legally a primary issuance/subscription and no unusual transfer mechanism changes the treatment.

Status: `PUBLIC_SOURCE_RESEARCH`.

### Redemption

The share class is accumulating. Belgian federal guidance expressly includes redemption by an investment company of its accumulating shares among TOB-covered operations. Wikifin/public Belgian schedules show redemption/sale of non-listed accumulating SICAV shares at **1.32%, capped at €4,000 per transaction**.

Working rule:

`REDEMPTION_TOB = min(redemption_value * 1.32%, 4000 EUR)`

For €2,000,000:

- raw 1.32% = €26,400;
- statutory cap = €4,000;
- working TOB hypothesis = **€4,000**.

Status: `PUBLIC_SOURCE_RESEARCH — HIGH PRIORITY PROFESSIONAL VALIDATION`.

### Foreign intermediary

Belgian TOB guidance treats an order as concluded/executed in Belgium where a Belgian legal person for a Belgian establishment gives the order directly or indirectly to a foreign professional intermediary. The Belgian investor may need to declare/pay if the intermediary does not do so.

Ophir must establish whether Spiko or its chain handles Belgian TOB. Until then:

`TOB_COLLECTION_PARTY = UNKNOWN`.

## Belgian annual tax on securities accounts

Potentially applicable if the actual holding constitutes a taxable securities account and average value exceeds €1m. Exact Spiko custody/register/account architecture must be mapped before any amount is calculated.

Status: `NEEDS_REVIEW`.

## Corporate income tax

Working hypothesis for a normal Belgian company subject to corporate income tax:

- realised fund gain is taxable unless a specific exemption applies;
- this money-market SICAV is not being treated as a DBI/RDT fund in the current research model;
- standard corporate tax rate assumption in the model: 25%;
- transaction/acquisition/disposal costs may affect accounting/tax result depending on treatment;
- do not apply the new private capital-gains regime intended for individuals to an ordinary Belgian company already within corporate income tax.

Status: `NEEDS PROFESSIONAL REVIEW`.

## Belgian accounting — working model

Public Belgian accounting examples for SICAV holdings use current-investment accounts in class 51, with financial costs and realised gains/losses in financial result accounts.

Candidate lifecycle:

### Subscription

```text
Dr 51 Financial investments / shares      acquisition value
Dr 65 Financial costs                     if expensed
Cr 55 Bank                                cash paid
```

### Redemption with gain

```text
Dr 55 Bank                                proceeds
Cr 51 Financial investments               carrying/acquisition value
Cr 752 Gain on disposal current assets     realised gain
```

Exact PCMN/MAR account choice and treatment of acquisition/TOB costs require accountant validation.

Status: `PUBLIC_SOURCE_RESEARCH`.

---

# Dossier B — Spiko Smart Cash EUR

## Identity

- ISIN: `FR0014015LD3`
- Currency: EUR
- Vehicle/share class within SPIKO SICAV prospectus
- UCITS
- Income: accumulating / capitalization
- Minimum subscription: €1
- Current 30-day annualised yield (28 Aug snapshot, NAV dated 27 Aug): 2.57%
- Current AUM: ~€1.01bn
- Management fee shown by Spiko data: 0.25%
- Subscription fee: 0%
- Redemption fee: 0%
- Reference index: capitalised €STR + 0.50%
- Current product description: total-return-swap strategy with Tier-1 bank exposure/collateral structure

## Belgian TOB — working hypothesis

Because this is also an accumulating share of the French SICAV, the same general Belgian accumulating-SICAV framework appears relevant:

- subscription: working hypothesis 0% TOB;
- redemption: working hypothesis 1.32%, capped at €4,000 per transaction.

However, **do not automatically inherit a production rule from the T-Bills dossier**. The exact share-class/provider path must be professionally confirmed separately.

Status: `PUBLIC_SOURCE_RESEARCH — HIGH PRIORITY PROFESSIONAL VALIDATION`.

## Other tax/accounting items

TACT, corporate-income-tax treatment, withholding mechanics and Belgian accounting remain `NEEDS_REVIEW`, separately from the T-Bills fund.

---

# Impact on the €2m / 92-day reference case

## Inputs

- Principal: €2,000,000
- Period: 92 days
- Public Belgian term-deposit benchmark: 1.65% p.a.
- EU T-Bills current 30d annualised yield: 2.13%
- Smart Cash current 30d annualised yield: 2.57%
- Simple day-count model: 92 / 365
- Standard corporate-income-tax model assumption: 25%

## Gross returns

Approximate:

- Deposit: €8,318
- EU T-Bills: €10,740
- Smart Cash: €12,951

Gross uplift vs deposit:

- EU T-Bills: +€2,422
- Smart Cash: +€4,633

## Provisional TOB-adjusted insight

If the 1.32% capped redemption rule is confirmed:

- subscription TOB: €0 working hypothesis;
- redemption TOB: €4,000 on a €2m redemption.

Therefore, before even resolving TACT and exact CIT/accounting mechanics:

- EU T-Bills gross uplift of ~€2,422 is **smaller than the €4,000 redemption TOB**;
- Smart Cash gross uplift of ~€4,633 is only ~€633 above the redemption TOB before corporate tax and other differences.

This materially weakens a short 92-day 'yield arbitrage' pitch.

### Illustrative post-CIT sensitivity

If, purely for modelling, the €4,000 disposal tax is treated as a deductible transaction cost and the remaining economic profit is taxed at 25%:

- EU T-Bills economic profit before CIT ≈ €10,740 - €4,000 = €6,740;
- after 25% CIT ≈ €5,055;
- deposit after 25% CIT ≈ €6,239;
- indicative difference ≈ **-€1,184** versus deposit.

This is **not a certified tax calculation**; deductibility/timing must be professionally validated. It demonstrates why Ophir needs instrument-specific Belgian tax intelligence.

For Smart Cash under the same illustrative assumptions:

- economic profit before CIT ≈ €12,951 - €4,000 = €8,951;
- after 25% CIT ≈ €6,713;
- deposit after CIT ≈ €6,239;
- indicative difference ≈ **+€474**.

Again, TACT and other effects are excluded.

## Product implication

For short holding periods, the financial case may **not** be 'tokenized funds yield more'. A capped exit tax creates a fixed-cost effect that favours:

- larger balances;
- longer holding periods;
- fewer redemptions;
- products/legal structures with better Belgian tax treatment;
- conventional bank deposits when the expected idle period is short.

This is exactly the type of conclusion Ophir should calculate automatically rather than promoting a preferred rail.

---

# Break-even engine requirement

Ophir should calculate the minimum holding period at which each alternative beats the customer's bank quote after:

- product yield;
- fees;
- subscription/redemption tax;
- corporate income tax;
- TACT where applicable;
- operational costs;
- liquidity requirements.

Example UI concept:

```text
€2,000,000 surplus cash
Bank quote: 1.65%
EU T-Bills yield: 2.13%
Estimated exit TOB: €4,000 [research status]

Break-even holding period: [calculated after validation]

90 days     Bank likely superior
180 days    ...
365 days    ...

Reason: fixed redemption tax outweighs yield spread at short horizons.
```

This may be more valuable to a CFO than simply displaying the highest annualised yield.

---

# Sources / evidence classes

Primary/high-authority sources to preserve in the eventual machine-readable dossier:

1. Spiko SICAV official prospectus — legal form, share classes, accumulation, investor eligibility.
2. Spiko official data API/pages — current NAV/yield/AUM/fees.
3. Belgian FPS Finance — TOB taxable operations, foreign intermediary nexus, rates/caps and filing mechanics.
4. Wikifin/FSMA public investor guidance — TOB matrix for SICAV/FCP structures.
5. Belgian Accounting Standards Commission / professional accountant validation for final accounting rules.

Secondary professional sources may triangulate treatment but must not replace primary authority in production rules.

---

# Remaining blockers

1. Confirm exact TOB classification with Belgian tax professional for both ISINs.
2. Confirm whether Spiko/intermediary collects Belgian TOB or customer self-files.
3. Map exact legal custody/register architecture and TACT consequences.
4. Confirm CIT treatment and deductibility/timing of TOB and related costs.
5. Confirm Belgian GAAP/MAR entries.
6. Determine whether alternative fund structures (especially FCP/non-SICAV structures) can deliver comparable money-market exposure with materially better Belgian TOB economics.
7. Compare against traditional Belgian/European MMFs and real €2m bank quotes.

The sixth item is now strategically important: **the best Ophir product may be the fund structure with the best after-tax Belgian treasury economics, not the fund with the highest headline yield.**
