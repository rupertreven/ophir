# Belgian-Optimal Regulated Cash Instruments v1

> Status: public-source discovery research, 28 Aug 2026. Tax treatment is not professionally validated.

## Research question

Do regulated, tokenised/API-accessible EUR cash instruments exist today that could be economically superior for a Belgian company once yield, tax wrapper, liquidity and operational access are considered?

## Executive finding

Yes, the market is now materially broader than Spiko. However, the first search does **not** reveal an obvious public, plug-and-play `FCP + EUR + tokenised + Belgian corporate + embedded API` product.

The most important new candidates are:

1. **Amundi Funds Cash EUR — J28 EUR DLT (C)** — Luxembourg SICAV tokenised share on Ethereum, ISIN `LU3182424617`.
2. **Fidelity ILF — The Euro Fund via Archax** — Irish EUR institutional liquidity fund, ISIN `IE0003323494`, offered in tokenised or traditional form, fiat or stablecoin access.
3. **abrdn Liquidity Fund (Lux) — Euro Fund via Archax** — Luxembourg EUR liquidity fund, ISIN `LU0966092131`, tokenised/traditional access, fiat or stablecoin access.
4. **Amundi Money Market Fund — Short Term EUR tokenised solution** — already deployed for Ant International corporate treasury; public productisation/API access for Belgian SMEs remains unclear.

The market evidence strongly supports Ophir's thesis that regulated tokenised treasury rails are becoming real, but **tax wrapper and distribution access remain first-class selection variables**.

---

## 1. Amundi Funds Cash EUR — J28 EUR DLT (C)

### Identified facts

- tokenised share class of Amundi Funds Cash EUR;
- ISIN: `LU3182424617`;
- Luxembourg-domiciled Amundi Funds is an open-ended SICAV/UCITS;
- public Ethereum is used for tokenised record-keeping;
- CACEIS provides tokenisation infrastructure, digital investor wallets and a digital order platform for subscriptions/redemptions;
- Amundi/CACEIS describe instant order execution and 24/7 operability as benefits of the DLT model;
- current Amundi fund data on 14 Aug 2026 showed approximately 2.3459% annualised one-month performance and 2.2694% annualised three-month performance for J28 EUR DLT (C);
- financial statements list management fee around 0.03% and maximum management fee around 0.07% for the class.

### Strategic importance

This is a **large incumbent asset manager + large bank/transfer agent + real tokenised EUR MMF share class**, not a crypto-native experiment.

It also proves that tokenisation can be layered onto a mainstream institutional cash fund while the same fund remains available through traditional channels.

### Belgian issue

It is still a **Luxembourg SICAV capitalisation share class**. Therefore the same Belgian TOB concern identified for Spiko cannot be assumed away. Exact Belgian subscription/redemption treatment must be validated for this ISIN.

### Access issue

The public material confirms CACEIS digital order infrastructure but does not establish a public embedded API comparable to Spiko's developer/distributor API for a small independent Belgian SaaS company.

**Ophir status:** strong benchmark/candidate; integration feasibility `NEEDS_PROVIDER_DISCUSSION`.

---

## 2. Fidelity ILF — The Euro Fund via Archax

### Identified facts

- ISIN `IE0003323494`;
- institutional/professional investor product;
- tokenised **or traditional** form through Archax;
- invest using fiat or stablecoins;
- T+0 availability subject to payment rails;
- minimum investment EUR 50,000;
- Fidelity management fee shown as 0.15%;
- Archax access fee shown as 0.20%;
- published dealing cut-off 11:00 UK time on business days.

### Strategic importance

This is especially valuable for Ophir research because the **same underlying fund can be accessed in tokenised or traditional form**. It is therefore a potential clean experiment for isolating the value of tokenisation from the value of the investment strategy itself.

### Belgian issue

The legal wrapper/share-class and exact Belgian TOB/TACT/corporate-tax treatment must be determined from the prospectus and Belgian rules. Irish domicile alone does not prove favourable Belgian treatment.

### Integration issue

Archax publicly offers the investment access layer, but an Ophir-grade embedded/API distribution model must be confirmed commercially and technically.

**Ophir status:** high-priority candidate for provider outreach and Belgian tax classification.

---

## 3. abrdn Liquidity Fund (Lux) — Euro Fund via Archax

### Identified facts

- ISIN `LU0966092131`;
- professional/institutional investor product;
- tokenised or traditional access;
- fiat or stablecoin investment rails;
- T+0 availability subject to payment rails;
- EUR 50,000 minimum;
- abrdn management fee shown as 0.10%;
- Archax access fee shown as 0.20%;
- objective is capital preservation/liquidity with return in line with short-term money-market rates, using €STR as comparator.

### Strategic importance

Again provides a potentially useful traditional-vs-tokenised comparison through one access platform.

### Belgian issue

Luxembourg domicile and the displayed `L-1 Income EUR` share class require exact legal-form and Belgian-tax analysis. A distributing/income share class may have materially different Belgian cash-tax mechanics from an accumulating SICAV share, but this cannot be inferred without professional review.

**Ophir status:** high-priority tax-wrapper comparison.

---

## 4. Amundi Money Market Fund — Short Term EUR / Ant International

Amundi and CACEIS publicly confirmed in June 2026 that tokenised EUR and USD shares of Amundi Money Market Fund — Short Term were launched for Ant International for real-time intra-group liquidity management.

This is direct evidence that **corporate treasury using tokenised MMFs is already in production** at a sophisticated corporate client.

Public Amundi data for traditional EUR share classes around Aug 2026 showed annualised one-month performance around 2.18%–2.32% depending on class, and roughly 2.09%–2.24% over three months.

The open question is not product existence but **distribution/accessibility**: the Ant implementation is bespoke and public sources do not establish that a Belgian SME or Ophir can access the tokenised corporate flow through a public API today.

---

## 5. What the ECB says the market looks like

ECB research published in April 2026 confirms:

- EU/global TMMFs are growing rapidly but remain small relative to traditional MMFs;
- tokenisation can provide faster settlement, near-24/7 availability and programmability;
- TMMF tokens can enable collateral use cases;
- the economic return remains broadly comparable to traditional MMFs because the underlying assets are similar;
- adoption has so far been concentrated substantially in the digital-asset ecosystem;
- only a minority of structures provide deeply on-chain end-to-end operation; many still rely on transfer agents and traditional underlying assets.

This supports Ophir's neutral thesis:

> **Tokenisation is primarily an operational/settlement innovation; it is not inherently a yield premium.**

---

## 6. FCP hypothesis — current result

The research hypothesis was that a contractual/FCP wrapper could potentially avoid the Belgian redemption TOB drag associated with accumulating SICAV shares while Ophir automates the more complex transparent tax reporting.

### Current search result

No obvious public product was found that simultaneously satisfies all of:

```text
EUR money-market exposure
+ regulated EU fund
+ contractual/FCP wrapper
+ tokenised share/official DLT representation
+ Belgian corporate distribution
+ practical SME minimum
+ public/embedded API
+ high liquidity
```

This does **not** prove none exists. It means the public market is not yet commoditised enough to discover one easily.

### Implication

Do not make `FCP` a product requirement. Make **Belgian after-tax outcome** the requirement. Other legal structures/share classes may also be optimal.

---

## 7. Candidate ranking for next diligence

### Tier 1 — immediate

**Fidelity ILF Euro via Archax**
- reason: tokenised/traditional dual access; Irish structure; fiat/stablecoin; T+0; clean tokenisation comparison.

**abrdn Liquidity Fund Lux Euro via Archax**
- reason: same platform, different domicile/share-class structure; useful tax comparison.

**Amundi J28 EUR DLT**
- reason: major incumbent, real Ethereum share class, very low fund fee, strong current performance, institutional credibility.

### Tier 2

**Amundi Short Term EUR tokenised corporate solution**
- reason: strongest proof that the corporate-treasury use case is real; access may be bespoke.

**BlackRock tokenised European cash products**
- reason: major institutional platform; determine exact EUR share classes, legal wrappers, Belgian availability and integration path.

### Existing benchmark

**Spiko EU T-Bills / Smart Cash**
- reason: best public developer/embedded infrastructure discovered so far, but Belgian short-horizon tax drag may be material.

---

## 8. Ophir instrument-selection model should now include

```text
headline_yield
net_fund_fee
wrapper_type
legal_form
fund_domicile
accumulating_or_distributing
Belgian_TOB_subscription
Belgian_TOB_redemption
Belgian_TACT
withholding_tax
corporate_income_tax
accounting_complexity
minimum_ticket
settlement_time
redemption_time
weekend_liquidity
fiat_rails
stablecoin_rails
tokenised_or_traditional
API_access
embedded_distribution
regulated_provider
custody_model
collateral_utility
professional_validation_status
```

The optimizer must never select by yield alone.

---

## 9. Important commercial insight

The strongest product may **not** be a marketplace of only tokenised products.

Archax itself demonstrates why: the same institutional funds can be offered in traditional or tokenised form. Ophir can therefore become the decision layer that says:

> For this Belgian company, amount and holding horizon, use the traditional rail.

or

> For this case, the tokenised rail has enough settlement/liquidity/programming value to justify it.

That neutrality increases trust and protects Ophir from becoming obsolete if tokenisation itself becomes commodity infrastructure.

---

## 10. Immediate next diligence

For each Tier-1 candidate obtain/validate:

1. prospectus and KID;
2. exact legal form and share-class type;
3. Belgian corporate investor eligibility;
4. Belgian TOB on buy/redeem;
5. TACT treatment/custody structure;
6. withholding and corporate-income-tax treatment;
7. current net yield/performance;
8. minimum investment;
9. exact settlement/redemption mechanics;
10. API/embedded/distributor capability;
11. fees charged by access platform;
12. whether traditional and tokenised rails have identical economic rights;
13. whether stablecoin settlement is live or merely planned;
14. provider willingness to onboard a Belgian treasury SaaS/distribution partner.

Then rerun the EUR 2m / 92-day Ophir model across all candidates.

---

## Public sources used in discovery

- ECB, *Tokenised money market funds: new technology, familiar risks?*, Apr 2026.
- Amundi/CACEIS official tokenisation announcements and fund data.
- Amundi Funds financial statements / share-class data.
- Archax product pages for Fidelity ILF Euro and abrdn Liquidity Fund Lux Euro.
- Franklin Templeton official tokenisation materials as broader market evidence.

Exact source URLs/retrieval dates should be stored in production instrument dossiers rather than relying on this narrative research note.
