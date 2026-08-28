# Ophir — Banking vs Tokenized Treasury Rails (Belgium/EU)

> Status: research memo v0.1 — 28 Aug 2026. Not legal, tax or accounting advice.

## Executive conclusion

For a Belgian SME, tokenized treasury is **not automatically better** than bank treasury. Bank connectivity is already reasonably accessible through licensed aggregators such as Isabel/Ponto, while tokenized rails add regulatory, accounting, custody and operational complexity.

The tokenized advantage becomes meaningful when a company needs one or more of the following:

1. 24/7 settlement and transferability;
2. cross-border programmable money movement;
3. rapid movement between cash-like assets and yield-bearing instruments;
4. collateral mobility and reuse;
5. multi-provider treasury orchestration that is not tied to one bank;
6. API-native execution for governed software/AI agents.

For the average Belgian SME today, the strongest initial Ophir product should therefore **start from bank and accounting connectivity** and add tokenized rails only where they demonstrably improve economics or operational flexibility.

## 1. Belgian bank connectivity: more open than expected

Belgian banks do not generally expose unrestricted public corporate banking APIs in the way a developer might expect from Stripe. PSD2 APIs exist, but direct access can bring licensing and bank-specific complexity.

The practical route is an aggregator.

Isabel states that:

- Isabel 6 consolidates account information and payment capabilities from more than 500 banks via partner banks;
- Ponto provides access to more than 1,700 European banks and payment providers;
- Ponto supports both account information and payment initiation;
- Isabel exposes embedded/open-banking APIs for software partners.

This changes the Ophir architecture. Ophir does **not** need to negotiate bilateral integrations with KBC, Belfius, ING Belgium and BNP Paribas Fortis for the first MVP. It can initially integrate a licensed aggregator such as Ponto/Isabel and remain the orchestration/data layer.

Source: https://www.isabel.eu/en

## 2. What are tokenized alternatives actually competing with?

The treasury comparison is not “bank account vs crypto”. It is closer to:

### Traditional rails

- current account / savings / term deposit;
- money-market fund via bank/broker;
- government or corporate bonds via securities account;
- SEPA/instant payments;
- bank credit and guarantees.

### Tokenized rails

- EURC / regulated euro e-money token;
- tokenized deposits;
- tokenized money-market funds;
- tokenized government debt and eventually corporate debt;
- tokenized fund/securities positions that can move or be pledged on-chain.

The economic asset can be nearly identical; the difference is primarily **settlement, programmability, transferability, integration and collateral utility**.

## 3. Stablecoins: liquidity rail, not return product

EURC is a useful example. Circle states that EURC is MiCA-compliant, backed by euro, redeemable 1:1 and available on multiple public blockchains. Businesses can mint and redeem through Circle Mint.

However, EURC itself pays **no yield**. Circle's MiCA white paper explicitly says holders are not entitled to interest earned on reserves.

So the CFO case for holding EURC is not “earn more”. It is:

- 24/7 transferable euro liquidity;
- programmable settlement;
- cross-border movement without banking-hour dependency;
- direct interaction with tokenized assets;
- API-native treasury workflows.

Sources:
- https://www.circle.com/eurc
- https://www.circle.com/legal/mica-eurc-whitepaper

## 4. On/off ramps are becoming viable

Circle Europe is an EU-regulated electronic-money institution and also holds a MiCA CASP licence in France as of 2026. Its EU redemption policy allows eligible holders to redeem EURC to an EEA bank account subject to KYC/KYT and AML controls.

Circle Mint also provides institutional mint/redemption infrastructure. Circle describes standard/institutional processing as near-instant in some tiers, although its public MiCA redemption fallback may take up to five business days and compliance checks can delay redemptions.

Therefore the ramp is no longer the existential problem it was several years ago. The remaining issues are:

- onboarding/KYB friction;
- AML/KYT screening;
- bank acceptance and compliance reviews;
- fees/limits at scale;
- chain/network support;
- operational controls around addresses and wallets.

Sources:
- https://www.circle.com/legal/mica-redemption-policy
- https://help.circle.com/support/en/usdc-eurc-redemption-structure?id=kb_article_view&sysparm_article=KB0010644

## 5. Tokenized MMFs: this is where return + liquidity starts to matter

A stablecoin separates liquidity from yield. A tokenized money-market fund can combine a cash-management return with on-chain utility.

This moved materially forward in Europe in August 2026. BlackRock launched tokenized access to selected Institutional Cash Series money-market funds in Europe, including euro share classes, using J.P. Morgan Kinexys and Ethereum. BlackRock describes the products as existing regulated money-market fund structures with tokenized functionality and existing institutional-scale liquidity.

Franklin Templeton also has blockchain-native money-market and UCITS initiatives and emphasizes wallet-to-wallet transferability, intraday yield and the ability to use tokenized MMF holdings as collateral in digital markets.

This is likely the strongest long-term Ophir treasury use case:

**Idle operational cash → regulated yield-bearing cash equivalent → still programmable / rapidly mobilisable as collateral or settlement asset.**

Sources:
- https://www.blackrock.com/cash/en-ie/press-release-t4
- https://www.franklintempleton.com/press-releases/news-room/2026/franklin-templeton-stellar-development-foundation-mark-five-years-of-benji-the-first-u.s.-registered-tokenized-money-market-fund
- https://www.franklintempleton.com/articles/2025/disruption/tokenized-money-market-funds-the-bridge-to-a-new-financial-infrastructure

## 6. What is the real liquidity advantage?

Tokenization does **not create economic liquidity from nothing**. A thinly traded bond remains a thinly traded bond.

Tokenization can improve *operational liquidity*:

- settlement can occur continuously rather than only inside market/banking windows;
- ownership records can update immediately;
- assets can potentially transfer wallet-to-wallet;
- cash-like and yield-bearing instruments can interoperate on the same rail;
- collateral can be moved or pledged without first liquidating to bank cash;
- software can automatically rebalance between allowed instruments.

This distinction is crucial for Ophir:

> **Market liquidity is a property of buyers/sellers. Operational liquidity is a property of infrastructure. Tokenization mainly improves the latter.**

## 7. Regulation: where the overhead really appears

### Stablecoins / crypto-assets

MiCA regulates custody, exchange, order execution/transmission, advice, portfolio management and transfers of crypto-assets on behalf of clients. A company like Ophir should initially avoid becoming the provider of those regulated services and instead orchestrate licensed partners.

Belgium implemented MiCA through the Law of 11 December 2025, and the legacy transition ended on 1 July 2026.

Source: https://www.fsma.be/en/crypto-asset-service-provider-casp

### Tokenized securities/funds

A tokenized fund share, bond or equity may remain a regulated financial instrument. Tokenization does not remove MiFID/fund/securities rules. In many cases the legal wrapper remains conventional and only the transfer/recording rail changes.

This means Ophir needs an asset-classification layer rather than a binary 'crypto / not crypto' model.

### Tax transparency

Belgium transposed DAC8/CARF in March 2026. Reporting crypto-asset service providers face due-diligence and reporting requirements and information will be exchanged with tax authorities.

For an ordinary corporate holder, this means the direction of travel is toward **more automatic tax transparency**, not an opaque crypto environment.

Source: https://finance.belgium.be/en/E-services/dac8

## 8. Belgian accounting/tax friction

This is currently one of the biggest reasons Ophir could create value.

Belgian companies must keep full accounting records appropriate to their activities and retain supporting documents. Corporate taxable income starts from accounting profit and is then adjusted for tax purposes. The standard corporate income-tax rate is 25%.

There is no simple universal accounting bucket called 'tokenized asset'. Classification depends on what the token legally/economically represents:

- EURC-like EMT: cash-like claim/e-money analysis;
- tokenized MMF: fund/security treatment;
- tokenized bond: debt security treatment;
- utility/other crypto: separate asset analysis.

This requires validation with a Belgian accountant/auditor and, for material deployments, probably a written accounting policy.

For tokenized securities, Belgian transaction taxes can also matter. Belgian legal persons can themselves become liable for TOB when transactions are executed through a foreign professional intermediary and the tax has not otherwise been paid. Applicable treatment depends on the exact instrument and transaction.

Sources:
- https://finance.belgium.be/en/enterprises/corporation-tax/accounting
- https://finance.belgium.be/en/node/11884
- https://finance.belgium.be/en/enterprises/other-taxes/financial-institutions-and-insurance-companies/tax-stock-exchange

## 9. Operational burden for the CFO

A tokenized treasury stack can introduce:

- KYB with each regulated provider;
- wallet/address governance;
- transaction signing policies;
- custody/vendor due diligence;
- chain/network risk;
- smart-contract risk;
- reconciliation between wallet, custodian and accounting ledger;
- pricing/valuation feeds;
- AML/KYT evidence;
- tax-lot and transaction history;
- auditor evidence;
- recovery procedures for lost/compromised keys;
- legal classification per instrument.

If these steps are manual, tokenization can easily be **worse** than the bank.

This is therefore not merely friction for Ophir to tolerate. It may be the core product opportunity.

## 10. When does it financially make sense?

### Stablecoin only

For a euro-based Belgian company that has no on-chain suppliers/customers/assets, the financial return is usually weak: EURC itself yields nothing. The company adds operational and compliance complexity without earning a spread.

**Verdict: weak use case unless 24/7/cross-border/programmatic settlement matters.**

### Tokenized money-market fund

Potentially compelling when:

- the firm has material idle liquidity;
- the MMF yield materially exceeds its bank deposit economics;
- liquidity/redemption is sufficiently strong;
- operational overhead is automated;
- the company benefits from 24/7 collateral or treasury mobility.

The comparison should be **net yield**, not headline yield:

`Net benefit = MMF yield - bank alternative yield - fees - tax friction - accounting/compliance cost - operational risk premium`

### Tokenized bonds

Interesting mainly where tokenization materially improves access, settlement, fractionalisation or collateral use. It does not make a mediocre bond economically better merely because it is tokenized.

## 11. The product implication for Ophir

The strongest near-term concept may be narrower and better than 'crypto treasury'.

### Ophir = Treasury Compliance & Control Plane

Banking and accounting first:

1. connect Belgian/European bank accounts via Ponto/Isabel;
2. connect ERP/accounting;
3. create a normalized cash/asset ledger;
4. model liquidity and idle cash;
5. calculate available treasury alternatives;
6. classify each alternative legally/accountingly;
7. show expected **net** return after fees/tax/friction;
8. maintain audit evidence and accounting entries;
9. route approved execution to regulated partners;
10. reconcile the result automatically.

The killer screen may therefore not be a wallet screen. It may be:

> **You have €1.2m of excess cash for an expected 83 days.**
>
> Current bank return: X%
>
> Eligible regulated alternatives: A / B / C
>
> Expected net incremental return: €Y
>
> Liquidity: same-day / T+1 / 24×7
>
> Regulatory classification: Green
>
> Accounting treatment: pre-mapped
>
> Required approval: CFO + director

That is a CFO product, not a crypto product.

## 12. Current strategic answer

For Belgium in 2026:

- **Bank API access:** solvable via Isabel/Ponto; not a major moat by itself.
- **Stablecoin on/off ramps:** increasingly viable through regulated EU providers such as Circle, but still KYB/AML dependent.
- **Stablecoin return:** essentially zero for EURC itself; value is settlement/programming.
- **Tokenized MMFs:** increasingly interesting because they combine regulated yield-bearing instruments with on-chain mobility.
- **Liquidity:** tokenization improves operational/settlement liquidity more reliably than it improves market liquidity.
- **Regulatory overhead:** meaningful, but much of it can be externalized to licensed partners if Ophir stays the control/orchestration layer.
- **Accounting/tax:** real friction and probably one of Ophir's strongest opportunities for differentiation.

### Working thesis

**Ophir should not sell tokenization. Ophir should tell a CFO exactly when tokenization is economically superior, make the compliant decision legible, and automate all the ugly banking, legal, tax and accounting plumbing around it.**
