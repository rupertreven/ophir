# Ophir Golden Path Sequence

> **Status:** Draft v0.1
> **Reference use case:** Belgian SME with surplus EUR cash using a regulated money-market-fund provider.

## 1. Objective

Define the exact end-to-end sequence for the first Ophir product so engineering, legal counsel and accounting reviewers can evaluate the same concrete workflow.

The path intentionally preserves a hard execution boundary:

> **Ophir analyses and prepares. The authorised company user approves. The licensed provider executes. Ophir observes, reconciles and documents.**

---

## 2. Actors

- **Company user** — CFO/finance manager authorised by the customer.
- **Ophir Web App** — customer-facing UI.
- **Ophir API** — application backend.
- **Bank Adapter** — Ponto or equivalent regulated/open-banking provider.
- **Accounting Adapter** — Exact Online / Odoo / Yuki / unified provider.
- **Treasury Engine** — cash and deployable-liquidity calculations.
- **Instrument Service** — factual product/instrument data.
- **Rules Engine** — deterministic Belgian tax/accounting/reporting logic.
- **Investment Provider Adapter** — Spiko as first reference adapter.
- **Licensed Provider UI/API** — regulated onboarding/order/execution boundary.
- **Document Engine** — journal/tax/filing/audit package generation.
- **Audit Service** — append-only evidence trail.

---

## 3. Phase A — Connect company data

### A1. Create legal entity

1. User creates/selects organisation.
2. User creates Belgian legal entity.
3. Ophir stores enterprise number, VAT number, accounting framework and fiscal year.
4. Audit event: `LEGAL_ENTITY_CREATED`.

### A2. Connect bank accounts

1. User chooses `Connect bank`.
2. Ophir creates provider connection intent.
3. User is redirected to / embedded into the bank/open-banking provider consent flow.
4. Provider handles authentication and bank consent.
5. Provider returns authorised account references/token/consent metadata.
6. Ophir stores only secret references in vault/KMS.
7. Ophir synchronises account metadata, available/booked balances and transactions.
8. Raw source payload/evidence reference is preserved.
9. Normalized `financial_account`, `account_balance_snapshot` and `cash_transaction` records are created.
10. Audit events record consent, connection and sync.

**Boundary:** Ophir does not impersonate the user at the bank. Bank authentication/consent remains in the regulated provider/bank flow.

### A3. Connect accounting system

1. User chooses accounting provider.
2. OAuth/provider consent occurs.
3. Ophir retrieves chart of accounts and permitted accounting data.
4. Optional inputs for v1 forecasting: open AP, open AR, tax/payroll/debt obligations where available and relevant.
5. Ophir creates semantic mapping suggestions.
6. User/accountant confirms mappings.
7. Audit event: `ACCOUNTING_CONNECTION_ACTIVE` and mapping approvals.

---

## 4. Phase B — Build current treasury position

### B1. Normalize cash

1. Scheduler/webhook triggers bank sync.
2. Adapter fetches new balances/transactions using cursor/watermark.
3. Idempotency checks reject duplicate provider events.
4. Ophir updates the projected current position from immutable records.
5. Reconciliation controls compare provider balance to normalized transaction history where feasible.

### B2. Build cash forecast

Inputs may include:
- current available cash;
- open supplier invoices;
- expected receivables;
- payroll;
- VAT/tax payments;
- debt service;
- manual finance-team adjustments;
- entity-specific recurring items.

The v1 forecast is deterministic and explainable.

Output example:

```text
Available bank cash           1,200,000 EUR
Expected 30d outflows          -550,000 EUR
Expected 30d inflows           +180,000 EUR
Minimum policy buffer          -250,000 EUR
--------------------------------------------
Deployable cash                 580,000 EUR
```

Every line links to source records or an explicit policy/manual assumption.

### B3. Create deployable-cash snapshot

Ophir persists:
- source balance snapshot ids;
- forecast version;
- policy version;
- horizon;
- computed deployable cash;
- timestamp and algorithm version.

Audit event: `DEPLOYABLE_CASH_CALCULATED`.

---

## 5. Phase C — Build factual instrument comparison

### C1. Retrieve instrument data

Instrument Service reads/provider-syncs:
- share-class identity and ISIN;
- currency;
- current NAV/yield metrics;
- fees;
- minimum ticket;
- subscription/redemption rules;
- settlement/liquidity characteristics;
- risk/product classifications;
- tokenization/network metadata if applicable.

Every displayed metric includes an `as_of` timestamp/source.

### C2. Evaluate Belgian rules

For the selected legal entity, amount, horizon and candidate instrument, the Rules Engine evaluates relevant validated rule versions.

Possible outputs:
- expected tax treatment;
- transaction-tax treatment;
- accounting classification options;
- proposed journal logic;
- reporting/filing obligations;
- known uncertainties requiring professional review.

The Rules Engine returns structured facts, not free-text legal guesses.

### C3. Calculate treasury scenario

Example fields:

```text
Amount                               500,000 EUR
Horizon                                   90 days
Current indicative yield                  2.13%
Estimated product fees                  included
Estimated gross return                 2,626 EUR
Estimated taxes/transaction costs        XXX EUR
Estimated admin cost                     XXX EUR
Expected net treasury benefit          X,XXX EUR
Redemption / settlement              T+? / rules
Operational liquidity              structured fact
Rule confidence                  validated/review needed
```

If a bank deposit comparison is available, it appears alongside the fund under the same calculation methodology.

### C4. Present information

The UI should distinguish:
- provider/product facts;
- Ophir calculations;
- customer assumptions/policies;
- validated legal/tax/accounting rules;
- unresolved legal/professional-review questions.

Avoid wording that implies guaranteed yield or unlicensed personalised investment advice.

Audit event: `TREASURY_SCENARIO_GENERATED`.

---

## 6. Phase D — Company chooses to proceed

### D1. Create transaction intent

The user selects a factual scenario and clicks an action such as `Prepare investment` / legally reviewed wording.

Ophir creates `transaction_intent` with status `DRAFT`.

The intent captures:
- legal entity;
- selected instrument/provider;
- proposed amount;
- scenario/rule versions;
- current disclosures;
- creator.

It is explicitly **not an order**.

### D2. Internal company approval

If policy requires approval:

1. Intent → `AWAITING_INTERNAL_APPROVAL`.
2. Required approver authenticates.
3. Ophir shows amount, instrument facts, source timestamp, liquidity/tax/accounting consequences and provider handoff notice.
4. Approver approves or rejects.
5. Immutable approval event is stored with auth context and policy version.
6. Once policy is satisfied, intent → `APPROVED_FOR_HANDOFF`.

**Boundary:** this is an internal corporate control, not execution of the financial transaction.

---

## 7. Phase E — Regulated execution handoff

### E1. Prepare provider session

Depending on provider model:

- Ophir requests/creates an authorised provider session/JWT/deep link;
- session is scoped to the legal entity/user;
- raw regulated-provider credentials remain external or securely vaulted;
- terms/disclosures shown at handoff are versioned.

### E2. Transfer control to licensed provider

Supported patterns:
- embedded provider-owned UI;
- redirect/deep link;
- provider-hosted transaction page;
- manual step-by-step guide as fallback.

Ophir records `execution_handoff` and changes intent to `HANDED_OFF`.

**Hard invariant:** Ophir's backend does not call a generic `executeTrade()` or confirm the order on behalf of the investor in v1.

### E3. User executes with provider

The provider is responsible for the regulated execution flow, including any required:
- KYC/KYB;
- eligibility;
- disclosures;
- investor confirmation;
- order creation;
- settlement instructions.

The user gives final provider-side confirmation.

### E4. Provider executes and settles

Possible fiat path:

```text
Company bank account
  -> provider/fund subscription account
  -> fund units issued
```

Possible stablecoin path, if supported and legally/product-wise applicable:

```text
Company-authorised wallet / regulated rail
  -> EURC/other supported settlement asset
  -> fund subscription
  -> fund units issued
```

Ophir never becomes beneficial owner of customer cash or fund units.

---

## 8. Phase F — Observe execution result

### F1. Retrieve provider transaction

Via provider webhook or polling:

1. Adapter receives subscription/order/settlement update.
2. Signature/authenticity is verified.
3. Provider external id is checked for idempotency.
4. Source evidence is preserved.
5. Ophir creates/updates canonical `economic_event`.

Intent becomes `COMPLETED_EXTERNALLY` only when external evidence confirms completion/settlement according to defined rule.

### F2. Update position

The confirmed economic event updates the projected position:
- units;
- acquisition amount;
- settlement date;
- carrying/market value metadata.

### F3. Reconcile cash movement

Bank sync later observes the related EUR debit/credit.

Ophir attempts deterministic matching using:
- amount;
- date/window;
- provider reference;
- counterparty;
- instrument intent id if available.

If confidence is insufficient, user reviews reconciliation.

Audit event: `EXTERNAL_TRANSACTION_RECONCILED`.

---

## 9. Phase G — Generate Belgian accounting and tax outputs

### G1. Rule evaluation

Rules Engine receives:
- legal entity tax/accounting profile;
- instrument/share class classification;
- economic event;
- transaction/effective date;
- relevant source facts.

It runs exact effective-dated validated rules.

### G2. Accounting entry proposal

Example structure only — exact Belgian accounts/classification require validation:

```text
Dr Financial investment / appropriate BE GAAP account   500,000
Cr Bank                                                  500,000
```

Output includes:
- proposed accounts;
- debit/credit lines;
- description;
- economic-event id;
- applied accounting-rule version;
- source documents;
- review status.

Accountant/CFO can approve or amend mapping before export.

### G3. Tax obligation calculation

If a validated rule determines an obligation:

Ophir generates:
- tax type;
- taxable base;
- rate;
- calculated amount;
- due date;
- filing obligation;
- exact legal source/rule version.

If the answer depends on facts Ophir does not know, output is `NEEDS_REVIEW`, not guessed.

### G4. Filing instruction/package

Where legally and technically validated, Ophir prepares:
- declaration/form name;
- period;
- exact field/code;
- amount/value;
- deadline;
- payment instructions/reference where applicable;
- source documents;
- rule citations;
- reviewer field.

Status begins `DRAFT` or `NEEDS_REVIEW` depending on validation level.

Ophir does not mark it `FILED_EXTERNALLY` without evidence/user confirmation of filing.

### G5. Accounting export

If approved by the customer/accountant, Ophir can:
- export structured journal lines;
- push an allowed journal proposal through the accounting adapter where supported and legally validated;
- attach/link evidence.

All writes require explicit user authority and are separately audited.

---

## 10. Phase H — Ongoing holding

On each relevant valuation date:

1. Instrument metrics/NAV refresh.
2. Position market value is recalculated.
3. Accounting rules determine whether/how valuation entries are required.
4. Tax/reporting rules determine whether any obligation exists.
5. Treasury Engine includes position liquidity in scenario calculations subject to policy haircut.
6. Source/rule versions remain reproducible.

Ophir may generate factual alerts such as:
- liquidity threshold breached;
- yield changed materially;
- redemption needed to satisfy forecast;
- regulatory/tax rule changed;
- filing deadline approaching.

---

## 11. Phase I — Redemption

### I1. Forecast triggers need for cash

Example:
- large payroll/tax/vendor outflow expected;
- liquidity policy indicates a shortfall unless investment is redeemed.

Ophir calculates:
- amount required;
- timing requirement;
- factual redemption characteristics;
- expected tax/accounting consequences.

### I2. User creates redemption intent

Same internal approval state machine as subscription.

### I3. Provider handoff

User completes final redemption instruction with the licensed provider.

### I4. Provider confirms redemption/settlement

Ophir records canonical economic events, reconciles the returning cash and adjusts the position.

### I5. Generate closing outputs

Rules Engine calculates where applicable:
- realised gain/loss;
- income treatment;
- fees;
- tax obligations;
- accounting entries;
- filing instructions.

Document Engine creates a complete audit/accountant/tax pack.

---

## 12. Sequence diagram

```text
User       Ophir UI/API     Bank/Acct      Treasury/Rules      Provider       Docs
 |              |               |                |                 |             |
 |--connect---->|-------------->|                |                 |             |
 |              |<--data--------|                |                 |             |
 |              |------------------------------->|                 |             |
 |              |<--deployable cash/scenario-----|                 |             |
 |<--facts------|                                 |                 |             |
 |--select----->|                                 |                 |             |
 |--approve---->|                                 |                 |             |
 |              |----------------------------------------------->|               |
 |              |           execution handoff                    |               |
 |------------------------------------------------------------->|               |
 |              |                    user confirms at provider    |               |
 |              |<--------------------------------------status----|               |
 |              |------normalize/reconcile------------>|         |               |
 |              |<-----tax/accounting evaluation-------|         |               |
 |              |------------------------------------------------------------->|
 |<----------------------review/export/file package--------------------------------|
```

---

## 13. Failure paths

### Provider unavailable
- do not infer execution;
- keep intent in `HANDED_OFF` or provider-specific pending state;
- notify user;
- reconcile only after authoritative evidence.

### Bank data stale
- show freshness prominently;
- prevent deployable-cash result from being treated as current beyond configured threshold;
- optionally block handoff if policy requires fresh balances.

### Rule uncertainty
- result marked `NEEDS_REVIEW`;
- do not generate a falsely authoritative filing instruction;
- expose missing fact/source.

### Duplicate webhook
- external event id/idempotency key makes processing safe.

### Amount mismatch
- transaction is not auto-reconciled;
- create reconciliation exception.

### Rule changes after transaction
- historical output retains historical rule version;
- new rule may generate a review alert if retroactive effect is possible.

---

## 14. Legal review checklist per step

For every numbered step above counsel should identify:

1. Actor performing the regulated/legal act.
2. Whether Ophir is providing information, recommendation, transmission, execution, accounting/tax service or pure software.
3. Required licence/registration, if any.
4. Required customer consent/disclosure.
5. Whether provider contract must allocate responsibility explicitly.
6. Required evidence/retention.
7. Wording/UI constraints.
8. Whether the action can remain Green, requires Amber partner/counsel controls, or is Red for Ophir v1.

This document becomes the input to `REGULATORY_BOUNDARY_V1.md`.

---

## 15. Golden-path acceptance criteria

A sandbox/demo passes when one Belgian test entity can:

1. connect a bank account;
2. import balances/transactions;
3. connect/import accounting data;
4. calculate deployable cash with traceable inputs;
5. retrieve one supported fund's current factual metrics;
6. evaluate a versioned Belgian rule set;
7. generate a reproducible net-benefit scenario;
8. create and internally approve a transaction intent;
9. hand off to a sandbox regulated provider without Ophir executing;
10. retrieve the external result;
11. reconcile the related cash/investment event;
12. generate an accounting proposal;
13. generate a tax/filing package with rule/source provenance;
14. produce a complete audit timeline from data ingestion through post-trade documentation.

Until this path works, adding additional chains, funds, AI autonomy or provider breadth is secondary.
