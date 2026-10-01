# Ophir Market Analysis

> **Status:** Research memo v0.1 — 28 August 2026
>
> This memo distinguishes observed market facts from Ophir assumptions. TAM figures are deliberately bottom-up and should be revised after customer discovery.

## 1. Core market hypothesis

Ophir is not betting on a standalone "crypto treasury" market. The target market is the broader corporate treasury software and financial-control layer, with tokenized money and assets becoming an additional rail inside that workflow.

The near-term wedge is therefore conventional treasury pain — fragmented bank accounts, manual cash visibility, forecasting, reconciliation and approvals — while the long-term expansion vector is stablecoins, tokenized funds, tokenized bonds and governed AI execution.

## 2. Belgian beachhead

Belgium is unusually attractive as a proving ground because it combines a dense SME base, sophisticated banking/ERP adoption, a multilingual market and EU financial regulation.

Official Belgian statistics show:

- 1,186,099 VAT-liable SMEs at year-end 2024 (FPS Economy).
- 225,374 private-sector SME employers with 1–249 employees at year-end 2024.
- Statbel's employee-class table shows 36,135 VAT-liable businesses with 10–249 employees and 67,567 with 5–249 employees.
- Belgium's SME population is concentrated in Flanders: 746,373 VAT-liable SMEs, 62.9% of the national total.

Sources:

- https://economie.fgov.be/nl/themas/ondernemingen/kmos-en-zelfstandigen-cijfers/statistieken-over-kmos-belgie
- https://economie.fgov.be/nl/themas/ondernemingen/kmos-en-zelfstandigen-cijfers/tewerkstelling-bij-kmos
- https://bestat.statbel.fgov.be/bestat/crosstable.xhtml?view=9d19ebe2-f35a-4b51-ac1a-c153e6d77d67

### Why total SME count is misleading

Most Belgian SMEs are too small to need Ophir. The relevant segment is companies with enough treasury complexity to suffer from fragmented cash visibility but not enough scale to justify a large enterprise TMS implementation.

The initial segmentation hypothesis should therefore use operational complexity rather than legal SME status:

- 10–249 employees as a useful first proxy;
- 2+ legal entities and/or 3+ bank accounts;
- meaningful working-capital swings;
- finance team of roughly 2–20 people;
- ERP/accounting system already in place;
- recurring manual treasury work in Excel and banking portals.

Revenue remains useful for qualification, but employee count, entity count and bank-account count are probably better predictors of pain.

## 3. Bottom-up Belgian market model

### Addressable-company base

Statbel reports approximately **36,135 Belgian VAT-liable enterprises with 10–249 employees** in 2024.

This is not Ophir's SAM. Many will have simple cash structures or no willingness to buy a dedicated treasury layer.

We therefore model three filters.

| Scenario | Share with sufficient complexity | Addressable companies |
|---|---:|---:|
| Conservative | 20% | ~7,200 |
| Base | 35% | ~12,650 |
| Upside | 50% | ~18,100 |

These percentages are Ophir assumptions, not external market facts. Customer discovery must replace them.

### ACV hypothesis

The right price is not yet known. The product should be priced against avoided finance-team effort, reduced liquidity buffers, better cash control and lower operational risk — not against transaction volume or token value.

Initial annual recurring revenue hypotheses:

| Segment | Indicative ACV hypothesis |
|---|---:|
| Small / single-country | €3k–€6k |
| Core lower mid-market | €6k–€15k |
| Multi-entity / complex | €15k–€30k+ |

A reasonable base blended ACV for modelling is **€9k–€12k**, pending interviews.

### Belgian SAM range

Using the complexity filters above and a €9k blended ACV:

- Conservative: ~7,200 × €9k = **~€65m ARR**
- Base: ~12,650 × €9k = **~€114m ARR**
- Upside: ~18,100 × €9k = **~€163m ARR**

This is a theoretical software revenue pool, not a forecast of attainable Ophir revenue.

At a €12k blended ACV, the same base cohort implies ~€152m ARR.

### Belgian SOM

For a founder-led, AI-native company, a more useful near-term question is: how many customers are required to build a meaningful business?

- 50 customers × €10k ACV = €0.5m ARR
- 100 customers × €10k ACV = €1m ARR
- 500 customers × €12k ACV = €6m ARR
- 1,000 customers × €15k ACV = €15m ARR

Ophir does not need dominant national market share to become a substantial Belgian SaaS company.

## 4. European expansion

The European Commission's 2025/2026 SME Performance Review reports roughly **34 million SMEs in the EU in 2025**. That number is far too broad for Ophir's TAM because the overwhelming majority are micro firms.

Eurostat reported for the EU business economy in 2024:

- around 33.5 million enterprises in total;
- ~251,000 medium-sized enterprises with 50–249 employees;
- the vast majority of the remainder are micro/small firms.

The Commission's 2024 SME dataset estimated approximately 1.405 million small enterprises (10–49 employees) and 214,000 medium enterprises (50–249 employees) in the non-financial business economy, or roughly **1.62 million enterprises with 10–249 employees**.

Sources:

- https://single-market-economy.ec.europa.eu/publications/annual-report-european-smes-20252026_en
- https://ec.europa.eu/eurostat/web/products-eurostat-news/w/ddn-20251209-2
- https://webgate.ec.europa.eu/circabc-ewpp/d/d/workspace/SpacesStore/e2f2be77-5257-4d05-9700-2c2f34f96294/download

Applying a deliberately conservative 20–35% treasury-complexity filter would imply roughly **320k–570k potentially relevant EU companies** before product/sector/geography filtering.

At €9k–€15k ACV, that corresponds to a theoretical European revenue pool measured in several billions of euros annually. This is best treated as evidence that the ceiling is large, not as an investor-facing TAM claim until the segmentation model is validated.

## 5. Why now

### Traditional treasury software is moving downmarket

Kyriba now explicitly markets "Essentials for Mid-Market", bundling cash management, forecasting, payments/controls and agentic AI. This validates both the pain and the willingness of enterprise TMS vendors to pursue smaller companies.

Source: https://www.kyriba.com/solutions/midsize-companies/

### Modern European TMS vendors are growing into the gap

Agicap markets cash management to finance teams and states that it serves 7,000+ businesses globally. Its product includes bank/ERP connectivity, cash positioning, forecasts, reconciliation and payments.

Source: https://agicap.com/en/products/cash-management/

Embat targets mid-market treasury teams with real-time bank/ERP connectivity, AI-assisted reconciliation, cash forecasting and payments. It reports 500+ corporate finance customers and connectivity to 15,000+ financial institutions.

Source: https://www.embat.io/treasury-management

Fygr positions a simpler product for SMEs and states that 3,000+ SMEs use its cash-flow software.

Source: https://www.fygr.io/nl/global/logiciel-de-tresorerie/logiciel-tresorerie-pme

This means Ophir is entering an already validated category. The opportunity cannot be based on "SMEs still use Excel" alone. The differentiation must come from the next control layer: traditional + tokenized capital, regulatory abstraction and governed AI orchestration.

## 6. Tokenized-capital expansion vector

Digital-asset infrastructure vendors are increasingly targeting corporate treasury directly.

Fireblocks now markets a dedicated corporate-treasury proposition covering stablecoin settlement, policy controls, tokenized T-bill yield, TMS integration and ERP-ready reporting. Fireblocks states it serves 2,400+ institutions and processes more than $200bn in stablecoin transactions monthly.

Sources:

- https://www.fireblocks.com/use-case/corporate-treasury
- https://www.fireblocks.com/blog/earn-on-stablecoin-balances

BVNK's 2026 partnership with Corpay is particularly relevant: the announced model brings stablecoin wallets and 24/7 settlement into a corporate-payments interface used by more than 800,000 enterprise clients, with stablecoin balances shown next to fiat balances.

Source: https://www.bvnk.com/blog/corpay-partners-with-bvnk-to-add-stablecoin-wallets

This is strong evidence for Ophir's core abstraction thesis: **business users will increasingly encounter tokenized money inside familiar financial software rather than through crypto-native interfaces.**

## 7. Market conclusion

The market evidence supports a stronger but narrower thesis than "tokenization creates a new treasury category".

The category already exists: corporate cash/treasury management. Modern SaaS vendors are successfully moving it downmarket and adding AI. Digital-asset infrastructure vendors are simultaneously moving stablecoins and tokenized instruments into treasury workflows.

Ophir's opportunity is to sit at the convergence:

**traditional bank treasury + ERP/accounting + tokenized capital + governed AI.**

The initial product must be valuable even if tokenization adoption is slower than expected. Tokenization should expand the product's strategic value, not be required for product-market fit.

## 8. Validation questions

Before treating the base-case SAM as credible, validate:

1. What percentage of Belgian 10–249 employee firms operate 3+ bank accounts or 2+ legal entities?
2. How many hours per week do finance teams spend collecting and reconciling cash positions?
3. At what complexity threshold do companies buy Agicap/Embat/Kyriba instead of remaining in Excel?
4. What is realistic Belgian willingness to pay for a read-only control plane?
5. Which ERP/accounting integrations dominate the beachhead?
6. Do CFOs care about stablecoins/tokenized funds today, or is this still purely a future expansion story?
7. Which industries have the highest cross-border, multi-currency or multi-entity treasury pain?
8. How much implementation effort can be tolerated while preserving a one-person/AI-native operating model?

## 9. Current market verdict

**Belgium is large enough to validate and build the first several million euros of ARR. Europe is large enough for venture-scale upside.**

The critical uncertainty is not market population. It is whether Ophir can find a sufficiently painful, repeatable workflow that is materially differentiated from modern TMS vendors and can be deployed with low implementation overhead.
