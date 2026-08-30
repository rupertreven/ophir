# Ophir Product Thesis v2

> **Date:** 2026-08-30 17:15 CEST  
> **Status:** Canonical strategic synthesis after Research Phase 1  
> **Supersedes as product framing:** tokenized-cash-first framing in early founder/business-plan drafts. Those documents remain historical inputs until updated.

## 1. One sentence

> **Ophir is the intelligence layer that tells a company the highest-value legal use of its next euro of capital.**

## 2. What changed during Research Phase 1

Ophir began with a tokenized-treasury hypothesis: connect Belgian corporate bank/accounting data to stablecoins, tokenized money-market funds and later tokenized bonds while hiding wallets/chains from the customer.

Research did not invalidate tokenized finance, but it changed its position in the product.

Key findings:

1. Tokenized MMFs do not inherently create yield alpha; the underlying instrument creates the return.
2. Belgian tax/legal wrapper effects can dominate modest headline-yield differences over short horizons.
3. Daily liquidity is valuable, but a few dozen basis points on €0.5m–€2m often creates only modest annual customer value.
4. Tokenization can create operational advantages — settlement, programmability, collateral mobility, machine access — but those benefits must be measured rather than assumed.
5. Much larger corporate treasury value pools exist in debt/cash overlap, receivables/working capital, supplier-payment economics and FX/netting.
6. The same bank/ERP/entity/rules architecture can analyze all of these opportunities.

Therefore:

> **Tokenized finance becomes an instrument/rail inside Ophir, not Ophir's reason for existing.**

## 3. Core problem

Corporate capital is fragmented across:

- bank accounts;
- legal entities;
- debt facilities;
- receivables;
- payables;
- supplier terms;
- currencies;
- guarantees/collateral;
- financial instruments;
- tax/accounting rules;
- treasury policies;
- ERP/project systems.

Finance teams often optimize each domain separately.

The economically correct question is cross-domain:

> **Given the company's actual liquidity requirements, legal entities, obligations, debt cost, supplier opportunities, receivables, currencies, tax/accounting treatment and risk policy, what is the best use of marginal capital now?**

## 4. The marginal-euro optimizer

Ophir should construct a transparent opportunity curve for corporate cash.

Illustrative ordering:

```text
Use of marginal €1                         Economic value
Supplier early-payment discount            12–20%+ implied annual return
Avoid overdraft                            5–7%
Repay revolver                             4–5%
Finance/accelerate receivable              context dependent
FX/netting opportunity                     measurable bp saving
Maintain required liquidity                mandatory constraint
Term deposit                               ~market cash rate
Daily MMF/FCP                              ~market cash rate, liquid
Idle current account                       low return
```

The order changes continuously and must be company-specific.

Ophir does not silently reduce risk/liquidity/legal constraints to one opaque score. It shows economics and constraints separately.

## 5. Primary opportunity engines

### A. Debt + idle cash

Detect simultaneous low-yield cash and higher-cost short-term debt.

Example screening economics:

```text
€3m actionable overlap
Debt cost: 4.0%
Cash yield: 0.3%
Gross spread: 3.7%
Annual opportunity: €111k
```

For multi-entity groups, apparent consolidated overlap is not automatically actionable. Entity, covenant, corporate-law, tax and transfer-pricing constraints must be applied first.

**Status:** `PRIORITY CANDIDATE`.

### B. Receivables / DSO / financing

Connect project/AR lifecycle to marginal funding cost.

At €100m revenue:

```text
10 avoidable DSO days = €2.74m working capital
At 5% marginal funding cost ≈ €137k/year
```

Ophir should distinguish operational delay, contractual delay, dispute, retention and financeable approved receivables.

**Status:** `PRIORITY CANDIDATE`.

### C. Dynamic discounting / supply-chain finance

Treat optional supplier early-payment discounts as a use of corporate capital.

A 1% discount for payment 30 days early implies roughly a 12% simple annualized return on the accelerated cash; 2% can imply ~25%.

Ophir compares the discount with debt repayment, liquidity requirements and financial investments.

**Status:** `PRIORITY CANDIDATE` where supplier spend/adoption is material.

### D. FX exposure + netting

Aggregate AP/AR/cash/forwards across entities and measure actual provider spread.

```text
€25m annual FX flow × 40 bp avoidable cost = €100k/year
€100m × 10 bp = €100k/year
```

Natural netting can reduce external conversion volume before pricing optimization.

**Status:** `PRIORITY` for FX-heavy companies; secondary for domestic-EUR companies.

## 6. Secondary / supporting modules

### Guarantees & collateral

Potential construction-native wedge: connect contractual/project milestones to guarantee reductions/releases, facility capacity and collateral opportunity cost.

**Status:** secondary / validate with real guarantee portfolios.

### Cash yield / deposits / MMFs / tokenized instruments

Still useful as a destination for genuinely deployable cash, but not sufficient as the core product thesis.

Ophir compares like-for-like liquidity and after-tax economics.

**Status:** secondary module / instrument layer.

### Treasury operations & compliance

Automation of reconciliation, tax/accounting evidence, policy checks, intercompany administration and audit support may create meaningful productivity value.

Its larger strategic role is horizontal: make every optimization administratively usable and create switching cost/moat.

**Status:** core platform capability; secondary standalone wedge.

## 7. Product architecture

```text
BANKS / ERP / AP / AR / PROJECTS / DEBT / FX / DOCUMENTS
                         │
                         ▼
              NORMALIZED CAPITAL GRAPH
                         │
             ┌───────────┼────────────┐
             ▼           ▼            ▼
        Forecast      Rules       Opportunity
        & liquidity   engine      engines
             │           │            │
             └───────────┼────────────┘
                         ▼
               MARGINAL € OPTIMIZER
                         │
                         ▼
                CFO DECISION VIEW
                         │
       ┌─────────────────┴─────────────────┐
       ▼                                   ▼
Instructions / evidence             Provider deep link
       │                                   │
       └──────── COMPANY EXECUTES ─────────┘
                         │
                         ▼
               OPHIR OBSERVES RESULT
                         │
                         ▼
          RECONCILIATION + ACCOUNTING/TAX
                         │
                         ▼
                REALIZED VALUE LEDGER
```

## 8. Hard execution boundary

The product invariant is:

> **Ophir observes, calculates, compares, explains, prepares and documents. The authorized company user decides. The bank or regulated provider executes.**

Ophir v1:

- does not hold customer money;
- does not custody keys/assets;
- does not autonomously trade/invest;
- does not become discretionary treasury manager;
- does not become a single point of failure for critical payments.

A provider may eventually support a scheduled instruction authorized in advance by the company. Once the provider accepts that binding instruction, Ophir must not be required for execution to occur.

## 9. Legal / tax / accounting gate

Every opportunity passes through:

1. ownership — whose asset/obligation is it?
2. permitted use — can it legally be moved, invested, netted, pledged or accelerated?
3. regulatory perimeter — what may Ophir do?
4. tax — Belgian consequences;
5. accounting — Belgian GAAP/IFRS consequences;
6. operational safety — liquidity, settlement, cutoffs, fallback;
7. economics — only then show realizable Net Treasury Benefit.

Research is not a production rule. Validation statuses remain explicit.

## 10. Role of tokenization

Tokenization is treated as a capability dimension:

```text
Instrument / rail
├── economics
├── liquidity
├── risk
├── tax
├── accounting
├── settlement
├── programmability
├── API access
└── collateral utility
```

Tokenized deposits, MMFs, bonds, receivables or collateral should win only when their total outcome is superior.

The user should not need to understand chains/wallets unless legally/operationally necessary.

## 11. Realized Value Ledger

Ophir's commercial proof should be measurable:

```text
Opportunity identified
Expected annual value
Constraints checked
Company decision
External execution observed
Actual balance/flow change
Tax/fees
Realized value
Accounting/evidence complete
```

Dashboard concept:

```text
Ophir cost YTD                 €18,000
Verified value created YTD    €247,000
ROI                             13.7×
```

This can support value-based pricing and customer retention.

## 12. Initial customer hypothesis v2

The original €5m–€100m revenue SME hypothesis may be too small for the strongest modules.

Research Phase 1 suggests prioritizing companies with **treasury complexity and capital scale**, not revenue alone.

Potential qualification signals:

- multiple legal entities;
- multiple banks/accounts;
- simultaneous cash and short-term debt;
- €50m+ supplier spend;
- €100m+ revenue with meaningful receivables;
- material non-EUR flows;
- significant guarantees/collateral;
- no fully optimized enterprise TMS/treasury function.

Likely beachhead: Belgian lower-mid-market to mid-market groups, with construction/project businesses as a useful design vertical but not necessarily the only market.

## 13. Moat v2

The moat is not blockchain access.

Candidate moat:

- normalized multi-entity capital graph;
- integrations;
- company-specific liquidity/treasury context;
- effective-dated Belgian tax/accounting/legal rules;
- opportunity history;
- realized-value dataset;
- provider pricing/outcome data;
- explainable decision engine;
- audit/evidence graph;
- trust.

AI is leverage over this graph, not the authoritative financial rule engine.

## 14. MVP direction

Do not build the full operating system first.

Candidate MVP:

1. connect bank/accounting data;
2. legal-entity model;
3. cash/forecast view;
4. debt/facility register;
5. detect same-entity debt/cash overlap;
6. calculate explainable opportunity;
7. optionally ingest AP/AR to add supplier/receivable opportunities;
8. prepare action package;
9. observe execution afterward;
10. realized-value ledger.

This should be validated with real company data before expanding instrument/tokenization breadth.

## 15. Research Phase 2

1. 10–20 CFO/treasurer interviews focused on measurable € leakage.
2. Obtain anonymized bank/accounting/debt/AP/AR samples from design partners.
3. Measure actual cash/debt overlap.
4. Measure actionable DSO delay.
5. Measure supplier-discount availability.
6. Measure actual FX spreads/netting potential.
7. Benchmark existing TMS/ERP/working-capital tools against the cross-domain optimizer thesis.
8. Rebuild ICP/pricing from observed customer value.
9. Update technical/domain model for capital/opportunity engines.
10. Specialist Belgian legal/tax/accounting validation for the first selected MVP opportunity.

## 16. Kill criteria

Reconsider/pivot if:

- well-run target companies already capture nearly all measurable opportunities;
- required data cannot be obtained reliably;
- entity/legal/tax constraints make most apparent value non-actionable;
- incumbents solve the cross-domain problem at acceptable cost for the target segment;
- implementation/integration cost destroys one-founder economics;
- verified customer value is consistently below a viable SaaS ACV multiple.

## 17. Long-term vision

The old vision of a financial control plane remains directionally valid, but autonomy is not the near-term thesis.

The long-term system understands every economically relevant corporate capital claim and obligation and continuously surfaces the highest-value permitted decisions.

Execution can remain with regulated financial infrastructure.

> **Ophir makes corporate capital legible, comparable and economically actionable.**
