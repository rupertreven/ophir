# Ophir Regulatory Perimeter — Belgium & EU

> **Status:** Research memo v0.1 — 28 August 2026
>
> **Important:** This is product/regulatory research, not formal legal advice. Before launch, Ophir should have the proposed MVP and customer journey reviewed by Belgian/EU fintech counsel and, where useful, discuss the perimeter with the FSMA/NBB.

## Executive conclusion

**A Belgian Ophir MVP appears feasible without Ophir itself becoming a CASP, payment institution or investment firm — if the initial product is deliberately designed as a read-only software/data/control layer and regulated actions remain with licensed third parties.**

That conclusion is architectural, not semantic. Calling Ophir “software” does not exempt it if the actual service crosses into regulated activity.

The safest initial model is:

> **Observe → Understand → Prepare → Human approval → Licensed provider executes**

Ophir should initially avoid custody, control of private keys, receiving/transmitting or executing crypto orders, transfers of crypto on behalf of clients, personalised investment recommendations, discretionary portfolio management, payment initiation, and execution/advice in tokenised financial instruments.

This creates a credible path to market while preserving a later choice: partner with regulated institutions, become an agent/technical provider where legally available, or seek licences only after product-market fit justifies the cost.

---

## 1. Regulatory map

Ophir potentially touches several regulatory regimes because “tokenised finance” is not one legal category.

### MiCA

MiCA regulates specified crypto-asset services. The Belgian FSMA lists custody/administration, operation of a crypto trading platform, exchange, execution of orders, placing, reception/transmission of orders, crypto advice, portfolio management and crypto transfer services as regulated crypto-asset services.

Belgium implemented MiCA through the Law of 11 December 2025. The Belgian transitional period ended on 30 June 2026; from 1 July 2026 providers of regulated crypto-asset services need the appropriate CASP status. As of 24 August 2026, the FSMA's own list of Belgian Article 63 CASPs showed none.

### MiFID II / securities framework

MiCA expressly excludes crypto-assets that qualify as financial instruments. Tokenisation does not remove a security or fund interest from existing financial-services law. ESMA has issued guidelines on the conditions and criteria for determining when crypto-assets qualify as financial instruments.

This matters enormously for Ophir: a tokenised bond, share or fund unit may fall under MiFID/UCITS/AIF and related securities rules rather than MiCA. “It is onchain” is not a regulatory category.

### Payments / PSD2 and successor framework

Bank aggregation and payment initiation are separately regulated. The NBB explains that an Account Information Service Provider (AISP) accessing payment accounts to provide consolidated payment information requires customer authorisation and an appropriate licence; Payment Initiation Service Providers (PISPs) initiate transfers on behalf of users.

Therefore Ophir should not assume that direct bank API connectivity is unregulated merely because the product is read-only. The practical MVP route is likely to consume bank data through an appropriately licensed open-banking provider rather than becoming an AISP itself.

### AML/KYC

If Ophir stays outside regulated financial activity, it should not assume it automatically becomes an AML obliged entity merely because customers can view crypto balances. However, regulated partners will have AML/KYC obligations and will impose onboarding, sanctions, transaction-monitoring and data requirements on the integration.

### DORA, GDPR and enterprise security

Even where Ophir is not itself a regulated financial entity, regulated customers/partners may treat Ophir as an ICT third-party provider and impose DORA-aligned contractual, resilience, incident-management and vendor-risk requirements. GDPR applies wherever Ophir processes personal data.

For product strategy, the important lesson is broader: **being outside the licensing perimeter does not mean being outside enterprise compliance expectations.**

---

## 2. Proposed MVP perimeter

### GREEN — target for v1

These features are the preferred initial surface, subject to implementation details and counsel review:

- Treasury dashboard using data supplied by the customer or licensed data providers.
- Read-only display of bank balances.
- Read-only display of public blockchain wallet balances where Ophir does not control keys.
- Normalisation of transaction data into an internal treasury ledger.
- Historical cash-position reporting.
- Cash-flow forecasting.
- Reconciliation assistance.
- Accounting/ERP exports.
- Generic analytics and scenario modelling.
- Alerts based on customer-defined thresholds.
- Audit logs and role-based access.
- AI explanations of the customer's own treasury data.
- Generic educational information about asset classes and treasury concepts.
- Preparation of a proposed workflow that requires a human to approve and execute through a regulated provider.

**Design principle:** Ophir observes and organises information; it does not take possession of assets or make regulated decisions for the customer.

### AMBER — partner/legal review before launch

- Direct open-banking account aggregation.
- Initiating bank payments from Ophir.
- Embedded buy/sell flows routed to a CASP.
- Embedded stablecoin conversion.
- Creating transaction payloads for customer signature.
- Smart-contract interaction initiated from the Ophir UI.
- Automated stablecoin transfers even when keys remain with the customer.
- Product ranking based on yield, risk or suitability.
- Treasury optimisation that recommends a specific crypto-asset or financial instrument.
- Yield routing.
- Embedded tokenised money-market funds.
- Embedded tokenised bonds.
- Fee/revenue-sharing arrangements with regulated providers.
- AI that moves from descriptive analysis to personalised recommendations.

These are not necessarily impossible. They are where legal classification becomes fact-specific and partner structure matters.

### RED — deliberately exclude from initial product

- Ophir holding customer fiat or crypto.
- Ophir controlling customer private keys or signing authority.
- Custody/administration of crypto-assets on behalf of clients.
- Ophir exchanging crypto against funds or other crypto as principal.
- Executing crypto orders for customers.
- Receiving and transmitting customer crypto orders as Ophir's regulated service.
- Transferring crypto-assets on behalf of clients where this constitutes the MiCA transfer service.
- Personalised crypto investment advice.
- Discretionary crypto portfolio management.
- Discretionary investment management of tokenised securities/funds.
- Unlicensed investment services relating to tokenised financial instruments.

---

## 3. The crucial distinction: stablecoins vs tokenised securities

Ophir must maintain an asset-classification layer.

A euro/dollar stablecoin may be regulated under MiCA, including the specific rules for e-money tokens or asset-referenced tokens depending on structure.

A tokenised bond, equity or fund interest can instead be a **financial instrument**, putting it outside MiCA's scope and inside existing securities regulation.

This means the product architecture should never use a simplistic `is_token = true` regulatory rule. Every supported asset needs metadata such as:

- legal issuer;
- jurisdiction;
- asset classification;
- MiCA category if applicable;
- financial-instrument status;
- distribution restrictions;
- eligible customer types;
- executing/custody provider;
- permitted actions by jurisdiction.

This classification becomes part of Ophir's long-term compliance moat.

---

## 4. Recommended operating model

### Ophir

Provides:

- software;
- unified data model;
- dashboards;
- forecasting;
- reconciliation;
- workflow orchestration;
- policy representation;
- auditability;
- AI-assisted analysis.

### Licensed partners

Provide regulated capabilities where required:

- bank account information/open banking;
- payment initiation;
- custody;
- fiat/stablecoin conversion;
- crypto execution and transfer;
- securities brokerage/execution;
- fund distribution;
- regulated advice where applicable.

### Customer

Retains:

- ownership of accounts and assets;
- signing authority;
- investment decisions;
- treasury policy;
- human approval during the initial phases.

This separation should exist in contracts **and in technical architecture**.

---

## 5. AI Treasury Agent: safe evolution

The long-term autonomous-agent vision should be introduced progressively.

### Level 0 — Explain

“Why did our EUR liquidity fall €180k this week?”

Low regulatory risk relative to action-taking.

### Level 1 — Forecast

“We are likely to fall below our €500k minimum cash buffer in 17 days.”

Still principally analytics.

### Level 2 — Propose

“Based on the policy you configured, €200k appears to be surplus liquidity. Here are the permitted actions.”

Requires careful separation between policy-driven workflow assistance and regulated personalised investment advice.

### Level 3 — Prepare

Ophir prepares an instruction, but an authorised human approves/signs and a licensed provider executes.

Target architecture for early commercial product.

### Level 4 — Execute within policy

Agent executes approved classes of transaction under delegated authority.

This is strategically attractive but should be treated as a later regulated-perimeter project, not as MVP scope.

---

## 6. Product architecture consequences

Regulation should shape the codebase from day one.

### Never store customer signing secrets in the core SaaS

The core application should not possess private keys or equivalent bank signing credentials.

### Separate read and action permissions

`READ_BALANCE` must be technically distinct from `PREPARE_TRANSACTION`, `REQUEST_SIGNATURE`, `INITIATE_PAYMENT`, `EXECUTE_ORDER` and `TRANSFER_ASSET`.

### Provider abstraction

All regulated execution should sit behind provider adapters so Ophir can change licensed partners without rewriting the treasury core.

### Immutable decision trail

For every AI-assisted workflow record:

- source data;
- policy evaluated;
- model/tool version;
- proposed action;
- human approver;
- executing provider;
- timestamps;
- final result.

### Kill switch

Action-capable integrations should have global, tenant and user-level disable controls.

---

## 7. Regulatory strategy for a one-founder, AI-native company

Ophir should use regulation as a constraint on scope, not try to outspend regulated incumbents.

### Stage A — unregulated/read-only SaaS

Goal: prove that CFOs will pay for unified treasury visibility and workflows.

No custody. No execution. No personalised investment advice. Use licensed bank-data infrastructure where required.

### Stage B — regulated-partner orchestration

Embed capabilities from licensed European providers. Ophir remains the control plane while partners remain the regulated execution/custody layer.

### Stage C — decide whether licensing creates strategic value

Only after meaningful ARR and clear customer demand should Ophir evaluate becoming directly regulated.

A licence is not a badge. It is an operating model with governance, capital, compliance, reporting, security and supervisory obligations. The one-man-unicorn thesis argues for postponing that burden unless direct licensing becomes a genuine moat.

---

## 8. Questions for Belgian fintech counsel

Before MVP launch obtain written advice on these concrete flows:

1. Can Ophir aggregate bank data solely through a licensed AISP while remaining a technical service provider?
2. Can Ophir display customer-specified public wallet addresses without CASP status?
3. At what point does constructing an unsigned crypto transaction become a MiCA transfer/execution service?
4. Can Ophir provide policy-based treasury suggestions without constituting personalised crypto advice or MiFID investment advice?
5. What UI language separates analytics from regulated recommendations?
6. Can a licensed CASP expose execution inside an Ophir-branded interface, and what outsourcing/agent/distribution rules apply?
7. What is the legal treatment of each target stablecoin used by Belgian corporate customers?
8. How may tokenised UCITS/MMFs/bonds be displayed, compared, distributed and transacted by corporate users?
9. Which AML obligations attach directly to Ophir under each proposed partner model?
10. Which DORA obligations arise contractually or directly as Ophir serves regulated partners/customers?
11. What professional-liability/cyber insurance is advisable before connecting production financial data?
12. Should Ophir seek an informal/pre-application discussion with FSMA and/or NBB before introducing action capabilities?

Counsel should review **screens and sequence diagrams**, not only a written product description.

---

## 9. Current Belgian signal

Belgium is simultaneously attractive and conservative as a launch market.

The regulatory responsibilities are now clearly allocated between FSMA and NBB under the Belgian implementation of MiCA. The transitional CASP regime has ended. At the same time, the FSMA's Belgian Article 63 CASP list showed no authorised Belgian providers as of 24 August 2026, while European providers can operate cross-border under the applicable EU frameworks.

Strategically, this reinforces the partner-first thesis: **Ophir does not need to manufacture every regulated rail in Belgium. It needs to make the best European rails usable by Belgian companies.**

---

## 10. Decision

### GO — with a deliberately narrow perimeter

The regulatory environment does **not** invalidate Ophir.

It changes what the first product should be.

The initial company should be a **treasury intelligence and control software company**, not a crypto custodian, broker, asset manager or payment institution.

That is arguably better for the business:

- lower capital requirements;
- lower compliance headcount;
- lower security blast radius;
- faster product iteration;
- partner optionality;
- easier one-founder economics;
- the customer relationship and data/control layer remain with Ophir.

The long-term opportunity is still autonomous treasury. The shortest credible route to it is **not** to begin with autonomy.

---

## Primary sources

- FSMA — Crypto-Asset Service Provider (CASP): https://www.fsma.be/en/crypto-asset-service-provider-casp
- FSMA — End of CASP transitional period, 25 June 2026: https://www.fsma.be/fr/news/prestataires-de-services-sur-crypto-actifs-fin-de-la-periode-transitoire
- FSMA — Authorised Belgian CASPs, status 24 August 2026: https://www.fsma.be/en/list/authorised-belgian-crypto-asset-service-providers
- NBB — Markets in Crypto Assets Regulation (MiCAR): https://www.nbb.be/en/financial-supervision-and-resolution/supervision-financial-institutions/markets-crypto
- EUR-Lex — Regulation (EU) 2023/1114 (MiCA): https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32023R1114
- ESMA — MiCA Article 2 scope: https://www.esma.europa.eu/publications-and-data/interactive-single-rulebook/mica/article-2-scope
- ESMA — Guidelines on qualification of crypto-assets as financial instruments: https://www.esma.europa.eu/document/guidelines-conditions-and-criteria-qualification-crypto-assets-financial-instruments
- NBB — explanation of AISP/PISP licensing under PSD2: https://www.nbb.be/en/news-events/news/blog/what-do-we-have-do-your-new-cowboy-boots
