# Use Case — FX Exposure, Netting & Execution Intelligence v1

> **Date:** 2026-08-29 08:22 CEST  
> **Status:** Initial deep dive / `PUBLIC_SOURCE_RESEARCH` + economic model  
> **Target:** Belgian mid-market and large companies with recurring non-EUR flows

## Executive conclusion

FX can clearly be a €100K treasury problem, but only for companies with sufficient foreign-currency flow or poor pricing/processes. The strongest Ophir wedge is not speculative FX timing. It is:

> **aggregate exposures across entities, net natural offsets, quantify actual bank spread/fees, compare hedging/payment alternatives, and prepare a policy-compliant action for the treasury team.**

At €25m annual FX flow, 40 bp of avoidable all-in spread equals €100k/year. At €100m flow, only 10 bp is required to create €100k of value.

Ophir should never promise market-direction alpha. The value is structural cost reduction, exposure reduction and control.

Tokenized deposits/stablecoins may eventually reduce cross-border settlement/prefunding friction, but only where regulated provider rails, legal ownership, accounting and tax treatment make them superior to conventional bank FX/payment rails.

---

## 1. Problem classes

### A. Fragmented FX execution

Different entities independently buy/sell currencies without group visibility.

Example:

```text
Entity A needs USD 4m
Entity B receives USD 2.5m
Entity C receives USD 1m

Gross external FX without netting:  USD 7.5m equivalent flow
Net group USD need:                 USD 0.5m
```

Subject to legal/entity/cash-pooling constraints, natural netting can drastically reduce external FX volume.

### B. Opaque bank spreads

Corporate FX cost can include:

- spread versus reference/interbank rate;
- explicit transaction fee;
- payment/correspondent fee;
- forward points;
- credit charge/margin;
- settlement/prefunding cost;
- operational cost.

Bank statements often make the true basis-point cost difficult to see.

### C. Unhedged forecast exposures

Treasury may hedge too late, too much, too little or inconsistently across entities.

Ophir can quantify exposure and policy compliance but should not become a discretionary trading system.

### D. Excess gross cross-border payments

Intercompany flows can create unnecessary two-way currency transfers and bank charges when legally permissible netting/central settlement could reduce volume.

---

## 2. €100K mathematics

### Spread optimization

```text
Annual FX flow     Avoidable cost       Annual value
€10m               40 bp                €40k
€25m               40 bp                €100k
€50m               25 bp                €125k
€100m              10 bp                €100k
€250m              10 bp                €250k
```

Thus this becomes highly relevant for internationally active mid-market/large corporates.

### Natural netting example

Suppose group entities generate annual gross USD buy/sell requirements of €80m equivalent but €30m can be naturally offset/legally netted before external execution.

If external all-in FX/payment cost averages 25 bp:

```text
€30m avoided external conversion × 0.25% = €75k/year
```

Add better pricing on the remaining €50m by 10 bp:

```text
€50m × 0.10% = €50k/year
```

Combined structural opportunity: **€125k/year**.

---

## 3. Ophir product

### Data

```text
Bank accounts
ERP / AP / AR
Purchase orders
Sales invoices
Intercompany balances
Debt facilities
FX contracts/forwards
Treasury policy
```

### Exposure engine

By currency, entity and date bucket:

```text
EUR functional entity
USD receivables
USD payables
USD bank cash
USD debt
committed orders
high-confidence forecast flows
existing forwards
= net USD exposure
```

Confidence must be explicit. A signed supplier invoice is not equivalent to a probabilistic sales forecast.

### Actual-cost engine

For completed FX transactions Ophir can reconstruct:

```text
reference market rate at execution
actual customer rate
explicit fees
payment fees
all-in basis-point cost
provider/bank
entity
currency pair
volume
```

This creates a negotiating dataset:

> “Bank A charged median 31 bp on EUR/USD over €12.4m; Bank B charged 18 bp on comparable tickets.”

### Netting engine

Identify offsetting exposures before external FX, subject to:

- legal entity;
- currency;
- value date;
- intercompany rules;
- tax/transfer-pricing;
- cash ownership;
- contractual restrictions.

### Decision output

```text
FX OPPORTUNITY — USD

Next 30 days
USD payables                              $8.2m
USD receivables                           $5.6m
Existing USD cash                         $0.9m
Existing forwards                         $0.5m
Net uncovered requirement                 $1.2m

Without group netting external FX need    $6.7m
After eligible netting                    $1.2m
Avoided external conversion               $5.5m
Historical all-in FX cost                  24 bp
Indicative avoided cost                  ~€13k

Policy hedge requirement                   80%
Remaining hedge gap                       $0.46m

[View exposure]
[Compare provider quotes]
[Prepare action]
```

Ophir does not execute the FX trade.

---

## 4. Belgian legal / tax / accounting gate

### Intercompany netting

Do not assume offsetting economic exposures can simply be settled centrally. Review:

- legal ownership of receivables/payables;
- intercompany agreements;
- transfer pricing;
- treasury/cash-pool structure;
- lender/security restrictions;
- sanctions/AML/payment restrictions where cross-border;
- local-country rules for foreign subsidiaries.

For a Belgian-only group with foreign currencies the legal analysis can be simpler than multinational cash concentration, but entity separateness remains real.

### Derivatives/hedging

Forward contracts and other derivatives introduce:

- accounting classification;
- fair-value treatment;
- possible hedge-accounting requirements;
- counterparty/credit documentation;
- MiFID/provider appropriateness obligations;
- treasury-policy controls.

Ophir should model and explain provider offers but not provide unlicensed personalized investment advice or execute derivatives.

### Tax

FX gains/losses and hedging costs affect taxable profit/accounting. Intercompany FX arrangements can create transfer-pricing consequences. Exact treatment must be validated by structure.

---

## 5. Tokenized rails

### Potential value

Regulated tokenized bank deposits and compliant stablecoin rails may improve:

- 24/7 settlement;
- atomic FX/payment settlement;
- reduction in correspondent chains;
- reduced prefunding;
- faster cross-border movement;
- programmable settlement.

Institutional bank initiatives in 2026 increasingly target these functions.

### Ophir test

For every rail compare:

```text
conventional bank FX + payment
vs
regulated tokenized deposit rail
vs
regulated stablecoin/payment provider
```

Measure:

- all-in FX spread;
- explicit fee;
- settlement time;
- prefunding requirement;
- weekend availability;
- counterparty/custody risk;
- accounting burden;
- tax treatment;
- legal eligibility;
- API quality.

Tokenized rail wins only if total economics/control are superior.

---

## 6. Construction relevance

Belgian construction groups may have meaningful FX where they:

- procure steel/equipment internationally;
- buy USD/CNY/GBP-denominated materials;
- execute projects outside the eurozone;
- own foreign subsidiaries;
- finance equipment internationally.

Domestic Belgian contractors with overwhelmingly EUR flows are not the ICP for this module.

Industrials, import/export, logistics and multinational service groups may be stronger FX targets.

---

## 7. Competitive risk

Banks, TMS platforms and specialist FX providers already provide exposure/hedging tools.

Ophir's possible differentiation:

> **bank-agnostic actual-cost intelligence + entity-aware netting + Belgian tax/accounting context + marginal-capital integration.**

The product should connect FX decisions to cash/debt/receivables rather than operate as an isolated FX dashboard.

---

## 8. €100K verdict

`PRIORITY FOR FX-HEAVY COMPANIES`, `SECONDARY FOR DOMESTIC-EUR COMPANIES`.

The €100K threshold is straightforward:

- €25m flow × 40 bp;
- €50m × 20 bp;
- €100m × 10 bp.

The value is particularly credible when combining natural netting with measurable provider spread differences.

Main risk: sophisticated treasury teams already negotiate institutional spreads and net exposures efficiently.

---

## 9. Market validation

For target companies collect:

- annual FX volume by pair;
- number of executing banks/providers;
- actual customer rates and timestamps;
- explicit fees;
- gross buy/sell flows by entity;
- natural offsets currently netted/not netted;
- hedging policy;
- forward volume;
- current TMS;
- treasury FTE effort;
- cross-border payment fees;
- prefunding requirements;
- settlement delays.

### Promote criterion

Promote as core module where a company has >€25m annual FX flow and measured avoidable all-in cost/netting opportunity >€100k/year.

### Kill/downgrade criterion

Downgrade for companies with predominantly EUR flows or already highly optimized institutional execution.
