# Ophir Benchmarking Methodology

> **Updated:** 2026-08-28 23:58 CEST  
> **Status:** Active methodology  
> **Purpose:** Ensure treasury products are compared on a like-for-like basis.

## Core principle

Ophir must not compare products solely on yield. The primary benchmark must match the user's liquidity requirement.

> **Daily-liquid products should first be compared with daily-liquid alternatives. Fixed-term products should be compared separately as a liquidity-for-yield trade-off.**

For Belgian corporates, the preferred benchmark hierarchy is:

1. **actual customer bank quote / actual interest credited** on the connected account;
2. **Belgian corporate overnight-deposit market rate** from ECB/NBB monetary-interest-rate statistics;
3. public business savings-account rates;
4. term-deposit rates only as a separate locked-liquidity comparator.

This hierarchy avoids comparing an institutional/corporate MMF with a retail-like savings product when better market data exists.

## Benchmark buckets

### Bucket A — Immediate / daily liquidity
Examples:
- corporate overnight/current-account deposits;
- business savings/current-account products with immediate withdrawal;
- daily-liquid MMFs/FCPs;
- tokenized MMFs with same-day/daily redemption;
- stablecoin cash rails where economically appropriate.

Metrics:
- base/current yield;
- whether loyalty/fidelity bonuses require a minimum holding period;
- same-day/T+0/T+1 redemption;
- weekend availability;
- fees/taxes;
- capital/risk profile;
- deposit guarantee / fund investor protection;
- operational access.

### Bucket B — Fixed-term liquidity
Examples:
- 1/3/6/12-month corporate term deposits;
- fixed-maturity short-duration instruments;
- products with material exit penalties.

Metrics include contractual lock-up, breakage fees and early-withdrawal economics.

### Bucket C — Conditional liquidity
Examples:
- products that are daily dealing but not instant;
- notice accounts;
- funds with T+1/T+2 settlement;
- products with daily redemption caps.

These require explicit cash-availability timing rather than a binary 'liquid/not liquid' flag.

## Belgian corporate market benchmark

ECB monetary-interest-rate statistics provide a series specifically for **Belgian non-financial corporations' overnight deposits** (`MIR.M.BE.B.L21.A.R.A.2240.EUR.N`).

The latest value surfaced in the current public ECB data result during this research was **0.21% p.a. for March 2026**. Because the data page/search index can lag later releases, Ophir should fetch the latest available observation programmatically at calculation time rather than hard-code 0.21%.

This is conceptually a stronger primary benchmark than a named bank's public savings-account rate because it measures the average rate actually paid to Belgian non-financial corporations on overnight deposits.

### EUR 2m / 92-day illustration at 0.21%

```text
EUR 2,000,000 × 0.21% × 92/365 ≈ EUR 1,059 gross
Simple 25% CIT-equivalent proxy       ≈ EUR   794
```

If Carmignac Court Terme produced the backward-looking +0.40% 3-month fund performance used in the current dossier:

```text
Carmignac gross                       ≈ EUR 8,000
Carmignac 25% tax proxy               ≈ EUR 6,000
Corporate overnight gross             ≈ EUR 1,059
Corporate overnight tax proxy         ≈ EUR   794
Indicative uplift                     ≈ EUR 5,206 after simple tax proxy
```

This is much more informative than comparing Carmignac only with a 1.65% locked 3-month deposit.

The fund's exact Belgian transparent-tax treatment, TACT/custody implications and distributor fee remain unresolved; therefore this is not a certified net-benefit calculation.

## Current Belgian public daily-liquid bank examples — 28 Aug 2026

### Triodos Business Savings Account
- money available at any time;
- base rate: 0.30% p.a.;
- loyalty premium: 0.10% p.a. only after 12 consecutive months;
- for a 92-day treasury horizon, the economically relevant rate is therefore primarily the 0.30% base rate, not 0.40%.

### KBC Savings Account PRO
- open-ended business savings account;
- base rate: 0.35% p.a.;
- loyalty premium: 0.15% p.a.;
- loyalty component depends on holding conditions and should not be credited to a short-horizon scenario unless earned.

### BNP Paribas Fortis PRO Savings Account
- funds can be withdrawn to the customer's own BNP Paribas Fortis account;
- base rate: 0.30% p.a.;
- loyalty premium: 0.20% p.a.;
- short-horizon analysis should count only the component actually earned during the modeled holding period.

These public products remain useful sanity checks, but actual connected-account rates and the ECB/NBB corporate overnight series are preferred.

## Methodological correction to the EUR 2m / 92-day case

The 1.65% Triodos 3-month term deposit is a useful **fixed-term comparator**, but it is not the primary like-for-like comparator for a daily-liquid MMF/FCP.

For daily-liquid corporate cash, the relevant observed benchmark can be materially below 1%: the ECB Belgian corporate overnight series surfaced 0.21% for March 2026, while public business savings accounts currently show around 0.30–0.35% base interest.

Illustrative simple 92-day gross return on EUR 2m:

```text
0.21% p.a. Belgian corporate overnight average -> ~EUR 1,059
0.30% p.a. daily-liquid public bank baseline    -> ~EUR 1,512
0.35% p.a. daily-liquid public bank baseline    -> ~EUR 1,764
1.65% p.a. fixed 3-month term deposit           -> ~EUR 8,318
```

Therefore a daily-liquid MMF earning around 1.8–2.2% can generate materially more return than daily corporate bank cash while retaining substantially more liquidity than a term deposit.

The fair decision view is not one ranking but a frontier:

```text
Option                     Liquidity              Return
Corporate overnight        immediate              very low on current observed data
Daily bank savings         immediate              low
Daily/T+1 MMF              daily / T+0-T+1        higher, variable
3m term deposit            locked 92 days         higher, fixed
```

## Ophir product implication

Ophir should model a **liquidity-adjusted opportunity set** rather than a single yield leaderboard.

For each customer's cash bucket, determine:

1. required minimum liquidity;
2. maximum acceptable settlement delay;
3. probability/size of unexpected outflows;
4. minimum operating buffer;
5. amount genuinely lockable for a fixed term;
6. **actual effective yield currently earned by that cash**.

The sixth input is crucial. If the company already negotiates 1.8% on overnight cash, Ophir may find little financial alpha. If the company earns 0.1–0.3%, the opportunity can be large.

A company with EUR 2m 'free for three months' may still value daily access. Ophir should therefore calculate both:

- **return premium for keeping liquidity**, versus actual daily bank cash;
- **return sacrifice for keeping liquidity**, versus a locked term deposit.

## UI concept

```text
EUR 2,000,000 surplus cash — 92-day planning horizon

Actual account yield        0.18%       Immediate
Belgian corporate avg       0.xx%       Immediate
Daily MMF/FCP               1.xx%       Daily/T+1
3m term deposit             1.xx%       Locked

Ophir shows:
- incremental after-tax return versus the company's actual current position;
- liquidity gained/lost;
- break-even holding period;
- tax/accounting/admin implications.
```

## Rule

Never claim one instrument is 'better' without matching the company's liquidity constraint, risk constraint and tax/accounting treatment. Prefer actual account economics over generic advertised rates whenever connected data makes them available.
