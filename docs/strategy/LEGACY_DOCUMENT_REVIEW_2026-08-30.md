# Legacy Document Review — 2026-08-30

> **Date:** 2026-08-30 17:15 CEST  
> **Purpose:** Double-check early Ophir documents against Product Thesis v2 before restructuring/updating them.  
> **Rule:** Preserve useful research/history; do not silently rewrite historical assumptions into facts.

## Executive finding

The early documents contain a strong architectural foundation, but the **strategic center of gravity has changed**.

Early framing:

> Treasury Operating System for the Tokenized Economy → Observe → Understand → Orchestrate → Autonomous Treasury.

Current framing:

> Corporate Treasury Intelligence → identify the highest-value legal use of marginal corporate capital → company decides → regulated/existing provider executes → Ophir observes and measures realized value.

The old documents are therefore not wrong wholesale. They are **partially superseded**.

---

## 1. `founder-memo.md`

### Keep

Strong and still relevant:

- corporate treasury is fragmented;
- digital/API-native finance trend;
- traditional and tokenized rails should coexist;
- compliance-first architecture;
- no initial bank/custodian/exchange role;
- AI-native lean company model;
- auditability/security/simplicity;
- integration graph as strategic asset.

### Change

Sections requiring material revision:

#### Opening thesis

Current memo overweights:

- tokenization;
- programmable money;
- autonomous economic action.

New opening should lead with **capital inefficiency** and measurable corporate value.

#### Product Vision Phase III/IV

`Orchestrate` and especially `Autonomous Treasury` conflict with the clarified near-term execution boundary.

Long-term provider-authorized automation can remain a possibility, but should not be presented as the inevitable product destination.

#### Mission

`Build the operating system for digital capital` is broad and technology-centered.

Candidate v2 mission language:

> **Make every corporate euro economically legible.**

or

> **Help companies put every euro to its highest-value permitted use.**

Do not finalize slogan before GTM/customer validation.

### Status

`NEEDS_V2_UPDATE`.

---

## 2. `business-plan.md`

### Keep

- evidence-driven/falsifiable approach;
- founder-led Belgian validation;
- recurring SaaS model;
- regulatory Green/Amber/Red methodology;
- multi-tenant secure architecture;
- AI operating leverage;
- conservative financial modeling;
- explicit risks/kill criteria.

### Change

#### Executive summary

`Treasury Operating System for the Tokenized Economy` is now superseded as the primary proposition.

#### Customer problem

Current list is mostly workflow pain:

- fragmented visibility;
- spreadsheets;
- reconciliation;
- forecasting.

These are real but insufficient. Add measurable economic leakage:

- simultaneous idle cash + expensive debt;
- avoidable working-capital delay;
- missed supplier discounts;
- avoidable FX gross flow/spread;
- stale guarantees/collateral;
- suboptimal liquid cash.

#### MVP

Read-only dashboard + wallet visibility is too generic and unlikely to prove strong willingness-to-pay.

MVP should center on one measurable opportunity engine, likely debt/cash overlap, with realized-value tracking.

#### Customer segment

`€5m–€100m revenue SMEs` may be too small. Replace revenue-first segmentation with treasury-complexity/value signals.

#### Roadmap

`Regulated-partner orchestration` and `Governed agents` should be demoted from assumed stages to optional future capabilities.

#### Risks

Add:

- target companies may already optimize obvious capital inefficiencies;
- apparent consolidated value may be legally non-actionable;
- cross-domain data may be incomplete;
- existing TMS/ERP/working-capital tools may cover enough of the opportunity.

### Status

`NEEDS_V2_UPDATE`.

---

## 3. `TECHNICAL_PRODUCT_SPEC.md`

### Keep

The technical foundation is strong:

- modular monolith;
- normalized treasury ledger;
- source provenance;
- effective-dated deterministic rules;
- AI cannot authoritatively invent tax/accounting rules;
- legal-entity model;
- bank/accounting adapters;
- explainable forecasting;
- external execution boundary;
- audit/event log;
- human review.

These decisions survive the strategic pivot well.

### Change

#### Primary use case

Current primary use case is surplus cash → regulated cash-management instruments. Replace with **capital opportunity detection**.

#### Treasury engine

Expand from `DeployableCashCalculation` to:

- marginal cash value;
- debt facility economics;
- cash/debt overlap;
- AP early-payment opportunities;
- receivable lifecycle/funding cost;
- FX exposure/netting;
- opportunity confidence/actionability.

#### Domain model additions

Need first-class entities for:

- `DebtFacility`;
- `DebtBalance`;
- `Opportunity`;
- `OpportunityConstraint`;
- `OpportunityCalculation`;
- `RealizedValueEvent`;
- supplier payment terms/discount offers;
- richer receivable lifecycle;
- FX exposure/hedge where selected.

#### Instrument graph

Keep it, but make it one destination class inside the marginal-capital engine rather than the center of the MVP.

#### Execution boundary

Clarify further:

> Ophir can prepare instructions. For critical scheduled flows, any future binding scheduled instruction must be accepted/held by the regulated provider so Ophir is not a single point of failure at execution time.

### Status

`ARCHITECTURE_REUSABLE / NEEDS_V2_DOMAIN_UPDATE`.

---

## 4. `DOMAIN_MODEL_V1.md`

Likely reusable core:

- tenant;
- legal entity;
- user/roles;
- bank/accounting data;
- transaction intent/handoff/reconciliation;
- rule/evidence model.

Required extension mirrors technical spec:

- facilities/debt;
- opportunity graph;
- realized value;
- AP discount terms;
- receivable states;
- legal actionability constraints.

Status: `NEEDS_V2_EXTENSION`, not replacement.

---

## 5. `GOLDEN_PATH_SEQUENCE.md`

Current golden path is investment-centric:

> bank → cash forecast → instrument → tax → approval → provider → reconciliation.

Keep this as an **instrument-investment subflow**, but it should no longer be the product-wide golden path.

New canonical golden path should be:

```text
connect data
 -> normalize capital graph
 -> forecast/liquidity constraints
 -> detect opportunities
 -> apply legal/tax/accounting/policy gates
 -> rank permitted uses of marginal capital
 -> explain expected value
 -> prepare action package
 -> company executes externally
 -> observe/reconcile
 -> calculate realized value
```

Status: `DEMOTE_TO_INSTRUMENT_SUBFLOW`; create V2 product golden path later.

---

## 6. Regulatory documents

`regulatory.md` and `REGULATORY_BOUNDARY_V1.md` remain highly valuable.

The execution boundary became **more conservative**, not less.

Need to extend regulatory mapping to:

- debt repayment recommendations/preparation;
- supplier discount decision support;
- receivables financing comparison/referrals;
- FX/derivative comparison;
- intercompany funding/netting;
- guarantee/collateral recommendations.

Status: `KEEP + EXTEND`.

---

## 7. Tokenized-rail / instrument research

Keep all research. It is not obsolete.

Reclassify it as:

> **Instrument & Rail Research** supporting one branch of the capital-allocation engine.

Key retained insight:

> Tokenization is not automatically yield alpha. Instrument/wrapper selection can create tax/yield alpha; tokenization can create operational alpha; Ophir aims to create intelligence/compliance alpha.

Status: `KEEP / RECLASSIFY`.

---

## 8. Market / competition / GTM

These documents were written before the €100K problem sprint and should be reviewed next in detail.

Expected changes:

- ICP likely moves upward from small SME toward lower-mid/mid-market complexity;
- competitor set must include working-capital, AP discounting, AR/receivables, FX intelligence and capital allocation products, not only TMS/tokenized-finance vendors;
- pricing should be tested against verified realized value;
- design partners should supply anonymized real treasury data, not only interview opinions.

Status: `NEEDS_V2_RESEARCH_UPDATE`.

---

## 9. Documentation restructuring recommendation

Target logical structure:

```text
docs/
├── strategy/
│   ├── OPHIR_PRODUCT_THESIS_V2.md
│   ├── founder-memo.md
│   ├── business-plan.md
│   ├── market.md
│   ├── competition.md
│   └── go-to-market.md
│
├── product/
│   ├── TECHNICAL_PRODUCT_SPEC.md
│   ├── DOMAIN_MODEL_V1.md
│   ├── GOLDEN_PATH_SEQUENCE.md
│   └── product-validation-plan.md
│
├── regulatory/
│   ├── regulatory.md
│   └── REGULATORY_BOUNDARY_V1.md
│
├── research/
│   ├── instruments/
│   ├── tax/
│   ├── rails/
│   └── validation/
│
└── use-cases/
    ├── THE_100K_TREASURY_PROBLEM_SPRINT.md
    ├── USE_CASE_DEBT_IDLE_CASH_V1.md
    ├── USE_CASE_RECEIVABLES_DSO_V1.md
    ├── USE_CASE_DYNAMIC_DISCOUNTING_SCF_V1.md
    ├── USE_CASE_FX_NETTING_V1.md
    ├── USE_CASE_GUARANTEES_COLLATERAL_V1.md
    └── USE_CASE_TREASURY_OPERATIONS_COMPLIANCE_V1.md
```

Do the physical file moves only after updating references/indexes, to avoid breaking internal links/history unnecessarily.

---

## 10. Immediate sequence

1. Product Thesis v2 — done.
2. Legacy review — this document.
3. Update `PROJECT_STRUCTURE.md` to recognize v2 and planned directory migration.
4. Update founder memo/business plan rather than delete them.
5. Update technical/domain model around `Opportunity` + `RealizedValue`.
6. Create product-wide `GOLDEN_PATH_V2.md` while preserving investment golden path as a subflow.
7. Extend regulatory boundary to the four priority opportunity engines.
8. Review market/competition/GTM against new ICP before implementation.

This avoids building against obsolete assumptions while preserving the useful work already completed.
