# Ophir Economic Validation v1

> Status: live-data research snapshot — 28 August 2026. Not investment, tax or legal advice. Belgian tax treatment of the specific fund share classes still requires professional validation before any production recommendation or filing output.

## Objective

Test whether regulated/tokenized treasury instruments create measurable current value for a Belgian company versus ordinary corporate cash products.

## Live market facts — 28 Aug 2026

### ECB benchmark
- €STR reference date 27 Aug 2026: **2.188%**.
- Source: ECB.

### Spiko EU T-Bills MMF — FR001400ODL1
- EUR short-term VNAV money-market fund.
- AUM: **€773.03m**.
- 30-day annualised yield: **2.13%**.
- 7-day annualised yield: **2.08%**.
- Management fee: **0.25%**; displayed yield is net of fund fees.
- Subscription fee: **0%**.
- Redemption fee: **0%**.
- Minimum subscription: **€1**.
- Reference index: capitalised €STR.
- Accumulating share class.
- Spiko states withdrawals are processed daily; up to €500k/day can use instant SEPA, including weekends; larger withdrawals follow normal daily processing, generally T+1 when before cut-off.

### Spiko Smart Cash EUR — FR0014015LD3
- EUR UCITS, AMF-regulated.
- AUM: **€1.01bn**.
- 30-day annualised yield shown by Spiko data: **2.57%**.
- Reference index: capitalised €STR + 0.50%.
- Management fee: **0.25%**.
- Subscription/redemption fee: **0%**.
- Minimum subscription: **€1**.
- Strategy uses a Total Return Swap with a Tier-1 bank; BNP Paribas is identified as primary counterparty, with a securities portfolio held by the fund/custodian.
- This is economically different from a government T-bill MMF and should carry a different risk classification in Ophir.

### Public Belgian corporate term-deposit benchmark
Triodos Belgium published on 27 Aug 2026:
- 3 months: **1.65% gross annual rate**.
- The product page shows 1.16% net annual / 0.291% over three months after 30% withholding for its displayed example.

KBC offers corporate EUR term accounts from 1–11 months and Termijndeposito PRO from 7–364 days, but does not publish the live corporate rate publicly; customers must request the current quote. This is important: Ophir needs a customer-specific bank-quote input/API/manual capture rather than pretending public web rates represent the customer's best bank offer.

## Worked scenario — €2m surplus for 3 months

For comparability use 92 days, matching the current Triodos three-month example. Assume yields remain constant for illustration. Actual fund yields float daily and are not guaranteed.

### Gross / pre-Belgian-tax economics

Formula: `principal × annualised yield × 92 / 365`.

| Option | Current annualised rate/yield | Approx. 92-day gross return | Liquidity characteristic |
|---|---:|---:|---|
| Triodos corporate term deposit | 1.65% | €8,318 | locked to maturity / early-exit constraints |
| Spiko EU T-Bills MMF | 2.13% | €10,740 | daily; instant SEPA up to €500k/day under current Spiko feature, larger normal redemption processing |
| Spiko Smart Cash EUR | 2.57% | €12,951 | daily liquidity; different TRS/counterparty risk profile |

Gross incremental return over the public Triodos benchmark:
- EU T-Bills: **~€2,422** over 92 days.
- Smart Cash EUR: **~€4,633** over 92 days.

### Illustrative corporate-tax normalisation

Belgian corporate cash investment comparisons must be done on final corporate-tax economics, not simply the cash withholding shown on a bank website. A Belgian accounting/tax source notes that 30% withholding on term-deposit interest is creditable against corporate income tax, with the underlying interest ultimately taxed at the applicable corporate rate. Assuming a 25% corporate income-tax rate purely for comparison:

| Option | Approx. gross 92d return | Illustrative after-25%-tax return* |
|---|---:|---:|
| Triodos term deposit | €8,318 | €6,238 |
| Spiko EU T-Bills | €10,740 | €8,055 |
| Spiko Smart Cash | €12,951 | €9,713 |

Illustrative uplift after a common 25% income-tax assumption:
- EU T-Bills vs term deposit: **~€1,817**.
- Smart Cash vs term deposit: **~€3,475**.

`*` This is NOT yet the validated Belgian tax result for the Spiko share classes. It merely applies the same 25% income-tax haircut to isolate the economic spread. The actual Belgian fund tax/TOB/accounting treatment must be validated instrument-by-instrument.

## Why TOB can change the answer completely

Belgian FPS Finance states that Belgian legal persons can themselves become liable for TOB when transactions are executed for them by a foreign professional intermediary unless they can prove TOB was paid. Official TOB rates are 0.12%, 0.35% or 1.32%, depending on the transaction/instrument, with statutory caps.

Therefore Ophir must never show the €1,817 / €3,475 uplift above as a final net benefit until the exact share-class treatment is known.

Sensitivity example on a €2m transaction:
- 0.12% uncapped arithmetic = €2,400, but the current statutory cap for that rate is €1,300 per operation.
- 0.35% arithmetic = €7,000, capped at €1,600 per operation.
- 1.32% arithmetic = €26,400, capped at €4,000 per operation.

If TOB applied both on entry and exit, even capped amounts could erase a meaningful part or all of a three-month yield advantage. The exact applicability/rate to subscriptions/redemptions of each supported fund is therefore a **go/no-go data field**, not a footnote.

## Securities-account tax

FPS Finance states that the annual tax on securities accounts increased to **0.30%** for relevant reference periods after the 2026 change. Applicability depends on the legal/account structure and average taxable value. A €2m corporate investment can therefore cross thresholds where account structuring/tax treatment materially affects the economics. This requires instrument/account-specific legal validation before inclusion in Net Treasury Benefit.

## Tokenization: what is the concrete current benefit?

The yield itself is not created by tokenization. The underlying regulated fund strategy creates the yield.

Current operational benefits evidenced by Spiko include:
1. API-accessible positions, transactions, NAV and yield data.
2. Embedded distribution model for treasury SaaS providers; Spiko can act as the regulated investment firm while an unregulated SaaS acts as business introducer.
3. Tokenized fund shares / digital rails usable in web3-oriented workflows.
4. EURC/USDC subscription and redemption for supported products without a conventional bank on/off-ramp in the middle.
5. High-frequency, machine-readable reconciliation and accounting data.
6. Instant EUR redemption feature up to €500k/day via instant SEPA for supported EUR products, including weekends.

The strongest near-term benefit for a normal Belgian SME may therefore be **liquidity + automation + administrative integration**, not a magical tokenization yield premium.

## Example Ophir proposal screen

```text
OPHIR — SURPLUS CASH SCENARIO
Entity: Belgian Operating BV
Surplus cash:                         €2,000,000
Expected unused horizon:                  92 days
Required availability:                 daily

LIVE MARKET SNAPSHOT (28 Aug 2026)

Option A — Corporate term deposit (public benchmark)
Provider benchmark: Triodos
Rate:                                      1.65%
Est. 92d gross return:                    €8,318
Liquidity:                         locked / term

Option B — EU T-Bills MMF
Instrument: Spiko FR001400ODL1
30d annualised yield:                       2.13%
Est. 92d gross return:                   €10,740
Gross uplift vs benchmark:                €2,422
Liquidity:                            daily / T+1
Instant EUR:                  up to €500k/day*

Option C — Smart Cash EUR
Instrument: Spiko FR0014015LD3
30d annualised yield:                       2.57%
Est. 92d gross return:                   €12,951
Gross uplift vs benchmark:                €4,633
Liquidity:                                  daily
Risk note:             TRS / bank counterparty layer

BELGIAN TAX & ACCOUNTING
Corporate income tax:          calculation pending/known
TOB:                           NEEDS VALIDATION
Securities-account tax:        NEEDS VALIDATION
Accounting classification:     NEEDS VALIDATION

STATUS
⚠ Net Treasury Benefit cannot yet be certified.
Reason: exact Belgian tax treatment of selected share class not validated.

[View sources] [Send to accountant] [Prepare provider handoff]
```

This is intentionally better than a fake recommendation. Ophir exposes when it does **not yet know enough** to call the trade economically superior.

## What Ophir must collect next

### Bank benchmark dataset
For real customer proposals capture:
- current-account remuneration;
- 1m/3m/6m corporate term quote;
- negotiated rate for the customer's balance tier;
- early-withdrawal rules;
- bank concentration/deposit-guarantee exposure.

### Fund dataset
For every candidate share class:
- exact Belgian TOB treatment on subscription/redemption;
- Belgian corporate income-tax treatment;
- securities-account-tax treatment;
- withholding/source-tax treatment;
- Belgian GAAP classification and valuation;
- settlement/redemption cut-offs;
- instant-liquidity limits;
- risk classification;
- API capabilities;
- whether tokenized share transfer/collateral use is actually available to the target SME.

### Benchmark methodology
Ophir should compare at least:
- customer-specific bank quote;
- traditional EUR MMF accessible through a conventional broker/bank;
- tokenized regulated MMF;
- tokenized Smart Cash-like product where risk differs;
- EURC only when settlement/programming value is relevant (EURC itself should not be treated as yield-bearing).

## Current preliminary conclusion

On live 28 Aug 2026 public data, regulated Spiko products show a **gross yield advantage of roughly 48–92 bps** over one publicly quoted Belgian three-month corporate term deposit benchmark, while also offering daily rather than three-month locked liquidity.

For €2m over 92 days, that is approximately **€2.4k–€4.6k gross incremental return** before Belgian tax/accounting effects. This is economically real but not enormous. It becomes more compelling when combined with liquidity, bank-risk diversification, API automation and reduced finance-team administration.

The Belgian tax treatment can easily dominate a short three-month spread, so instrument-level tax validation is the immediate next research priority.

## Sources snapshot
- ECB €STR page, update 28 Aug 2026.
- Spiko Public API/data pages for FR001400ODL1 and FR0014015LD3, data through 27 Aug 2026.
- Spiko SME/Web3/technical documentation for liquidity, stablecoin and embedded API features.
- Triodos Belgium business term-account rate page, rates effective 27 Aug 2026.
- KBC business term-account page.
- Belgian FPS Finance TOB and DivTax pages.
- SBB corporate cash-surplus tax explainer used only for the illustrative corporate-tax normalisation; formal tax conclusions remain to be validated.
