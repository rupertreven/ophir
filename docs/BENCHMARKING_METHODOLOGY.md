# Ophir Benchmarking Methodology

> **Date:** 2026-08-28 23:50 CEST  
> **Status:** Active methodology  
> **Purpose:** Ensure treasury products are compared on a like-for-like basis.

## Core principle

Ophir must not compare products solely on yield. The primary benchmark must match the user's liquidity requirement.

> **Daily-liquid products should first be compared with daily-liquid alternatives. Fixed-term products should be compared separately as a liquidity-for-yield trade-off.**

## Benchmark buckets

### Bucket A — Immediate / daily liquidity
Examples:
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

## Methodological correction to the EUR 2m / 92-day case

The 1.65% Triodos 3-month term deposit is a useful **fixed-term comparator**, but it is not the primary like-for-like comparator for a daily-liquid MMF/FCP.

For daily-liquid cash, the primary public Belgian bank baseline is currently closer to 0.30–0.35% base interest before negotiated corporate cash rates, subject to provider-specific conditions.

This materially changes the apparent economic value of daily-liquid funds.

Illustrative simple 92-day gross return on EUR 2m:

```text
0.30% p.a. daily-liquid bank baseline  -> ~EUR 1,512
0.35% p.a. daily-liquid bank baseline  -> ~EUR 1,764
1.65% p.a. fixed 3-month term deposit  -> ~EUR 8,318
```

Therefore a daily-liquid MMF earning around 1.8–2.2% can generate materially more return than a daily-liquid savings account while preserving substantially more liquidity than the term deposit.

The fair decision view is not one ranking but a frontier:

```text
Option                     Liquidity              Return
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
5. amount genuinely lockable for a fixed term.

Only then compare eligible instruments.

A company with EUR 2m 'free for three months' may still value daily access. Ophir should therefore calculate both:

- **return premium for keeping liquidity**, versus daily bank cash;
- **return sacrifice for keeping liquidity**, versus a locked term deposit.

This is a core treasury trade-off and should be visible in the UI.

## UI concept

```text
EUR 2,000,000 surplus cash — 92-day planning horizon

Option                   Liquidity     Est. return      Liquidity premium/cost
Business savings         Immediate     ...              baseline
Daily MMF/FCP             Daily/T+1     ...              +EUR X vs liquid bank
3m term deposit           Locked        ...              +EUR Y vs liquid bank

Ophir note:
The term deposit pays more/less but removes access for 92 days.
The MMF retains daily liquidity but carries investment risk and tax/accounting considerations.
```

## Rule

Never claim one instrument is 'better' without matching the company's liquidity constraint, risk constraint and tax/accounting treatment.
