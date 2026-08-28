# Ophir Project Structure

> **Created:** 2026-08-28 23:12 CEST  
> **Status:** Living index and documentation protocol  
> **Repository:** `rupertreven/ophir`  
> **Working branch:** `docs/initial-business-plan`

## 1. Purpose

This file is the canonical map of the Ophir research/product repository. It should make it possible for the founder, an AI coding/research agent, engineer, accountant, tax professional or counsel to understand:

- what each document is for;
- which documents are authoritative versus exploratory;
- what has already been researched;
- what remains unresolved;
- where new findings belong;
- the current build/research sequence.

## 2. Documentation protocol

### Every substantive Ophir conversation output

When a conversation produces a substantive Ophir decision, research finding, calculation, specification or plan:

1. write it to the appropriate Git document in the same working session;
2. date the document/update where practical;
3. preserve evidence level and unresolved assumptions;
4. report in the chat response exactly **whether and how it was written to Git**, including file and commit where available.

### Every assistant message in the Ophir project

Every assistant response should visibly include:

- **Date:** local Belgian date/time when useful, at minimum date;
- **Git status:** `Written`, `Updated`, or `Not written — no substantive project change`;
- file path(s) and commit SHA(s) for writes.

### Evidence levels

Never collapse research into validated rules.

Use at least:

- `PUBLIC_SOURCE_RESEARCH`
- `NEEDS_REVIEW`
- `PROFESSIONAL_REVIEWED`
- `COUNSEL_VALIDATED`
- `SUPERSEDED`

Tax/legal/accounting calculations shown as filing-grade must meet the validation level defined by the relevant product rule.

## 3. Repository structure

```text
README.md

docs/
├── PROJECT_STRUCTURE.md
│
├── founder-memo.md
├── business-plan.md
├── market.md
├── competition.md
├── go-to-market.md
│
├── product-validation-plan.md
├── TECHNICAL_PRODUCT_SPEC.md
├── DOMAIN_MODEL_V1.md
├── GOLDEN_PATH_SEQUENCE.md
│
├── regulatory.md
├── REGULATORY_BOUNDARY_V1.md
│
├── banking-tokenized-rails.md
├── ECONOMIC_VALIDATION_V1.md
│
├── BELGIAN_FUND_TAX_ACCOUNTING_RESEARCH_PLAN.md
├── BELGIAN_TAX_FINDINGS_V1.md
├── SPIKO_BELGIAN_INSTRUMENT_DOSSIER_V0.md
├── BELGIAN_OPTIMAL_CASH_INSTRUMENTS_V1.md
└── BELGIAN_CANDIDATE_FUND_TAX_TEARDOWN_V1.md
```

This is the current research structure. Application/code directories will be added only when implementation begins.

## 4. Strategic documents

### `founder-memo.md`
Ophir's constitutional thesis: why the company exists, long-term direction, operating philosophy and core product principles.

### `business-plan.md`
Structured business-plan framework. Should increasingly reference validated market, product, regulatory and economic work rather than duplicate it.

### `market.md`
Bottom-up Belgian/EU market sizing and assumptions.

### `competition.md`
Competitive landscape across treasury SaaS, banking, crypto/tokenized infrastructure and related providers.

### `go-to-market.md`
ICP, Belgian beachhead, discovery, design-partner approach, pricing hypotheses and kill criteria.

## 5. Product and technical documents

### `product-validation-plan.md`
Canonical sequence:

1. technical product;
2. legal/regulatory validation;
3. economic/business-case validation.

### `TECHNICAL_PRODUCT_SPEC.md`
Primary technical build specification. Defines architecture, modules, adapters, treasury engine, rules engine, document engine, AI boundary, security and MVP.

### `DOMAIN_MODEL_V1.md`
Canonical domain entities/states/relationships. Important invariant:

```text
transaction_intent
 -> internal approval
 -> execution_handoff
 -> external confirmation
 -> reconciliation
```

No generic Ophir `trade` or `executeTrade()` primitive in v1.

### `GOLDEN_PATH_SEQUENCE.md`
Exact end-to-end user/system sequence from bank/accounting connection through deployable-cash calculation, instrument comparison, user approval, regulated-provider execution, reconciliation and Belgian tax/accounting output.

## 6. Regulatory documents

### `regulatory.md`
Initial Belgium/EU regulatory research and perimeter memo.

### `REGULATORY_BOUNDARY_V1.md`
Feature-by-feature Green / Amber / Red classification against the golden path.

Core v1 principle:

> **Ophir prepares. The company decides. The regulated provider executes. Ophir observes, reconciles and documents.**

## 7. Banking / tokenized rails

### `banking-tokenized-rails.md`
Research on open-banking, accounting connectors, fiat/stablecoin rails and partner-first architecture.

Key direction:

- use licensed open-banking/payment/investment infrastructure;
- Ophir owns intelligence, orchestration, compliance/accounting context and UX;
- avoid unnecessary regulated balance-sheet/custody/execution roles.

## 8. Economic validation

### `ECONOMIC_VALIDATION_V1.md`
Initial live-data comparison of Belgian corporate cash alternatives, including the EUR 2m / ~92-day scenario.

### `BELGIAN_FUND_TAX_ACCOUNTING_RESEARCH_PLAN.md`
Research plan required to convert indicative gross comparisons into Belgian corporate after-tax outcomes.

### `BELGIAN_TAX_FINDINGS_V1.md`
Public-source Belgian TOB, annual securities-account tax and filing-workflow findings. Findings are explicitly not automatically production rules.

### `SPIKO_BELGIAN_INSTRUMENT_DOSSIER_V0.md`
First instrument-level Belgian dossier for the Spiko reference products.

### `BELGIAN_OPTIMAL_CASH_INSTRUMENTS_V1.md`
Search for regulated/API-accessible cash instruments whose wrapper, liquidity and tax treatment may be better suited to Belgian corporate treasury.

### `BELGIAN_CANDIDATE_FUND_TAX_TEARDOWN_V1.md`
Comparison of current candidate wrappers/products and short-horizon break-even economics.

Key current insight:

> **Tokenization is not automatically yield alpha. Wrapper/instrument selection can create tax/yield alpha; tokenization can create operational alpha; Ophir aims to create intelligence/compliance alpha.**

## 9. Current product thesis

Ophir should be rail-neutral.

It should answer:

> **Given this Belgian legal entity, its bank cash, forecast, liquidity policy, current bank quote, available regulated instruments, tax treatment, accounting treatment and execution rails: what are the economically rational options, and what administration follows from each?**

The product should be able to conclude that keeping cash in a bank is optimal.

## 10. Current highest-priority research

1. Find Belgian-tax-efficient EUR short-term regulated fund wrappers, especially FCP/contractual or equivalent structures.
2. Validate exact TOB treatment by ISIN/share class and transaction type.
3. Validate TACT applicability from actual custody/account structures.
4. Validate corporate-income-tax and withholding mechanics.
5. Define Belgian GAAP/MAR treatment per economic event.
6. Compare real negotiated Belgian corporate deposit quotes against fund alternatives.
7. Compare traditional versus tokenized access to the same fund to isolate operational alpha.
8. Quantify the value of accounting/tax/document automation separately from investment yield.

## 11. Planned future documents

Likely next artefacts:

```text
docs/
├── INSTRUMENT_DOSSIERS/
│   ├── <ISIN>.md
│   └── ...
├── BELGIAN_ACCOUNTING_RULES_V1.md
├── BELGIAN_TAX_RULES_V1.md
├── NET_TREASURY_BENEFIT_MODEL.md
├── PROVIDER_INTEGRATION_MATRIX.md
├── SECURITY_ARCHITECTURE_V1.md
└── MVP_BUILD_PLAN.md
```

Create these only when the underlying work begins; avoid empty-document bureaucracy.

## 12. Source-of-truth hierarchy

When documents conflict, prefer in this order:

1. professionally/counsel-validated effective-dated rule or instrument dossier;
2. latest technical/regulatory specification;
3. latest public-source finding;
4. research plan/hypothesis;
5. founder/business-plan narrative.

A newer finding does not automatically become a validated rule.

## 13. Update rule

Update this structure document whenever:

- a major document is created/renamed;
- project phases change;
- a new source-of-truth category is introduced;
- implementation begins and code directories are added;
- a major product invariant changes.
