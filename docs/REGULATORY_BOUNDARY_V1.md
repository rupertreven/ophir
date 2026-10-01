# Ophir Regulatory Boundary v1

> **Status:** Research draft — requires Belgian/EU fintech counsel validation before production.  
> **Scope:** B2B Belgian corporate treasury golden path defined in `GOLDEN_PATH_SEQUENCE.md`.  
> **Design principle:** **Ophir prepares. The company decides. The regulated provider executes. Ophir observes, reconciles and documents.**

This document is a product-boundary map, not legal advice. Its purpose is to make the software architecture reviewable by counsel and to prevent regulated functionality from appearing accidentally through UX wording, API design or AI behaviour.

---

## 1. Classification

### GREEN — target v1 perimeter
Functionality that appears capable of being structured primarily as software, factual data processing, internal corporate workflow or administrative tooling, subject to normal contractual/privacy/security obligations.

### AMBER — partner/counsel controlled
Functionality that may be feasible but is sensitive to implementation details, wording, commercial arrangements, user-specific context or Belgian professional-services rules. It requires explicit legal validation and often a licensed/registered partner boundary.

### RED — excluded from Ophir v1
Functionality that would move Ophir materially toward regulated payment/investment/crypto execution, custody, discretionary management or another activity we do not intend to license for initially.

A classification is attached to the **actual behaviour**, not the feature name. A Green dashboard can become Amber/Red if an AI layer turns factual data into a personalised investment recommendation or initiates a regulated transaction.

---

## 2. Regulatory architecture

```text
                         OPHIR
        software / data / control / documentation
                           │
          ┌────────────────┼─────────────────┐
          │                │                 │
          ▼                ▼                 ▼
  Open-banking       Accounting       Investment/fund
     partner            system            provider
          │                                  │
          ▼                                  ▼
       Banks                         regulated execution
                                             │
                                             ▼
                                    fund / financial asset
```

### Core invariants

1. Ophir does not hold customer money.
2. Ophir does not hold customer private keys or custody financial assets.
3. Ophir does not execute investment orders in v1.
4. Ophir does not autonomously transmit an investment order in v1 unless later specifically validated under a licensed-partner model.
5. The authorised company user gives final regulated-provider confirmation.
6. Customer money/assets move directly through regulated/provider rails, never through an Ophir omnibus account.
7. Ophir records an internal `transaction_intent`, not a financial order.
8. AI cannot bypass the human/provider execution boundary.
9. Tax/accounting outputs are deterministic, versioned and reviewable; uncertain outputs are marked `NEEDS_REVIEW`.
10. Product wording must distinguish facts/calculations from recommendations/advice.

---

## 3. Golden-path boundary matrix

| Golden-path activity | v1 | Primary concern | Required boundary/control |
|---|---|---|---|
| Create company/legal-entity profile | GREEN | GDPR/company data | lawful basis, minimisation, retention/security |
| Connect bank through licensed open-banking provider | GREEN/AMBER | PSD2/AISP | provider owns regulated account-information consent; Ophir uses partner contract/API |
| Directly become account-information provider | RED initially | PSD2/AISP authorisation | use licensed provider instead |
| Import balances/transactions | GREEN/AMBER | PSD2 + GDPR | consent scope, provider terms, data security |
| Connect ERP/accounting system | GREEN | GDPR/confidential financial data | OAuth/authority, security, contractual permissions |
| Normalize bank/accounting data | GREEN | software/data processing | lineage and correctness controls |
| Calculate cash position | GREEN | software | deterministic, source-linked calculation |
| Forecast cash | GREEN | software | explain assumptions; no guarantee |
| Apply internal liquidity policy | GREEN | internal corporate workflow | customer-defined/approved policy |
| Calculate deployable cash | GREEN | software/internal decision support | factual calculation; avoid automatic investment instruction |
| Retrieve NAV/yield/fees/liquidity facts | GREEN | financial promotion/data accuracy | source/as-of/provenance; no guarantee |
| Display several products neutrally | GREEN/AMBER | MiFID distribution/promotion | counsel-review presentation/ranking/compensation model |
| Rank products for a specific company | AMBER | personalised investment recommendation | do not ship until advice perimeter reviewed |
| Say “we recommend you buy X” | RED initially | MiFID investment advice | excluded without appropriate licence/partner model |
| Calculate gross return scenario | GREEN | financial calculation | factual assumptions + sensitivity |
| Calculate estimated after-tax return | AMBER | tax-profession/liability perimeter | validated rules, assumptions, review/disclaimer and professional-role analysis |
| Determine product eligibility | AMBER | distribution/suitability/appropriateness | licensed provider should own regulated investor eligibility where required |
| Facilitate provider onboarding | AMBER | distribution/KYB/AML allocation | formal introducer/distributor agreement; provider owns regulated checks |
| Internal company approval workflow | GREEN | corporate governance | clear that approval is internal, not market order |
| Create `transaction_intent` | GREEN/AMBER | order-transmission characterization | not executable order; no provider submission until user enters regulated flow |
| Create provider session/deep link | AMBER | distribution/order boundary | licensed-provider contract and counsel-approved UX |
| Embedded provider-owned execution UI | AMBER | responsibility clarity | provider identity/disclosures/final confirmation must remain clear |
| User confirms transaction at provider | GREEN for Ophir boundary | provider regulated activity | authoritative provider-side confirmation |
| Ophir backend executes order | RED | execution/reception-transmission | no `executeTrade()` in v1 |
| Ophir automatically redeems based on forecast | RED | discretionary management/execution | user/provider confirmation required |
| Ophir holds cash before investment | RED | payment/custody/safeguarding | money never enters Ophir account |
| Ophir holds fund units/keys | RED | custody | provider/custodian/investor owns/controls |
| Retrieve provider transaction/position data | GREEN/AMBER | consent/provider terms | read-only, authorised scope |
| Reconcile external transaction | GREEN | software/accounting | evidence and deterministic matching |
| Propose journal entry | AMBER | Belgian accounting-profession perimeter | customer/accountant review; do not claim regulated accountant role |
| Export approved journal data | GREEN/AMBER | authority/accounting integrity | explicit authority, audit trail, rollback/correction controls |
| Auto-post journal without review | AMBER | accounting responsibility/control | only after professional/legal validation and customer policy |
| Calculate possible tax obligation | AMBER | Belgian tax-profession/liability perimeter | deterministic validated rules + review status |
| Prepare filing instructions/field codes | AMBER | tax-profession boundary + correctness | source/effective date, review, explicit responsibility |
| File tax declaration as customer representative | RED initially | mandate/professional/filing obligations | excluded pending dedicated legal model |
| Generate evidence/accountant pack | GREEN | administrative software | provenance, integrity, retention |
| AI explains source-backed rule | GREEN/AMBER | hallucination/liability | cite exact rule/source; no unsupported output |
| AI changes tax/accounting rule | RED operationally | control failure | human-reviewed rule publication only |
| AI autonomously chooses/invests/redeems | RED | advice/discretionary management/execution | prohibited in v1 |

---

## 4. Banking / PSD boundary

### Target architecture

Ophir should not initially become an AISP/PISP. Bank account access should be mediated by an appropriately licensed open-banking provider such as Ponto/Isabel or another validated partner.

### GREEN target

Ophir:
- initiates the customer's connection journey to the licensed provider;
- stores provider connection metadata and secret references securely;
- consumes authorised account/balance/transaction data;
- normalizes and analyses the data;
- exposes consent status/freshness to the customer.

### AMBER questions for counsel/provider

1. Is Ophir technically acting as agent/technical service provider/outsourcing party of the regulated provider?
2. Which party contracts with the SME for account-information services?
3. Who presents PSD consent language?
4. Who handles SCA/bank authentication?
5. What raw payment-account data may Ophir retain and for how long?
6. What happens when consent expires/revokes?
7. May Ophir later expose payment initiation while remaining behind the provider's regulated boundary?

### RED initially

- scraping bank portals using customer credentials;
- storing customer bank authentication credentials;
- independently providing regulated AISP/PISP services without the required authorisation/registration model;
- initiating payments invisibly/autonomously.

---

## 5. Investment / MiFID boundary

Tokenized funds/securities that qualify as financial instruments are not made non-MiFID merely because they use a blockchain. The legal classification of the underlying/share class matters.

### Product-information mode

The safest v1 product starts from **factual comparison**:

- current yield/NAV facts;
- fees;
- settlement rules;
- liquidity;
- minimum ticket;
- legal/product classification;
- tax/accounting consequences;
- customer-entered horizon/amount;
- deterministic scenario calculations.

### Advice-risk triggers — AMBER/RED

Counsel must review whether the following create a personal recommendation or distribution obligation:

- “best for your company”;
- defaulting one product as recommended;
- ranking based on customer-specific balance/horizon/risk data;
- AI saying the company “should” invest;
- push alerts instructing the CFO to buy/redeem;
- compensation that varies by product/provider;
- filtering products based on investor-specific suitability characteristics.

### v1 wording principle

Prefer:

> “At the assumptions shown, Instrument A produces an estimated net outcome of X; Instrument B produces Y. Review the underlying risks and provider documentation before deciding.”

Avoid:

> “Ophir recommends investing €500,000 in Instrument A.”

### Provider boundary

Where Spiko or another investment firm distributes under its own licence, provider documentation/contract must establish:

- which regulated services the provider performs;
- Ophir's role (e.g. business introducer/technology/distribution interface as legally agreed);
- who performs investor classification/eligibility;
- who gives mandatory product disclosures;
- who receives the investor's legally operative instruction;
- who executes/subscribes/redeems;
- complaints handling;
- record retention;
- remuneration disclosures/conflicts where applicable.

---

## 6. Transaction intent vs order

This distinction is architecturally critical.

### `transaction_intent`

An Ophir record represents an internal corporate decision-preparation object containing:

- candidate instrument;
- amount;
- scenario snapshot;
- internal approvals;
- factual provider information;
- handoff status.

It must not contain credentials or semantics that allow Ophir to turn it into a binding provider order without a new user action inside the regulated-provider boundary.

### State machine

```text
DRAFT
  -> AWAITING_INTERNAL_APPROVAL
  -> APPROVED_FOR_HANDOFF
  -> HANDED_OFF
  -> COMPLETED_EXTERNALLY
```

The jump `APPROVED_FOR_HANDOFF -> COMPLETED_EXTERNALLY` cannot be caused by an Ophir execution command. Completion is derived from authoritative provider evidence.

### Counsel question

Even preparation/transmission can become regulated depending on the precise provider integration. Therefore deep-link/session creation remains AMBER until counsel reviews the actual API and commercial agreement.

---

## 7. Stablecoins / MiCA boundary

Stablecoins may appear as settlement rails even where the investment itself is a MiFID financial instrument.

### GREEN/AMBER target

Ophir may display and reconcile authorised stablecoin balances/transactions and explain factual settlement options, subject to data/custody/provider design.

### RED initially

Ophir does not:

- custody client crypto-assets/private keys;
- exchange EUR for stablecoins itself;
- execute crypto transfers on behalf of customers as a crypto-asset service;
- operate an exchange;
- provide autonomous crypto portfolio management/advice.

Where EURC or another regulated stablecoin is used, mint/redeem/custody/transfer execution should remain with appropriately regulated providers/customer-controlled infrastructure.

### Important classification rule

Do not use “onchain” as a regulatory category. The Rules/Instrument model must distinguish at least:

- e-money token / other MiCA crypto-asset where applicable;
- tokenized financial instrument excluded from MiCA because it is a MiFID financial instrument;
- traditional financial instrument represented/settled through DLT infrastructure;
- bank deposit/tokenized deposit where relevant.

---

## 8. Tax engine boundary

The commercial opportunity is large precisely because Belgian tax treatment can be operationally painful. That also creates professional-liability risk.

### Target behaviour

The engine can deterministically evaluate reviewed rules against structured facts:

```text
legal entity
+ instrument classification
+ transaction type
+ amount
+ date
+ holding/account facts
= tax evaluation
```

Output must include:

- result;
- calculation;
- required missing facts;
- effective rule version;
- legal/administrative source;
- validation status;
- reviewer/professional-review requirement.

### Rule confidence

Use statuses such as:

- `VALIDATED_INTERNAL_RESEARCH`
- `VALIDATED_COUNSEL`
- `VALIDATED_TAX_PROFESSIONAL`
- `NEEDS_REVIEW`
- `SUPERSEDED`

Production filing-grade outputs should require an agreed validation level.

### AMBER questions

Belgian counsel/tax professional must determine:

1. When does automated tax calculation become regulated tax advice/professional practice?
2. May Ophir prepare a complete draft return without being the filing representative?
3. Which disclaimers/review controls are legally meaningful rather than cosmetic?
4. Can an external accountant/tax adviser approve rules centrally for many customers?
5. Who bears liability for a wrong instrument classification or outdated rule?
6. Which tax forms may be generated versus filed?

### v1 safest path

**Prepare, explain, calculate and package; customer/accountant reviews and files.**

Do not represent that Ophir is the customer's tax adviser unless/until the professional model is validated.

---

## 9. Accounting engine boundary

### Target behaviour

Ophir maps an externally confirmed economic event to a proposed Belgian accounting treatment and journal entry.

The proposal must show:

- event/source evidence;
- instrument classification;
- proposed ledger accounts;
- debit/credit;
- valuation basis;
- applied rule version;
- review state.

### v1 workflow

```text
External transaction confirmed
        -> Ophir journal proposal
        -> CFO/accountant review
        -> approved export/API push
        -> accounting-system confirmation
```

### AMBER questions

- Does proposing entries constitute reserved accounting activity in the exact Belgian commercial model?
- Can Ophir sell directly to the company while its external accountant validates mappings/rules?
- What changes if Ophir automatically posts versus merely exports?
- What professional responsibility arises from year-end valuation/classification logic?

### Architectural response

Separate:

1. **calculation engine**;
2. **professional validation status**;
3. **customer approval**;
4. **accounting-system write**.

Never make AI-generated free text the authoritative journal logic.

---

## 10. Document and filing boundary

Ophir's strongest administrative value proposition can remain compatible with a conservative boundary if the system produces **filing-ready drafts** rather than silently acting as legal representative.

### Example output

```text
Obligation: [validated Belgian tax/reporting obligation]
Period: Q3 2026
Instrument: ...
ISIN: ...
Transaction: ...
Taxable base: ...
Rate: ...
Calculated amount: ...
Form/declaration: ...
Field/code: ...
Due date: ...
Payment instructions: ...
Rule version: ...
Source: ...
Review status: TAX PROFESSIONAL VALIDATED / NEEDS REVIEW
```

### GREEN target

- evidence packs;
- transaction schedules;
- accountant exports;
- audit timelines;
- source-backed calculation worksheets.

### AMBER

- exact tax form population;
- exact field/code instructions;
- generated filing file formats;
- automatic accounting writes.

### RED initially

- filing as authorised tax representative;
- signing/submitting declarations in the customer's name without a separately validated mandate/professional model.

---

## 11. AI boundary

AI is useful for explanation and interface, not authority.

### Allowed target uses

- explain why deployable cash changed;
- summarize instrument/provider documents;
- explain a deterministic rule evaluation using cited source/rule version;
- draft accountant notes;
- identify missing information;
- surface anomalies for human review.

### Prohibited v1 uses

- invent tax/accounting rules;
- change a production rule without human review;
- decide that a company should buy/sell a financial instrument;
- confirm an order;
- sign/file a declaration;
- override customer approval policy;
- fabricate a source when none exists.

### Technical enforcement

The AI layer receives read-only tools for authoritative financial/rule data by default. Any future write tool must be separately permissioned and cannot cross the regulated execution boundary.

---

## 12. Remuneration and conflicts

A material open legal/business question