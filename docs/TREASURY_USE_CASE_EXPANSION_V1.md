# Treasury Use Case Expansion v1

> **Date:** 2026-08-28 23:59 CEST  
> **Status:** `PUBLIC_SOURCE_RESEARCH` / product discovery  
> **Objective:** broaden Ophir beyond short-term yield optimization while reusing the current banking, accounting, rules, approval, provider-handoff and reconciliation architecture.

## Thesis

Ophir should not be designed around one product class (tokenized MMFs). The reusable architecture can support multiple corporate treasury problems where regulated tokenized money/assets create measurable operational or capital-efficiency value.

Core architecture reused across use cases:

```text
Banks / ERP / accounting / payroll / TMS
                │
                ▼
        Ophir Treasury Ledger
                │
       Forecast + Policy Engine
                │
    Instrument / Rail Intelligence
                │
       Tax + Accounting Rules
                │
         Approval Workflow
                │
      Regulated Provider Handoff
                │
          External Execution
                │
       Reconciliation + Documents
```

## Priority use cases

### UC1 — Daily-liquid surplus cash optimization

**Problem:** corporate operational cash often earns low overnight rates because it must remain liquid.

**Tokenized instrument:** regulated tokenized MMFs / short-term cash funds.

**Value:** keep cash invested until needed; daily/near-real-time transferability; potentially daily yield accrual; automated reconciliation.

**Current evidence:** ECB says TMMFs can provide faster settlement, near-24/7 availability, programmability and collateral use while retaining MMF economics. BlackRock explicitly markets tokenized MMFs to treasury teams for liquidity management.

**Ophir role:** forecast deployable cash, compare like-for-like liquid products, calculate Belgian after-tax result, prepare regulated-provider handoff, reconcile and generate accounting/tax pack.

**Target:** SME through enterprise.

### UC2 — Just-in-time payroll funding

**Example customer:** social secretariat, payroll processor, multi-entity employer.

**Problem:** payroll requires large, predictable payment waves. Cash may be pre-funded in accounts ahead of payment cutoffs, producing idle balances and operational risk.

**Tokenized rail:** bank-backed tokenized deposits / regulated digital money; potentially regulated stablecoins where appropriate.

**Value hypothesis:** keep liquidity centralized/invested longer, move it to payment accounts/entities closer to execution time, automate funding conditions and reconcile instantly.

**Evidence:** J.P. Morgan Blockchain Deposit Accounts support 24/7 near-real-time programmable money movement and position the product for global corporate treasury. Mitsubishi uses Kinexys for intragroup USD cash management. Citi reports Siemens uses Token Services for near-instant funding/liquidity management and cross-border transfers beyond local cutoffs.

**Ophir workflow:** payroll file/forecast -> funding requirement by entity/currency/time -> policy check -> funding plan -> human approval -> bank/tokenized-deposit provider executes -> reconcile payroll settlement.

**Potential value:** less prefunding, fewer idle balances, reduced manual treasury operations, lower failed-payment risk.

**Target:** social secretariats, payroll processors, large employers, staffing companies.

### UC3 — Multi-entity / cross-border liquidity sweeping

**Example customer:** construction group with many subsidiaries/project entities; international industrial company.

**Problem:** cash is fragmented across legal entities, countries, currencies and bank accounts. Traditional sweeps operate on banking windows and require cash pools/intercompany accounting.

**Tokenized rail:** tokenized bank deposits / blockchain deposit accounts; on-chain FX.

**Value:** near-real-time or programmable intragroup transfers, 24/7 liquidity movement, reduced prefunding, fewer idle balances and potentially fewer bank/cash-pool structures.

**Evidence:** J.P. Morgan says Mitsubishi adopted programmable 24/7 intragroup cash management; its BDA product is designed to centralize/mobilize global corporate liquidity. Siemens reportedly reduced bank accounts and cash pools by over 50% while adopting programmable/blockchain/virtual-account treasury technology (provider case study; exact causal attribution should be treated cautiously).

**Ophir role:** global cash map, entity constraints, intercompany rules, tax/accounting entries, approval and provider orchestration.

**Target:** mid-market and enterprise groups.

### UC4 — 24/7 cross-border supplier / contractor payments

**Example customer:** construction company paying international suppliers/subcontractors; global staffing/payroll platform.

**Problem:** bank cutoffs, correspondent chains, weekend/holiday delays, FX windows, prefunding and reconciliation.

**Tokenized rail:** tokenized deposits, regulated EUR stablecoins/EMTs, on-chain FX.

**Value:** wider settlement windows, near-real-time cross-border settlement, conditional/scheduled payments, potentially less cash-in-transit and prefunding.

**Evidence:** J.P. Morgan On-Chain FX markets 24/7 near-real-time FX/payment settlement to global corporates; SG-FORGE positions MiCA-compliant EURCV/USDCV as institutional-grade digital money for corporate treasury; HSBC describes tokenized deposits as suitable for wholesale transfers and digital currencies as offering 24/7 liquidity/automation.

**Ophir role:** compare conventional bank payment vs tokenized rail on FX spread, fees, timing, counterparty/regulatory treatment and accounting; user approves at provider.

**Target:** companies with meaningful international payment volume.

### UC5 — Yield-bearing operational collateral

**Example customer:** energy trader, commodity company, logistics group, large contractor with financial collateral needs, institution using exchanges/derivatives.

**Problem:** collateral/margin often sits idle in cash while posted; moving/replacing collateral is operationally slow.

**Tokenized instrument:** regulated tokenized MMF/Treasury-fund shares accepted as collateral.

**Value:** collateral can continue earning yield while being mobilized; faster substitution/transfer; regulated custody can remain off-venue.

**Evidence:** BlackRock + Standard Chartered + OKX launched a 2026 framework allowing BUIDL to be used as yield-bearing collateral while held in regulated custody. ECB identifies collateral for derivatives/repo as a core TMMF use case.

**Ophir role:** collateral inventory, eligibility rules, haircut/liquidity/yield comparison, provider handoff, accounting and evidence.

**Target:** primarily larger corporates / financial institutions; less relevant to ordinary SME.

### UC6 — Bank guarantees / trade-finance document orchestration

**Example customer:** construction company.

**Problem:** performance guarantees, advance-payment guarantees, letters of credit and related documents are slow, paper-heavy and difficult to reconcile with projects/ERP.

**Digital/tokenized instrument:** digitally native guarantees / electronic trade documents; potentially DLT-backed bank guarantees rather than an investable token.

**Value:** issuance/verification speed, less fraud/document handling, direct linkage to project milestones and accounting/ERP.

**Evidence:** Swedbank reported a 2026 pilot digitising guarantees and export LCs where traditional processes taking two to three days were targeted for faster open digital workflows. The European Commission identifies tokenisation/DLT as capable of reducing settlement friction and streamlining reconciliation.

**Ophir role:** guarantee register + project/ERP link + expiry alerts + approval + bank/provider handoff + fee/accounting reconciliation. This fits the architecture even if the final instrument is not public-chain tokenized.

**Target:** construction, manufacturing, import/export, infrastructure.

### UC7 — Working-capital / receivables financing marketplace

**Problem:** companies have invoices/receivables while simultaneously holding or borrowing working capital; financing is fragmented and bank-specific.

**Potential tokenized instrument:** regulated tokenized receivables/private credit/trade-finance claims.

**Value hypothesis:** standardized digital ownership and settlement can make financing assets easier to distribute and automate, potentially widening financing sources and shortening funding cycles.

**Status:** strategically interesting but not MVP-ready. Regulatory, credit-underwriting, true-sale, assignment, debtor-notification and Belgian accounting/legal complexity is high. Concrete EU SME-accessible regulated products need further research.

**Ophir role:** determine funding need from ledger, compare bank line/factoring/tokenized financing after all-in cost, prepare documents, reconcile financing and repayment.

**Target:** SMEs/mid-market with working-capital intensity.

### UC8 — Short-term corporate funding / tokenized commercial paper

**Example customer:** large corporate / very large mid-market.

**Problem:** bank credit may be more expensive/inflexible than direct short-term capital-market funding; issuance/admin/settlement can be costly.

**Tokenized instrument:** DLT-native commercial paper / short-term notes.

**Evidence:** EIB issued euro-denominated DLT-native commercial paper on Clearstream D7 in June 2026; it was distributed internationally and could be posted as ECB-eligible collateral through Clearstream infrastructure. ECB notes non-financial corporates have already begun DLT bond issuance.

**Value:** potentially faster issuance/settlement, broader digital distribution, automated lifecycle/servicing, collateral mobility.

**Ophir role:** probably not issuer itself; funding-needs detection, compare bank line vs CP economics, documentation/workflow/data room, regulated arranger/provider handoff, post-issuance cash/accounting tracking.

**Target:** large companies, not typical Belgian SME v1.

### UC9 — Conditional supplier payments / programmable escrow-like workflows

**Example customer:** construction.

**Problem:** payment depends on delivery, milestone acceptance, retention release or supporting documents. Manual sequencing creates disputes and delays.

**Tokenized rail:** programmable bank deposits/digital money paired with digitally verifiable conditions.

**Value:** payment can be prepared/released when approved conditions are satisfied; atomicity can link asset/document event and payment; shared status improves reconciliation.

**Evidence:** ECB describes programmability as allowing market participants to define conditions spanning a financial instrument lifecycle; J.P. Morgan describes programmable money supporting conditional release/scheduled/rule-based transfers and explicitly cites goods-delivered-triggered payments as the direction of institutional infrastructure.

**Boundary:** Ophir should remain workflow/control layer; regulated bank/payment provider moves funds. Project certification/acceptance remains an authorized human/business-system event.

**Target:** construction, procurement-heavy businesses, marketplaces.

### UC10 — FX liquidity optimization

**Problem:** companies pre-fund currencies or execute FX early because of cutoffs and settlement windows, leaving idle balances and creating FX exposure.

**Tokenized rail:** multi-currency tokenized deposits + on-chain FX.

**Value:** just-in-time currency conversion, wider dealing windows, reduced prefunding/cash-in-transit, potentially reduced settlement risk.

**Evidence:** J.P. Morgan offers On-Chain FX for 24/7 near-instant cross-currency settlement and positions it for global corporate treasury. Kinexys expanded blockchain deposit accounts to eight currencies in 2026.

**Ophir role:** forecast currency needs, quantify prefunding/FX exposure, compare rails/rates, policy approval, provider execution, reconciliation.

**Target:** international mid-market and enterprise.

## Prioritisation

### Tier 1 — strongest near-term Ophir fit

1. Daily-liquid surplus cash optimization.
2. Multi-entity liquidity / programmable sweeping.
3. Just-in-time payroll funding.
4. Cross-border supplier payments + FX optimization.
5. Digital guarantee register/orchestration for construction/trade-heavy companies.

These mostly reuse banking/accounting/forecast/rules/approval/reconciliation and leave regulated execution to banks/providers.

### Tier 2 — valuable but larger-enterprise biased

6. Yield-bearing collateral.
7. Conditional supplier settlement.
8. Tokenized commercial-paper/funding optimization.

### Tier 3 — later / regulatory complexity

9. Receivables/private-credit financing marketplace.
10. Autonomous allocation/execution.

## Vertical examples

### Social secretariat / payroll processor

Potential Ophir product:

```text
Payroll obligations by client/entity/time
        + incoming prefunding
        + bank balances
        + liquidity policy
                │
                ▼
     Funding gap / idle cash map
                │
        ┌───────┴────────┐
        ▼                ▼
liquid yield sleeve   just-in-time funding
(TMMF)                (tokenized deposit)
        │                │
        └───────┬────────┘
                ▼
      approved payroll settlement
                ▼
        automatic reconciliation
```

Possible value is not merely yield. It is **reducing the amount and duration of prefunded payroll cash** while preserving execution certainty.

### Construction company/group

Potential Ophir product:

```text
Bank cash + project ERP + AP forecast
              │
              ▼
      project/entity liquidity map
              │
   ┌──────────┼─────────────┐
   ▼          ▼             ▼
surplus    guarantees    supplier/FX
cash       & LCs         payments
   │          │             │
MMF/FCP   digital bank   programmable
optimizer guarantee      payment rail
   │          │             │
   └──────────┴──────┬──────┘
                     ▼
          accounting + tax + audit
```

This is much stronger than a standalone 'tokenized yield' feature because it solves several treasury workflows around the same data model.

## Strategic conclusion

The broader opportunity is not a tokenized-investment marketplace.

> **Ophir can become the policy, intelligence, compliance and reconciliation layer through which a company decides when traditional or tokenized financial rails improve its treasury.**

The strongest tokenization benefits found in current institutional deployments are often operational rather than higher investment returns:

- 24/7 movement;
- less prefunding;
- faster settlement;
- programmable conditions;
- automatic/shared reconciliation;
- collateral mobility;
- integration of cash and assets on the same rails.

This means Ophir's economic model should quantify **working-capital release and operational savings**, not only yield uplift.

## Next research

For each Tier-1 use case, produce one quantified company scenario with public/provider data where possible:

1. social secretariat — EUR 20m payroll batch, days of prefunding reduced;
2. construction group — multi-entity cash trapped across accounts;
3. international supplier payment — FX/prefunding/cutoff economics;
4. daily cash sleeve — liquid bank cash vs regulated MMF;
5. guarantee workflow — time/fees/admin savings.

The goal is to identify which wedge can plausibly create **EUR 25k–250k+ annual customer value**, rather than optimizing for a few thousand euros of quarterly yield.
