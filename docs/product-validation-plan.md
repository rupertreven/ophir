# Ophir Product Validation Plan

> **Status:** Working plan — v0.1  
> **Scope:** Belgian corporate treasury, starting with regulated cash-management instruments and tokenized rails.

## Objective

Validate one narrow Ophir product end-to-end before broadening the company thesis.

The sequence is deliberately:

1. **Technical product design** — define exactly what Ophir does and does not do.
2. **Legal/regulatory validation** — classify every material product action and boundary.
3. **Economic/business-case validation** — prove with data whether the product creates enough value for Belgian companies.

The working principle is:

> **Ophir prepares. The company decides. The regulated provider executes. Ophir reconciles and documents.**

The initial reference use case is a Belgian SME with multiple bank accounts and surplus EUR liquidity considering a regulated short-duration cash-management instrument, with Spiko as the first concrete reference adapter rather than an exclusive product commitment.

---

## Phase 1 — Technical Product Specification

Create `docs/TECHNICAL_PRODUCT_SPEC.md` before production code.

### Reference flow

```text
Banks
  │
  ▼
Open-banking provider
  │
  ▼
Ophir normalized treasury ledger
  │
  ├── cash position
  ├── forecast
  ├── liquidity policy
  └── deployable-cash calculation
  │
  ▼
Instrument Intelligence
  │
  ├── yield / fees
  ├── risk
  ├── liquidity
  ├── legal classification
  ├── Belgian tax treatment
  └── Belgian accounting treatment
  │
  ▼
User decision / approval
  │
  ▼
Licensed provider executes
  │
  ▼
Ophir reconciliation
  │
  ├── accounting proposal
  ├── tax calculation
  ├── filing/document package
  └── immutable audit trail
```

### Technical modules to specify

1. **Identity, tenant and legal-entity model**
   - organisation;
   - Belgian legal entity;
   - users, roles and permissions;
   - accountants/advisers;
   - approval policies.

2. **Bank Connectivity Engine**
   - Ponto/alternative provider adapter;
   - accounts, balances and transactions;
   - consent lifecycle;
   - webhooks/polling;
   - normalized bank data model.

3. **Accounting Connectivity Engine**
   - Exact Online, Odoo, Yuki and/or unified API adapters;
   - chart-of-accounts mapping;
   - invoices/AP/AR where useful for forecasting;
   - journal proposal/export;
   - supporting-document links.

4. **Normalized Treasury Ledger**
   - bank money;
   - stablecoins;
   - fund units/securities;
   - pending settlements;
   - fees, tax and accrued income;
   - immutable source references.

5. **Treasury Engine**
   - current cash position;
   - deterministic short-term forecast first;
   - minimum operating liquidity;
   - policy buffer;
   - deployable cash;
   - scenario analysis.

6. **Instrument Knowledge Graph**
   - instrument and share-class identity;
   - ISIN;
   - issuer/fund/provider;
   - domicile and currency;
   - legal/regulatory classification;
   - underlying assets;
   - risk indicators;
   - NAV/yield/fees;
   - minimum ticket;
   - subscription/redemption rules;
   - settlement and liquidity;
   - tokenization/network metadata where relevant;
   - source provenance and effective dates.

7. **Belgian Rules Engine**
   - rules depend on legal entity + instrument + event + date;
   - events include subscription, holding, valuation, income, redemption and transfer;
   - tax rules;
   - accounting rules;
   - reporting/filing rules;
   - legal source, version and effective-date tracking;
   - deterministic calculation core; AI may explain but not invent rules.

8. **Document & Compliance Engine**
   - accounting-entry proposal;
   - tax calculation worksheet;
   - declaration/form preparation where legally permissible;
   - exact field/code guidance where validated;
   - filing deadline;
   - payment instructions/reference where applicable;
   - supporting evidence pack;
   - accountant review pack;
   - versioned source/legal basis.

9. **Provider Adapter Layer**
   - Spiko as first reference adapter;
   - public market/instrument data;
   - investor/account data with consent;
   - onboarding/deep-link/embedded handoff;
   - post-trade transaction and position retrieval;
   - future providers behind a common interface.

10. **Execution Boundary**
    - Ophir does not silently execute an investment;
    - the authorised company user makes the final decision;
    - regulated execution remains with the licensed provider;
    - prefer provider-hosted/embedded approval or explicit deep-link handoff;
    - record decision, handoff and resulting transaction as separate audit events.

11. **Security & Audit**
    - encryption;
    - secrets management;
    - RBAC;
    - least privilege;
    - immutable audit events;
    - source-data lineage;
    - provider-consent records;
    - human approval evidence;
    - incident logging;
    - EU data-residency assumptions to validate.

12. **AI Boundary**
    - AI explains data and rules;
    - AI can draft scenarios and documentation;
    - deterministic engines calculate money, tax and compliance outputs;
    - AI output must cite the underlying rule/data source;
    - no autonomous investment execution in v1.

### Phase-1 deliverable

A specification detailed enough that:

- an engineer can implement the MVP;
- counsel can review each flow/button/API boundary;
- an accountant can validate the ledger and document outputs;
- a CFO can understand exactly what happens to company money and data.

---

## Phase 2 — Legal & Regulatory Validation

Do not perform a generic MiCA memo. Review the exact product specified in Phase 1.

### Classify every product action

At minimum:

| Product action | Legal question |
|---|---|
| Retrieve bank balances | AISP/open-banking perimeter and partner model |
| Retrieve accounting data | software/data-processing obligations |
| Calculate cash forecast | software vs regulated activity |
| Show instrument data | information vs promotion/advice |
| Compare yield/liquidity/cost | when does comparison become personalised advice? |
| Calculate after-tax return | information/tax-tool vs regulated professional advice |
| Determine instrument eligibility | information, distribution or advice? |
| Facilitate onboarding | introducer/distributor responsibilities |
| Prepare transaction handoff | reception/transmission/order-execution boundary |
| User approves at provider | responsibility and evidence |
| Retrieve executed transaction | data/reconciliation boundary |
| Generate journal entries | accounting-service perimeter |
| Generate tax calculations/forms | tax-profession/liability perimeter |
| Generate filing instructions | responsibility, disclaimers and review requirements |
| AI explanation | liability and human-review requirements |

### Frameworks to map

- MiFID II / Belgian implementation;
- MiCA where crypto-assets/services are relevant;
- PSD2 and successor payment/open-finance rules;
- UCITS/MMF rules for fund products;
- AML/KYC responsibilities;
- GDPR;
- DORA/vendor expectations;
- Belgian corporate tax;
- Belgian transaction taxes and securities-account taxes where applicable;
- Belgian accounting law and Belgian GAAP;
- Belgian rules on regulated accounting/tax professions;
- consumer rules only if the product ever leaves the B2B corporate scope.

### Required output

`docs/REGULATORY_BOUNDARY_V1.md`

Every significant UI action and API flow receives:

- Green / Amber / Red classification;
- legal rationale;
- responsible regulated party;
- required disclosure/consent;
- evidence/audit requirement;
- legal source;
- counsel-validation status.

No production execution flow ships while its boundary remains materially ambiguous.

---

## Phase 3 — Economic & Business-Case Validation

The product must create measurable value **today**, not merely depend on a future tokenization narrative.

### Core research question

For a Belgian company with surplus EUR liquidity, what is the true economic and operational difference between:

1. current account;
2. savings/notice/term deposit available to corporates;
3. traditional EUR money-market fund;
4. regulated tokenized EUR money-market fund;
5. short-duration government-bond alternatives;
6. stablecoin cash rail such as EURC where operationally relevant?

### Do not compare only `tokenized fund vs cash`

Where possible compare:

> **the same economic exposure on traditional rails versus tokenized rails**

This isolates the value created by tokenization itself.

### Data fields

For each product/provider capture:

- eligibility for Belgian corporate investors;
- minimum investment;
- gross/current yield;
- management/product fees;
- subscription/redemption fees;
- bank/payment/on-off-ramp costs;
- FX costs if any;
- Belgian tax consequences;
- settlement time;
- time to usable EUR in the company's bank account;
- weekend/after-hours liquidity;
- redemption limits;
- NAV volatility;
- credit/duration/liquidity risk;
- custody model;
- investor-protection structure;
- operational steps;
- accounting burden;
- tax/reporting burden;
- API availability;
- automation potential;
- collateral/programmability benefits where real;
- evidence/source date.

### Standard company scenarios

Model at least:

- €100k surplus for 30 / 90 / 180 days;
- €500k surplus for 30 / 90 / 180 days;
- €1m surplus for 30 / 90 / 180 days;
- predictable vs uncertain cash needs;
- normal business day vs weekend liquidity event.

### Ophir metric: Net Treasury Benefit

Build a transparent calculation such as:

```text
Gross investment return
- product fees
- transaction/on-off-ramp fees
- tax cost
- estimated operational/admin cost
- liquidity/risk penalty where explicitly modelled
+ quantified finance-team time saved
= Net Treasury Benefit
```

Never hide assumptions behind an AI score.

### Hypotheses to test

**H1 — Return:** regulated alternatives materially improve return on otherwise idle corporate cash.

**H2 — Liquidity:** tokenized rails improve operational liquidity/settlement enough to matter to a normal Belgian company.

**H3 — Administration:** Ophir materially reduces reconciliation, accounting, tax and compliance work.

**H4 — Programmability:** tokenized ownership/settlement creates a concrete current benefit, not merely future optionality.

**H5 — Willingness to pay:** the combination of incremental return + reduced administrative work comfortably exceeds Ophir's annual price.

### Kill / pivot conditions

Reconsider the product if research shows that:

- Belgian banks routinely offer comparable net yield with materially lower complexity;
- tax/transaction costs erase the return advantage;
- redemption-to-bank liquidity is too weak for treasury use;
- corporate accounting/tax overhead overwhelms operational savings;
- tokenization itself provides no meaningful current benefit and customers do not value future optionality;
- regulated distribution restrictions make the intended UX impractical;
- customers will not pay enough to support the required legal/security/integration burden.

---

## Research principle

Ophir is not a product designed to push companies onchain.

The system should be indifferent to the rail and instrument. If a Belgian bank deposit is the economically superior choice for a given company and horizon, Ophir should make that visible. If a regulated tokenized fund is superior, Ophir should make the legal, tax, accounting and operational consequences equally visible.

> **The product is trusted treasury intelligence and administrative orchestration; tokenization is one potentially superior rail, not the ideology.**
