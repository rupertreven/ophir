# Ophir Go-to-Market

> **Status:** GTM hypothesis v0.1 — 28 August 2026

## 1. GTM principle

Ophir should not launch by selling "tokenized treasury" to the general SME market.

The first sale must solve a painful treasury workflow that exists **today**, while the architecture is ready for the tokenized economy **tomorrow**.

The initial commercial question is therefore:

> Which Belgian finance teams have enough treasury complexity to pay for a control layer, but are still underserved by heavyweight TMS implementations?

## 2. Ideal customer profile v0.1

### Core ICP

Belgian lower-mid-market company with:

- 10–249 employees;
- preferably €10m–€150m revenue;
- 2+ legal entities or 3+ bank accounts;
- one central finance team;
- recurring manual cash-position / forecast / reconciliation work;
- established ERP or accounting system;
- no dedicated enterprise TMS;
- CFO/finance director who owns both liquidity and process improvement.

Revenue boundaries are intentionally soft. Operational complexity is the stronger signal.

### High-propensity attributes

Prioritize companies with:

- multiple subsidiaries;
- cross-border suppliers/customers;
- multiple currencies;
- acquisitive growth;
- private-equity ownership or lender reporting requirements;
- significant working-capital swings;
- large idle cash balances;
- finance transformation projects;
- an ERP migration or consolidation underway;
- interest in stablecoins/tokenized products, but no internal crypto expertise.

## 3. Beachhead sectors

Do not choose the beachhead only by market size. Choose sectors where treasury pain is observable and repeatable.

Candidate priority sectors:

1. construction and project-based groups;
2. industrial/manufacturing groups;
3. wholesale/distribution;
4. logistics;
5. business-services groups with multiple legal entities;
6. technology/SaaS companies with international cash flows;
7. PE-backed buy-and-build groups.

The first 20 customer interviews should test these rather than assume one is best.

## 4. Initial wedge

### Product promise

> **Know exactly where your group's cash is — every day, across every bank and entity — without spreadsheet consolidation.**

This is intentionally conventional. It is easy for a CFO to understand and measure.

### MVP commercial package

**Ophir Observe**

- read-only multi-bank cash visibility;
- multi-entity consolidation;
- normalized transaction feed;
- simple short-term cash forecast;
- alerts/anomaly detection;
- accounting/ERP export;
- read-only digital-wallet visibility where relevant;
- audit trail;
- AI query layer over treasury data.

No payment execution and no investment execution in the first commercial package.

### Why read-only first

- lower regulatory perimeter;
- lower security risk;
- shorter implementation;
- easier customer approval;
- easier founder-led support;
- creates the data foundation needed for later workflow/automation modules.

## 5. Founder-led sales motion

For the first 20 customers, no scalable sales machinery should exist.

The founder does:

1. target-account selection;
2. discovery interview;
3. workflow mapping;
4. product demo/prototype;
5. implementation;
6. weekly feedback;
7. ROI measurement;
8. renewal/expansion conversation.

The goal is not maximizing bookings. It is finding the narrow workflow customers repeatedly pay to remove.

## 6. Customer-discovery script

Avoid asking: "Would you use tokenized treasury?"

Ask about actual behavior.

### Current process

- Walk me through how you know your total cash position this morning.
- How many bank portals/accounts/entities are involved?
- Who assembles the data?
- How long does this take each day/week?
- Which spreadsheets are business-critical?
- How is the cash forecast produced?
- How often is it wrong and why?
- How are intercompany transfers handled?
- How are bank transactions reconciled with accounting?

### Cost and risk

- What happens when cash information is late or wrong?
- How much operating cash buffer do you keep because visibility is imperfect?
- Have you ever had a payment/liquidity surprise?
- What does month-end treasury reconciliation cost in time?

### Existing solutions

- Have you evaluated a TMS such as Kyriba, Agicap or alternatives?
- Why did you buy/not buy it?
- What implementation effort is unacceptable?
- What would need to be automated for this to be worth €500/€1,000/€2,000 per month?

### Future rails

Only after understanding the existing workflow:

- Would you hold regulated EUR stablecoins if your bank/accounting experience remained unchanged?
- Would tokenized money-market funds be interesting if they appeared as another treasury account?
- What would stop you: accounting, regulation, custody, board policy, risk, tax or lack of understanding?

## 7. Design-partner programme

Recruit **5 design partners** before building broadly.

Ideal mix:

- 2 companies with simple but painful multi-bank treasury;
- 2 multi-entity groups;
- 1 digitally sophisticated company open to tokenized cash experimentation.

Offer:

- discounted first-year contract;
- founder-level support;
- influence over roadmap;
- transparent early-product status.

Require in return:

- weekly access to finance users;
- permission to measure before/after process time;
- willingness to provide a reference/case study if value is proven;
- real data/integrations rather than a purely hypothetical pilot.

Avoid free pilots where possible. Even a modest paid commitment is stronger validation.

## 8. Pricing experiments

Do not launch with €99/month consumer-SaaS pricing. Treasury software touches high-value workflows, requires integrations and must support serious security expectations.

Test three packages:

### Observe

€400–€750/month hypothesis

- cash visibility;
- basic forecasting;
- limited entities/accounts;
- read-only.

### Control

€1,000–€2,000/month hypothesis

- multi-entity;
- ERP integration;
- reconciliation;
- advanced policies/workflows;
- richer AI.

### Enterprise

€25k+ ARR hypothesis

- complex group structures;
- custom connectivity;
- SSO/security requirements;
- partner-led execution;
- SLA/support.

Implementation fees should be charged where customer-specific work exists. The strategic goal is to reduce implementation effort until most customers can onboard with standardized connectors.

All prices are hypotheses until willingness-to-pay interviews are completed.

## 9. Distribution channels

### Phase A — direct network and warm introductions

Fastest path to truth. Target CFOs, finance directors and group controllers.

### Phase B — accounting and finance-transformation partners

Accountants and CFO-as-a-service firms repeatedly see fragmented cash-management workflows. They can become both lead source and implementation partner.

### Phase C — ERP ecosystem

ERP implementation firms are attractive because treasury pain often appears during finance-system consolidation.

Priority ecosystem hypotheses for Belgium:

- Microsoft Dynamics / Business Central;
- Odoo;
- Exact;
- SAP Business One / S/4HANA in larger accounts;
- sector-specific ERP/accounting systems where a repeatable niche emerges.

Integration priority should follow customer evidence, not founder preference.

### Phase D — regulated infrastructure partners

Licensed open-banking, payment, custody and digital-asset providers can give Ophir regulated capabilities without turning Ophir into every regulated institution itself.

Partner selection criteria:

- EU/Belgian regulatory status;
- API quality;
- white-label/embedded capability;
- EUR support;
- security posture;
- pricing;
- geographic reach;
- ability to support corporate accounts;
- data portability and avoidance of vendor lock-in.

## 10. Messaging ladder

### CFO headline

> **All your capital. One intelligent treasury.**

### Practical wedge

> Stop consolidating cash across banks and entities in spreadsheets.

### Strategic expansion

> Manage bank money, digital cash and tokenized financial assets through one governed control layer.

### Technical/investor explanation

> Ophir is an asset-agnostic treasury operating system connecting ERP/accounting data, traditional banking and tokenized financial rails with a policy-governed AI layer.

Never lead SME sales with blockchain terminology unless the buyer explicitly has that pain.

## 11. Sales qualification score

Score leads 0–2 on each dimension:

- bank-account count;
- entity count;
- currencies/cross-border exposure;
- hours of manual treasury work;
- quality of existing cash forecast;
- ERP maturity;
- executive urgency;
- budget authority;
- openness to SaaS/cloud finance tools;
- future digital-asset relevance.

Prioritize accounts with the highest pain + urgency, not the highest tokenization enthusiasm.

## 12. First-year targets — validation, not vanity

### Milestone 1

20 structured customer interviews.

Pass condition: at least 10 report the same high-value workflow problem.

### Milestone 2

5 design partners.

Pass condition: at least 3 willing to pay for the initial product.

### Milestone 3

10 paying customers.

Pass condition: onboarding process is repeatable and founder support load is manageable.

### Milestone 4

€100k+ ARR.

Pass condition: evidence of retention, usage and measurable ROI.

### Milestone 5

€500k ARR.

Pass condition: acquisition and onboarding begin to work beyond close personal network.

The first-year objective is not maximizing revenue. It is proving **repeatability**.

## 13. Metrics that matter

Product:

- number of connected bank accounts/entities;
- daily/weekly active finance users;
- time to first live cash position;
- forecast accuracy improvement;
- automated reconciliation percentage;
- alerts acted upon;
- manual hours eliminated.

Business:

- ACV;
- implementation hours per customer;
- gross margin;
- sales-cycle duration;
- customer acquisition source;
- churn;
- expansion revenue;
- ARR per human employee.

One-man-unicorn constraint:

> **Implementation hours per customer is a strategic metric, not an operations detail.**

If every customer needs weeks of bespoke integration, the AI-native small-team model breaks.

## 14. Expansion sequence

### Phase 1 — Observe

Read-only bank + ERP treasury visibility.

### Phase 2 — Understand

Forecasting, anomaly detection, reconciliation, liquidity intelligence.

### Phase 3 — Control

Policies, approvals and workflow orchestration.

### Phase 4 — Connect digital capital

Stablecoins, tokenized deposits, tokenized funds and securities presented through the same capital model.

### Phase 5 — Act through partners

Customer-approved transactions routed through licensed providers.

### Phase 6 — Governed autonomy

Routine treasury actions proposed and eventually executed by AI within explicit limits, permissions and human approval rules.

## 15. GTM kill criteria

Pause or pivot if after 30 high-quality interviews:

- treasury pain is real but willingness to pay is consistently below viable SaaS economics;
- customers overwhelmingly prefer their bank/ERP to solve the problem;
- implementation complexity cannot be standardized;
- the buying cycle requires enterprise sales effort at SME ACVs;
- a modern incumbent solves the same problem at materially better economics;
- tokenized-capital demand remains too weak to create eventual differentiation.

## 16. Current GTM verdict

Start narrow and boring.

Sell **cash control**, not crypto.

Use that wedge to earn access to the company's financial data model and treasury workflow. Then expand upward into policy, automation and tokenized assets.

The long-term ambition remains large, but the first customer should buy Ophir even if they never use a blockchain in year one.
