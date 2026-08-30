# Ophir Technical Product Specification

> **Status:** Working specification — v0.1  
> **Scope:** Belgian B2B corporate treasury MVP  
> **Primary use case:** Aggregate bank and accounting data, identify surplus liquidity, model regulated cash-management alternatives, prepare compliance/accounting outputs, hand execution to a licensed provider, then reconcile the result.

---

# 1. Product Principle

Ophir is a treasury intelligence and administrative orchestration layer.

It is **not** initially:

- a bank;
- a custodian;
- an exchange;
- a broker;
- an investment manager;
- an autonomous execution agent;
- a system that takes possession of customer funds or private keys.

The core control boundary is:

> **Ophir prepares. The company decides. The regulated provider executes. Ophir reconciles and documents.**

This boundary is both a product principle and a technical architecture requirement.

---

# 2. MVP Outcome

A Belgian company should be able to:

1. connect its bank accounts;
2. connect its accounting system;
3. see a normalized consolidated cash position;
4. estimate near-term cash requirements;
5. calculate deployable surplus cash under company-defined policies;
6. compare supported cash-management instruments using transparent data;
7. see estimated fees, liquidity, Belgian tax/accounting implications and operational steps;
8. open or continue a transaction with a licensed external provider;
9. explicitly approve and execute the transaction with that provider;
10. have Ophir detect/retrieve the resulting transaction;
11. reconcile the new position;
12. generate an accounting and compliance package with supporting evidence.

The MVP is successful if this workflow is reliable and valuable for one narrow set of Belgian corporate treasury cases.

---

# 3. Non-Goals for v1

The following are explicitly out of scope unless later legal review changes the boundary:

- autonomous investment execution;
- custody of securities, stablecoins or fiat;
- storage of private keys;
- personalised discretionary portfolio management;
- unrestricted investment recommendations;
- direct tax filing on behalf of customers;
- direct bookkeeping entry posting without customer/accountant approval;
- consumer use cases;
- complex derivatives;
- DeFi yield farming;
- unsecured lending;
- multi-jurisdiction tax support beyond Belgium.

---

# 4. Reference Architecture

```text
                           ┌──────────────────────┐
                           │       Ophir UI       │
                           └──────────┬───────────┘
                                      │
                          ┌───────────▼───────────┐
                          │   Ophir Application   │
                          │        API            │
                          └───────────┬───────────┘
                                      │
      ┌──────────────┬────────────────┼────────────────┬───────────────┐
      │              │                │                │               │
┌─────▼─────┐  ┌─────▼──────┐  ┌─────▼─────┐  ┌──────▼──────┐ ┌─────▼─────┐
│ Banking   │  │ Accounting │  │ Treasury  │  │ Instrument  │ │ Rules &   │
│ adapters  │  │ adapters   │  │ Engine    │  │ Intelligence│ │ Documents │
└─────┬─────┘  └─────┬──────┘  └─────┬─────┘  └──────┬──────┘ └─────┬─────┘
      │              │                │                │               │
  Ponto/...      Exact/Odoo/...   Forecast/policy  Spiko/...      BE tax/GAAP
      │              │                │                │               │
      └──────────────┴────────────────┴───────────────┴───────────────┘
                                      │
                              ┌───────▼────────┐
                              │ Normalized     │
                              │ Treasury Ledger│
                              └───────┬────────┘
                                      │
                              ┌───────▼────────┐
                              │ Audit/Event Log│
                              └────────────────┘
```

The architecture should begin as a modular monolith unless scale or team structure creates a real reason to split services.

---

# 5. Recommended Initial Stack

The stack is a working recommendation, not a permanent constraint.

## Application

- **Frontend:** Next.js + TypeScript
- **Backend:** TypeScript/Node.js service layer
- **Database:** PostgreSQL
- **ORM:** Prisma or equivalent strongly typed ORM
- **Queue/jobs:** PostgreSQL-backed jobs initially; dedicated queue only when necessary
- **Object storage:** EU-region S3-compatible storage
- **Authentication:** managed OIDC provider with MFA support
- **Observability:** structured logs + metrics + tracing
- **Deployment:** EU-region cloud infrastructure

## Architecture rule

Prefer boring, auditable infrastructure over novelty.

Financial correctness, provenance and deterministic behaviour matter more than microservice purity.

---

# 6. Core Domain Model

## 6.1 Tenant

Represents the Ophir customer organisation.

```ts
Tenant {
  id
  name
  status
  baseCurrency
  createdAt
  updatedAt
}
```

A tenant can contain multiple legal entities.

## 6.2 LegalEntity

Represents a specific company whose treasury is managed.

```ts
LegalEntity {
  id
  tenantId
  legalName
  enterpriseNumber
  countryCode
  legalForm
  accountingCurrency
  fiscalYearEnd
  vatNumber
  status
}
```

For v1, Belgian entities are first-class and other jurisdictions are unsupported unless marked experimental.

## 6.3 User

```ts
User {
  id
  tenantId
  email
  displayName
  status
  mfaEnabled
}
```

## 6.4 RoleAssignment

```ts
RoleAssignment {
  userId
  legalEntityId?
  role
}
```

Initial roles:

- `OWNER`
- `CFO`
- `FINANCE_ADMIN`
- `ACCOUNTANT`
- `VIEWER`
- `AUDITOR`

Execution rights should not be implied by an Ophir role when the actual transaction is executed externally.

---

# 7. Banking Domain

## 7.1 BankConnection

```ts
BankConnection {
  id
  legalEntityId
  provider
  providerConnectionId
  status
  consentExpiresAt
  lastSyncedAt
  capabilities[]
}
```

Capabilities can include:

- `ACCOUNT_INFORMATION`
- `TRANSACTIONS`
- `BALANCES`
- `PAYMENT_INITIATION`

Payment initiation is disabled in the initial product unless separately validated.

## 7.2 BankAccount

```ts
BankAccount {
  id
  legalEntityId
  bankConnectionId
  providerAccountId
  iban
  bic
  bankName
  accountName
  currency
  accountType
  status
}
```

## 7.3 BankBalanceSnapshot

```ts
BankBalanceSnapshot {
  id
  bankAccountId
  availableAmount
  bookedAmount
  currency
  observedAt
  sourcePayloadHash
}
```

Never overwrite history. Balance snapshots are time-series observations.

## 7.4 BankTransaction

```ts
BankTransaction {
  id
  bankAccountId
  providerTransactionId
  bookedAt
  valueDate
  amount
  currency
  counterpartyName
  counterpartyIban
  remittanceInformation
  rawCategory
  normalizedCategory
  sourcePayloadHash
}
```

Provider IDs plus account IDs must form an idempotency boundary.

---

# 8. Accounting Domain

## 8.1 AccountingConnection

```ts
AccountingConnection {
  id
  legalEntityId
  provider
  providerCompanyId
  status
  lastSyncedAt
}
```

## 8.2 LedgerAccountMapping

Maps provider chart-of-account entries into Ophir concepts.

```ts
LedgerAccountMapping {
  id
  legalEntityId
  providerAccountCode
  providerAccountName
  ophirCategory
  confidence
  reviewedByUserId?
}
```

## 8.3 Payable / Receivable

Ophir may ingest only the fields required for forecasting.

```ts
OpenItem {
  id
  legalEntityId
  type // PAYABLE | RECEIVABLE
  sourceSystem
  sourceId
  amount
  currency
  dueDate
  counterparty
  status
}
```

## 8.4 JournalProposal

Ophir proposes; the user/accountant approves or exports.

```ts
JournalProposal {
  id
  legalEntityId
  eventId
  status // DRAFT | REVIEWED | EXPORTED | REJECTED
  accountingFramework
  effectiveDate
  explanation
}

JournalLine {
  id
  journalProposalId
  accountCode
  debit
  credit
  currency
  description
}
```

The calculation source and applicable rule version must be attached.

---

# 9. Normalized Treasury Ledger

This is Ophir's internal economic truth layer.

It does not replace the statutory accounting ledger.

## 9.1 TreasuryAccount

```ts
TreasuryAccount {
  id
  legalEntityId
  type // BANK | STABLECOIN | FUND | SECURITY | SETTLEMENT
  currency
  provider
  externalReference
}
```

## 9.2 TreasuryEntry

Use double-entry semantics internally for all material value movements.

```ts
TreasuryEntry {
  id
  legalEntityId
  eventId
  accountId
  debitAmount
  creditAmount
  currency
  effectiveAt
  sourceType
  sourceId
}
```

Each economic event must balance in its transaction currency or explicitly record FX differences.

## 9.3 Position

Derived from ledger entries; do not treat provider balances as the only truth.

```ts
Position {
  legalEntityId
  instrumentId?
  treasuryAccountId
  quantity
  bookValue
  marketValue
  currency
  observedAt
}
```

---

# 10. Treasury Engine

The first version should be deterministic and explainable.

## 10.1 Inputs

- current available bank balances;
- known payables;
- known receivables;
- payroll estimates;
- VAT/tax dates where configured;
- debt-service obligations;
- recurring payments;
- manually entered expected flows;
- company liquidity policy.

## 10.2 LiquidityPolicy

```ts
LiquidityPolicy {
  id
  legalEntityId
  minimumAbsoluteCash
  minimumDaysOfOutflows
  safetyBufferAmount?
  safetyBufferPercent?
  forecastHorizonDays
  allowedCurrencies[]
}
```

## 10.3 DeployableCashCalculation

```text
Available liquid cash
- committed outflows within horizon
+ high-confidence inflows within horizon
- minimum operating cash
- policy safety buffer
= deployable cash
```

Return both the number and an explanation tree.

```ts
DeployableCashResult {
  amount
  currency
  calculatedAt
  horizonDays
  inputs[]
  policyVersionId
  confidence
}
```

The UI must allow a CFO to inspect every material assumption.

---

# 11. Forecasting

## v1

Use rules and accounting data first:

- due-date based AP/AR;
- historical recurring flows;
- payroll schedules;
- tax schedules;
- manually entered known events.

## Later

ML/AI can generate forecast suggestions, but must never silently alter policy or committed obligations.

Every AI-generated forecast component must be tagged:

```ts
ForecastItem {
  id
  sourceType // ACCOUNTING | BANK_PATTERN | MANUAL | AI_ESTIMATE
  amount
  date
  confidence
  explanation
  approved
}
```

---

# 12. Instrument Knowledge Graph

This is a strategic Ophir asset.

## 12.1 Instrument

```ts
Instrument {
  id
  name
  instrumentType
  issuerId
  domicile
  baseCurrency
  isin?
  legalClassification
  regulatoryFramework[]
  riskClass?
  status
}
```

## 12.2 ShareClass

```ts
ShareClass {
  id
  instrumentId
  isin
  currency
  minimumInvestment
  managementFeeBps
  subscriptionFeeBps
  redemptionFeeBps
  settlementSubscription
  settlementRedemption
  distributionPolicy
}
```

## 12.3 InstrumentMarketSnapshot

```ts
InstrumentMarketSnapshot {
  id
  shareClassId
  nav
  yieldMetric
  yieldValue
  yieldPeriod
  aum
  observedAt
  sourceId
}
```

## 12.4 LiquidityProfile

```ts
LiquidityProfile {
  shareClassId
  dealingFrequency
  cutoffTime
  settlementTime
  instantRedemptionLimit?
  weekendAvailability
  providerRestrictions
  effectiveFrom
}
```

## 12.5 TokenizationMetadata

Optional.

```ts
TokenizationMetadata {
  instrumentId
  network
  tokenContract?
  ledgerRole
  transferability
  walletRequirements
  stablecoinSubscriptionSupported
  stablecoinRedemptionSupported
}
```

Tokenization is metadata, not a separate product universe.

---

# 13. Source Provenance

Every material field used in a financial comparison must be traceable.

```ts
Source {
  id
  publisher
  url
  sourceType
  retrievedAt
  effectiveDate?
  contentHash?
}

SourcedValue {
  entityType
  entityId
  field
  value
  sourceId
  effectiveFrom
  effectiveTo?
}
```

The system must be able to answer:

> Why did Ophir display this yield / tax rate / settlement time on this date?

---

# 14. Belgian Rules Engine

This is a deterministic policy engine.

AI may explain rule results but must not determine tax/accounting obligations from free-form reasoning at runtime.

## 14.1 Rule Inputs

```ts
RuleContext {
  jurisdiction
  legalEntityType
  accountingFramework
  instrumentId
  shareClassId?
  eventType
  eventDate
  amount
  currency
  provider
}
```

## 14.2 Event Types

Initial events:

- `SUBSCRIPTION`
- `REDEMPTION`
- `TRANSFER`
- `INCOME_DISTRIBUTION`
- `NAV_REVALUATION`
- `FEE`
- `FX_REVALUATION`
- `YEAR_END_HOLDING`

## 14.3 Rule

```ts
Rule {
  id
  jurisdiction
  domain // TAX | ACCOUNTING | REPORTING | ELIGIBILITY
  name
  version
  status
  effectiveFrom
  effectiveTo?
  sourceIds[]
  logic
  requiresProfessionalReview
}
```

Rules should preferably be stored as versioned code/config reviewed through pull requests, not as editable free-form database text.

## 14.4 RuleResult

```ts
RuleResult {
  ruleId
  ruleVersion
  status // APPLIES | DOES_NOT_APPLY | REVIEW_REQUIRED
  amount?
  rate?
  code?
  deadline?
  explanation
  evidence[]
}
```

If Ophir cannot determine a rule confidently, the correct result is `REVIEW_REQUIRED`, not a guess.

---

# 15. Tax Engine

The tax engine consumes rule results and produces a transparent calculation.

```ts
TaxCalculation {
  id
  legalEntityId
  eventId
  taxType
  taxableBase
  rate
  amount
  dueDate?
  declarationCode?
  status
  ruleVersion
}
```

Initial Belgian tax types to model only after formal validation may include:

- corporate income implications;
- transaction tax where applicable;
- withholding tax where applicable;
- securities-account tax where applicable.

The engine must support `NOT_APPLICABLE`, `CALCULATED`, and `PROFESSIONAL_REVIEW_REQUIRED`.

---

# 16. Accounting Rules Engine

The accounting engine maps economic events to proposed Belgian-GAAP entries.

```ts
AccountingRule {
  id
  eventType
  instrumentClassification
  legalEntityType
  debitAccountTemplate
  creditAccountTemplate
  valuationMethod
  effectiveFrom
  sourceIds[]
}
```

Outputs must be proposals until reviewed.

Every proposal should explain:

- event recognized;
- valuation basis;
- accounts used;
- amount;
- applicable rule/source;
- any unresolved question.

---

# 17. Compliance & Document Engine

The document engine converts structured facts into human-reviewable artifacts.

Initial artifacts:

- transaction summary;
- accountant pack;
- journal proposal;
- tax calculation worksheet;
- filing checklist;
- filing field/code guidance where validated;
- deadline reminder;
- supporting-document bundle;
- annual instrument statement.

## Document metadata

```ts
GeneratedDocument {
  id
  legalEntityId
  documentType
  eventId?
  period?
  generatedAt
  templateVersion
  ruleVersions[]
  sourceIds[]
  reviewStatus
  reviewedBy?
}
```

No document should claim to be officially filed unless Ophir has explicit future authority/integration to file it.

---

# 18. Provider Adapter Layer

Every external provider must implement a common internal contract.

## 18.1 BankDataProvider

```ts
interface BankDataProvider {
  createConsent(...): Promise<ConsentFlow>
  listAccounts(...): Promise<ExternalBankAccount[]>
  listBalances(...): Promise<ExternalBalance[]>
  listTransactions(...): Promise<ExternalBankTransaction[]>
  revokeConsent(...): Promise<void>
}
```

First candidate: Ponto.

## 18.2 AccountingProvider

```ts
interface AccountingProvider {
  connect(...): Promise<ConnectionFlow>
  listLedgerAccounts(...): Promise<ExternalLedgerAccount[]>
  listOpenPayables(...): Promise<ExternalOpenItem[]>
  listOpenReceivables(...): Promise<ExternalOpenItem[]>
  exportJournalProposal?(...): Promise<ExportResult>
}
```

First candidates: Exact Online and Odoo; Yuki/unified APIs can follow.

## 18.3 InstrumentProvider

```ts
interface InstrumentProvider {
  listInstruments(...): Promise<ExternalInstrument[]>
  getMarketData(...): Promise<ExternalMarketData>
  getLiquidityTerms(...): Promise<ExternalLiquidityTerms>
}
```

## 18.4 RegulatedExecutionProvider

The v1 interface must preserve explicit human execution.

```ts
interface RegulatedExecutionProvider {
  createInvestorOnboardingFlow(...): Promise<Handoff>
  createExecutionHandoff(...): Promise<Handoff>
  getPositions(...): Promise<ExternalPosition[]>
  getTransactions(...): Promise<ExternalInvestmentTransaction[]>
}
```

There is intentionally no generic `executeTrade()` method in the Ophir v1 backend contract.

First reference adapter: Spiko.

---

# 19. Handoff / Execution Boundary

## 19.1 Handoff object

```ts
Handoff {
  id
  legalEntityId
  provider
  type // ONBOARDING | SUBSCRIPTION | REDEMPTION
  instrumentId
  amount?
  currency?
  urlOrEmbeddedToken
  expiresAt
  status
}
```

## 19.2 Required user journey

1. Ophir presents objective data and consequences.
2. User chooses to continue.
3. Ophir generates provider handoff.
4. User enters provider-controlled execution context.
5. Provider obtains required confirmations and executes.
6. Provider returns or exposes transaction status.
7. Ophir retrieves the executed event.
8. Ophir reconciles and documents.

Audit records must distinguish `OPHIR_PREPARED`, `USER_HANDOFF_STARTED`, `PROVIDER_EXECUTED`, and `OPHIR_RECONCILED`.

---

# 20. Event Model

Use explicit domain events to create a durable audit chain.

Examples:

```text
BANK_CONNECTION_CREATED
BANK_ACCOUNT_SYNCED
BANK_TRANSACTION_IMPORTED
ACCOUNTING_CONNECTION_CREATED
OPEN_ITEM_IMPORTED
CASH_POSITION_CALCULATED
DEPLOYABLE_CASH_CALCULATED
INSTRUMENT_DATA_UPDATED
SCENARIO_CREATED
HANDOFF_CREATED
HANDOFF_OPENED
PROVIDER_TRANSACTION_DETECTED
TREASURY_LEDGER_POSTED
TAX_CALCULATION_CREATED
JOURNAL_PROPOSAL_CREATED
DOCUMENT_PACK_GENERATED
USER_REVIEW_COMPLETED
```

## Event schema

```ts
DomainEvent {
  id
  tenantId
  legalEntityId?
  eventType
  actorType // USER | SYSTEM | PROVIDER
  actorId?
  occurredAt
  correlationId
  payload
  payloadHash
}
```

Events are append-only.

---

# 21. Scenario Comparison Engine

Ophir should compare alternatives, not merely display them.

## Input

- deployable amount;
- expected holding period;
- required liquidity;
- instrument data;
- fees;
- tax model;
- operational costs;
- optional user-defined bank deposit offer.

## Output

```ts
TreasuryScenario {
  id
  legalEntityId
  amount
  horizonDays
  currency
  assumptions
  alternatives[]
}

ScenarioAlternative {
  instrumentId?
  label
  grossReturn
  fees
  estimatedTax
  estimatedAdminCost
  expectedNetBenefit
  liquidityProfile
  riskSummary
  unresolvedItems[]
}
```

Never collapse uncertainty into a false single-score precision.

---

# 22. Net Treasury Benefit

Working formula:

```text
Gross return
- product fees
- execution/on-off-ramp fees
- estimated tax cost
- estimated administration cost
+ quantified operational time savings
= Net Treasury Benefit
```

Risk and liquidity should be shown separately in v1 rather than hidden in an arbitrary monetary penalty.

The user should be able to inspect every term.

---

# 23. AI Architecture

AI is an assistant over deterministic systems.

## Permitted v1 uses

- explain a cash forecast;
- summarize instrument documents;
- explain a tax/accounting rule result using retrieved structured rules;
- generate a CFO-friendly scenario narrative;
- draft accountant notes;
- classify transaction descriptions with confidence and review;
- identify missing data;
- prepare support documentation.

## Prohibited v1 uses

- silently calculate statutory tax from model memory;
- invent filing codes;
- invent current yields;
- autonomously alter liquidity policy;
- autonomously execute an investment;
- override deterministic rule-engine results;
- present unsupported personalised investment advice.

## AI evidence contract

Any AI output involving finance, tax, accounting or regulation must include references to the structured facts/rules used.

If no reliable source exists, output must say that professional review is required.

---

# 24. Security Architecture

## Minimum requirements

- MFA for privileged users;
- strong tenant isolation;
- encryption in transit and at rest;
- secrets outside application code/database plaintext;
- least-privilege provider scopes;
- token rotation and revocation;
- no storage of customer banking credentials;
- no storage of blockchain private keys;
- immutable audit events;
- encrypted sensitive document storage;
- signed webhook validation;
- replay protection;
- idempotent provider ingestion;
- dependency and vulnerability scanning;
- production access logging;
- backup and restore testing.

## Data classification

At minimum:

- `PUBLIC`
- `INTERNAL`
- `CONFIDENTIAL`
- `FINANCIAL_SENSITIVE`
- `AUTH_SECRET`

Provider access tokens and authentication material are `AUTH_SECRET` and require dedicated secret storage.

---

# 25. Data Residency & Privacy

Working v1 assumption: keep primary application data and backups in the EEA where practical.

GDPR requirements include:

- explicit processing purposes;
- data minimisation;
- retention policy;
- user/tenant deletion workflow where legally possible;
- subprocessor register;
- data-processing agreements;
- access/export process;
- documented lawful bases.

Audit records required for legal/security reasons may require separate retention handling.

---

# 26. Provider Webhooks and Synchronisation

All external integrations must support eventual consistency.

General flow:

```text
Webhook received
→ verify signature
→ store raw event metadata/hash
→ idempotency check
→ enqueue sync
→ fetch authoritative provider object
→ normalize
→ reconcile
→ emit domain event
```

Do not trust webhook payloads as the sole authoritative financial record if the provider offers a retrieval API.

---

# 27. Reconciliation

Reconciliation is a first-class feature.

For each provider transaction:

1. identify source provider event;
2. match related bank movement where applicable;
3. match investment transaction/position;
4. post internal treasury ledger event;
5. calculate fees/tax/accounting consequences;
6. flag unmatched or inconsistent amounts;
7. require review when confidence is below threshold.

```ts
ReconciliationCase {
  id
  legalEntityId
  status
  sourceObjects[]
  matchedObjects[]
  differenceAmount
  confidence
  reviewRequired
}
```

---

# 28. Audit Trail

Every consequential calculation must capture:

- user/system actor;
- time;
- source data version;
- policy version;
- rules version;
- calculation inputs;
- calculation output;
- review decision;
- provider outcome.

The audit view should allow reconstruction of what Ophir knew when a user made a decision.

---

# 29. MVP Screens

## 29.1 Overview

- total cash;
- cash by bank/entity;
- upcoming obligations;
- liquidity buffer;
- deployable cash;
- unresolved data issues.

## 29.2 Cash Forecast

- 7 / 30 / 60 / 90 day views;
- known vs estimated flows;
- confidence;
- editable manual events;
- policy threshold.

## 29.3 Opportunities / Alternatives

Avoid sales-oriented language.

Show:

- eligible supported alternatives;
- current yield metric;
- fees;
- expected net benefit;
- settlement/liquidity;
- risks;
- Belgian tax/accounting status;
- unresolved professional-review items;
- `Continue with provider` action.

## 29.4 Instrument Detail

- legal structure;
- ISIN;
- provider;
- domicile;
- underlying portfolio;
- risk;
- yield history;
- fees;
- liquidity;
- tax/accounting treatment;
- source documents;
- source freshness.

## 29.5 Transaction / Handoff

- amount;
- entity;
- source account;
- selected instrument;
- consequences summary;
- explicit statement that execution occurs with provider;
- handoff button.

## 29.6 Compliance Inbox

- pending review;
- journal proposals;
- tax calculations;
- upcoming filing deadlines;
- missing documents;
- accountant review status.

## 29.7 Audit

Chronological event and decision history.

---

# 30. API Surface — Ophir Internal/Frontend

Initial conceptual endpoints:

```text
GET  /entities
GET  /entities/:id/cash-position
GET  /entities/:id/forecast
GET  /entities/:id/deployable-cash
GET  /entities/:id/instruments
POST /entities/:id/scenarios
GET  /scenarios/:id
POST /scenarios/:id/handoffs
GET  /entities/:id/positions
GET  /entities/:id/reconciliations
GET  /entities/:id/compliance
GET  /events/:id/documents
POST /journal-proposals/:id/review
```

Provider callbacks live under isolated integration endpoints.

---

# 31. Background Jobs

Initial jobs:

- bank sync;
- accounting sync;
- instrument market-data refresh;
- source freshness check;
- provider transaction sync;
- reconciliation;
- forecast recalculation;
- rule recalculation after rule-version change;
- compliance deadline generation;
- document generation.

Every job must be idempotent where practical.

---

# 32. Rule Change Impact Analysis

This is an important future moat and should influence the data model from day one.

When a rule changes:

```text
new RuleVersion
→ identify affected instruments
→ identify affected entities/events/periods
→ create review tasks
→ regenerate impacted draft calculations/documents
→ never silently rewrite already-filed historical outputs
```

Ophir should eventually answer:

> Which clients and transactions are affected by this Belgian tax/accounting change?

---

# 33. Source Freshness

Each data category has a freshness policy.

Examples:

- bank balances: hours/minutes;
- fund NAV/yield: daily;
- instrument legal metadata: event-driven + periodic review;
- tax/accounting rules: versioned and manually approved;
- provider fees: periodic/API refresh;
- liquidity terms: periodic review.

Stale data must be visibly marked and should block calculations when material.

---

# 34. Failure Modes

The product must fail safely.

Examples:

- bank consent expired → show stale state, do not imply live cash position;
- accounting sync failed → flag forecast incompleteness;
- yield feed unavailable → suppress comparison rather than reuse unknown stale data;
- tax rule ambiguous → professional review required;
- provider transaction mismatch → reconciliation case;
- document generation failure → no filing-ready status;
- source changed materially → invalidate affected result.

---

# 35. Human Review Model

Review states:

```text
NOT_REVIEWED
SYSTEM_VALIDATED
USER_REVIEWED
ACCOUNTANT_REVIEWED
LEGAL_REVIEWED
PROFESSIONAL_REVIEW_REQUIRED
```

Not every artifact requires every level, but Ophir must make the review status explicit.

---

# 36. MVP Integration Order

Recommended implementation sequence:

### Sprint A — Foundation

- tenant/legal-entity/user model;
- authentication/RBAC;
- PostgreSQL schema;
- audit/event log;
- source provenance framework.

### Sprint B — Banking

- Ponto sandbox adapter;
- accounts/balances/transactions;
- normalized cash ledger;
- dashboard.

### Sprint C — Accounting

- one provider only, preferably Exact Online or Odoo based on first design partner;
- AP/AR ingestion;
- basic chart mapping;
- forecast inputs.

### Sprint D — Treasury Engine

- liquidity policy;
- deterministic forecast;
- deployable cash;
- scenario engine.

### Sprint E — Instrument Intelligence

- Spiko public data adapter;
- instrument/share-class model;
- NAV/yield/fees/liquidity;
- source provenance.

### Sprint F — Belgian Rules Prototype

- one instrument;
- one Belgian legal-entity type;
- subscription and redemption only;
- accounting proposal;
- tax/compliance checklist;
- rules versioning.

### Sprint G — Regulated Handoff

- Spiko sandbox onboarding/handoff;
- external execution boundary;
- transaction retrieval;
- reconciliation.

### Sprint H — Compliance Pack

- journal proposal;
- tax worksheet;
- supporting evidence;
- review workflow;
- PDF/export only after source/rule validation.

---

# 37. Acceptance Test — Golden Path

Given:

- Belgian company A;
- KBC + BNP bank accounts connected;
- accounting system connected;
- €1,200,000 available cash;
- €600,000 forecast obligations/buffer;
- one supported regulated EUR MMF;

Ophir must be able to:

1. show the €1.2m source cash with provenance;
2. explain the €600k liquidity requirement;
3. derive €600k deployable cash;
4. show a supported instrument with current sourced yield/fees/liquidity;
5. calculate a transparent scenario for a chosen amount/horizon;
6. flag any tax/accounting uncertainty;
7. create a provider handoff without Ophir executing the transaction;
8. detect the completed external transaction;
9. reconcile the cash movement and fund position;
10. create a balanced internal ledger event;
11. generate a journal proposal;
12. generate a tax/compliance worksheet;
13. preserve an audit trail tying all results to the exact data/rule/source versions used.

If this golden path works, Ophir has demonstrated the core product thesis.

---

# 38. Technical Kill Criteria

Pause or redesign if:

- bank/accounting connectivity requires excessive per-customer manual work;
- provider APIs cannot reliably expose post-trade data;
- reconciliation requires persistent human intervention;
- tax/accounting rules cannot be represented deterministically enough for useful automation;
- source provenance cannot be maintained reliably;
- regulated provider handoff produces a broken user experience;
- the security burden fundamentally conflicts with the intended small-team operating model.

---

# 39. Open Technical Questions

1. Ponto pricing/consent model for Ophir's exact multi-tenant use case.
2. Exact Online vs Odoo as first accounting adapter.
3. Whether a unified accounting API creates more value than direct first-party connectors.
4. Spiko embedded/distributor API exact sandbox capabilities for a Belgian corporate investor.
5. Webhook coverage and post-trade retrieval guarantees from investment providers.
6. Exact Belgian accounting representation of the first reference instrument.
7. Exact Belgian tax/document-generation boundary.
8. Whether source documents need cryptographic snapshots for later audit defensibility.
9. Whether a rules DSL is worthwhile or versioned TypeScript rules are simpler for v1.
10. Which artifact formats accountants actually want: CSV, CODA-like exports, PDF, API, UBL-linked evidence, or direct journal export.

---

# 40. Immediate Next Step

Do **not** start by building every module.

The next work item is to convert this specification into two smaller artifacts:

1. `docs/DOMAIN_MODEL_V1.md` — exact entities, relations and lifecycle states;
2. `docs/GOLDEN_PATH_SEQUENCE.md` — API-by-API sequence for one Belgian company investing surplus EUR into one supported regulated fund and later redeeming it.

Those two artifacts will make the subsequent regulatory review much more precise because counsel can review concrete data flows and user actions rather than abstract product language.
