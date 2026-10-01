# Belgian Candidate Fund Tax Teardown v1

> Status: public-source research / scenario analysis — not filing-grade tax advice.
> Date: 28 August 2026.
> Objective: identify regulated short-term cash instruments whose Belgian corporate after-tax economics can beat the initial Spiko SICAV example.

## 1. Executive finding

The first search did **not** yet identify a clearly superior, plug-and-play, Belgian-corporate, tokenized EUR cash fund with a proven favourable Belgian tax wrapper.

The most important finding is structural:

> **The wrapper and Belgian tax treatment can matter more over a short holding period than 50–100 bps of headline yield.**

Therefore Ophir's instrument optimizer must rank `share class + legal wrapper + investor jurisdiction + transaction path`, not merely funds or yields.

---

## 2. Candidates

### A. Spiko EU T-Bills Money Market Fund

- ISIN: `FR001400ODL1`
- French SICAV share class
- accumulating/capitalisation structure
- regulated MMF
- tokenized/digital ownership infrastructure
- public 30-day annualised yield snapshot used in current model: ~2.13%
- very low minimum and strong API/embedded integration characteristics

### B. Spiko Smart Cash EUR

- ISIN: `FR0014015LD3`
- French SICAV share class
- accumulating/capitalisation structure
- UCITS cash-management strategy
- public 30-day annualised yield snapshot used in current model: ~2.57%
- strong API/embedded characteristics

### C. Amundi Funds Cash EUR — J28 EUR DLT

- ISIN: `LU3182424617`
- Luxembourg SICAV share class
- EUR money-market fund exposure
- DLT/tokenized share class using CACEIS digital infrastructure
- public Amundi institutional data snapshot previously observed: ~2.35% 1-month annualised performance and ~2.27% 3-month annualised performance
- institutional orientation
- management fee reported around 0.03% for the DLT share class in current public material

### D. Fidelity ILF — The Euro Fund via Archax

- ISIN: `IE0003323494`
- Irish fund structure
- short-term EUR liquidity product
- Archax advertises access in traditional and tokenized form
- EUR 50k minimum in the Archax access proposition
- T+0 dealing/settlement proposition advertised by Archax
- fiat/stablecoin access supported by the platform proposition

### E. abrdn Liquidity Fund (Lux) — Euro Fund via Archax

- ISIN: `LU0966092131`
- Luxembourg fund structure
- short-term EUR liquidity product
- traditional and tokenized access advertised through Archax
- EUR 50k minimum in the platform proposition
- T+0 proposition and fiat/stablecoin rails advertised

---

## 3. Belgian TOB structural observations

Belgian public guidance distinguishes materially between fund legal forms and transaction types.

The current Spiko working hypothesis is problematic for short holding periods because the share classes are capitalisation shares of a SICAV. Public Belgian guidance indicates that primary subscription to a non-listed SICAV can have no TOB while redemption/repurchase of capitalisation shares can fall into the high TOB category, currently 1.32% with a EUR 4,000 cap per transaction.

This exact treatment still requires professional confirmation for the specific Spiko distribution/custody flow, but the cap alone is economically material for a EUR 2m / 92-day case.

### FCP observation

Belgian public investor guidance indicates a materially different TOB profile for non-listed contractual mutual funds/FCPs, with purchase/sale not treated like SICAV share transactions in the same table.

However, Belgian tax practice can treat foreign contractual funds as fiscally transparent, requiring the Belgian investor to identify and report/tax the underlying income composition. This may remove transaction-tax drag while increasing tax-accounting complexity.

This is precisely the kind of complexity Ophir could automate if the economic benefit is real.

### Current candidate problem

The tokenized EUR products found so far are not obviously the ideal FCP candidate:

- Spiko: French SICAV;
- Amundi DLT: Luxembourg SICAV;
- abrdn candidate: Luxembourg fund whose exact Belgian TOB treatment must be established from its legal form/share class;
- Fidelity Irish candidate: exact Irish legal form and Belgian treatment must be established before making any tax claim.

Therefore none is yet marked `BELGIAN_TAX_OPTIMAL`.

---

## 4. EUR 2m / 92-day scenario — why wrapper dominates

### Benchmark

Public Belgian corporate 3-month deposit benchmark used in the current snapshot:

- rate: 1.65% p.a.
- principal: EUR 2,000,000
- horizon: 92 days
- simple gross return: ~EUR 8,318
- simple post-25%-CIT return: ~EUR 6,239

This remains an imperfect benchmark because a EUR 2m corporate treasury customer may negotiate a different bank rate.

### Spiko EU T-Bills

At 2.13% p.a. indicative yield:

- gross 92-day return: ~EUR 10,740
- gross uplift vs 1.65% deposit: ~EUR 2,422

If the current working TOB hypothesis of a EUR 4,000 redemption tax applies, that one transaction cost exceeds the entire gross yield advantage.

Illustrative bridge, assuming TOB is deductible before 25% CIT:

```text
Fund gross return                     ~10,740
Less redemption TOB                    -4,000
Taxable residual                        6,740
Less 25% CIT                           -1,685
Indicative after-tax cash return        5,055

Deposit after-tax return               ~6,239
Difference                             ~-1,184
```

This is a scenario, not a certified tax calculation.

### Spiko Smart Cash

At 2.57% p.a. indicative yield:

- gross 92-day return: ~EUR 12,951
- gross uplift vs deposit: ~EUR 4,633

With the same illustrative EUR 4,000 redemption-tax assumption:

```text
Fund gross return                     ~12,951
Less redemption TOB                    -4,000
Taxable residual                        8,951
Less 25% CIT                           -2,238
Indicative after-tax cash return        6,713

Deposit after-tax return               ~6,239
Difference                                +474
```

Again, this is not filing-grade. It demonstrates that even a 92 bp headline yield advantage can almost disappear over three months because of legal-wrapper tax friction.

### Amundi DLT

Using a ~2.27–2.35% annualised public performance range, the gross 92-day return on EUR 2m would be roughly EUR 11.4k–11.8k under a simple annualised calculation.

If Belgian redemption TOB were also capped at EUR 4,000 because the relevant DLT share is an accumulating/capitalisation SICAV share, much of its gross advantage over the deposit would similarly disappear.

**Therefore the DLT technology itself does not solve Belgian tax friction.**

Exact TOB treatment for `LU3182424617` remains `NEEDS_REVIEW`.

---

## 5. Break-even logic Ophir should implement

For an instrument with a one-time exit tax/cost `C`, deposit annual rate `r_d`, fund annual net-of-product-fee yield `r_f`, corporate tax rate `t`, and principal `P`, a simplified break-even horizon can be approximated by solving:

```text
(P × (r_f - r_d) × days / 365 - C) × (1 - t) >= 0
```

If `C` is deductible symmetrically, corporate tax cancels from the break-even condition:

```text
days >= C × 365 / (P × (r_f - r_d))
```

Illustrative Spiko EU T-Bills vs 1.65% deposit:

- P = EUR 2m
- spread = 0.48% = 0.0048
- C = EUR 4,000

```text
break-even days ≈ 4,000 × 365 / (2,000,000 × 0.0048)
                ≈ 152 days
```

So under those assumptions the fund only begins to overcome the one-time EUR 4k exit drag after roughly **five months**, before considering TACT, operational costs or negotiated bank rates.

Illustrative Smart Cash vs 1.65% deposit:

- spread = 0.92% = 0.0092

```text
break-even days ≈ 4,000 × 365 / (2,000,000 × 0.0092)
                ≈ 79 days
```

This explains why Smart Cash can barely beat the deposit at 92 days under the current simplified assumptions.

### Product requirement

Ophir should calculate this dynamically for every company/instrument:

> “At your bank quote, amount and current fund yield, this instrument's estimated tax/cost break-even holding period is 152 days.”

That is more useful than displaying APY.

---

## 6. Tokenized vs traditional access — critical experiment

Fidelity and abrdn via Archax are strategically valuable research candidates because the platform advertises traditional and tokenized forms of the same/related institutional liquidity products.

For each, Ophir should compare:

```text
same underlying fund/share exposure
traditional custody/dealing path
vs
DLT/tokenized representation/path
```

Measure:

- yield difference;
- product fee difference;
- transaction fee difference;
- Belgian TOB difference, if any;
- TACT/account structure;
- subscription cut-off;
- redemption cut-off;
- settlement time;
- weekend access;
- stablecoin settlement;
- collateral/composability;
- accounting evidence;
- API automation.

If tax and yield are identical, any measured advantage is genuine **operational alpha from tokenization**, not financial-product alpha.

---

## 7. Search target: Belgian-optimal wrapper

The next candidate search should explicitly target:

1. EUR-denominated short-term MMF/cash fund;
2. EU/EEA regulated and accessible to Belgian corporates;
3. contractual/FCP or another wrapper with demonstrably low Belgian transaction-tax drag;
4. daily/T+0 or T+1 liquidity;
5. low fees;
6. public/current yield data;
7. API or embedded distribution access;
8. tokenized/DLT access preferred but not mandatory;
9. stablecoin settlement a bonus;
10. custody/account structure that does not introduce disproportionate Belgian TACT drag.

A traditional fund that wins this optimization is a valid Ophir recommendation candidate. Ophir is rail-neutral.

---

## 8. New Ophir ranking model

Do not rank by yield.

Rank by a transparent multi-dimensional outcome:

```text
Expected gross return
- product fees
- subscription costs/tax
- redemption costs/tax
- attributable account taxes
- on/off-ramp costs
- expected corporate tax
- quantified administration cost
= Expected after-tax cash outcome
```

Then display separately:

- liquidity score/facts;
- credit/duration/counterparty risk;
- operational settlement speed;
- API/automation quality;
- accounting complexity;
- tax confidence/validation level.

Do not silently collapse risk into return without an explicit model approved for that use.

---

## 9. Current conclusion

No researched tokenized candidate is yet proven to beat the Belgian bank benchmark on a fully validated after-tax basis for EUR 2m over 92 days.

That is not a failure of the thesis. It reveals the real product:

> **Ophir is a jurisdiction-aware treasury optimizer that finds when a financial instrument is actually worth using after tax, legal wrapper, liquidity and administrative friction.**

The system should be capable of concluding “keep the cash at the bank” when that is the best answer.

The highest-value research now is not another blockchain integration. It is finding and validating the wrappers/instruments where Belgian tax economics and modern digital rails align.
