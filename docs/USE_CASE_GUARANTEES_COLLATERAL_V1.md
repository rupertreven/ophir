# Use Case — Construction Guarantees & Collateral v1

> **Date:** 2026-08-28 23:59 CEST  
> **Status:** Initial deep dive / `PUBLIC_SOURCE_RESEARCH` + economic hypotheses  
> **Vertical:** Belgian construction / infrastructure groups

## Executive conclusion

Guarantees and collateral are economically more promising than small cash-yield optimization, but the opportunity is **not yet proven as a universal €100k/year wedge** for a mid-sized Belgian contractor.

The strongest opportunity is likely a combination of:

1. visibility over all outstanding guarantees across banks/entities/projects;
2. eliminating guarantees that remain open after contractual need has ended;
3. comparing guarantee pricing and collateral requirements across providers;
4. forecasting guarantee capacity before tenders/projects;
5. identifying cash collateral that could potentially be replaced by unsecured/credit-line capacity or other eligible collateral;
6. preparing release/reduction requests at contractual milestones;
7. later, where banks support it, evaluating regulated digital/tokenized collateral that can remain yield-bearing.

Ophir does not issue guarantees, pledge assets or move collateral. It calculates and prepares decisions/actions for execution by the company and its bank/insurer.

## 1. Why construction is guarantee-heavy

Typical instruments include:

- bid/tender guarantees;
- performance guarantees;
- advance-payment guarantees;
- retention/release guarantees;
- warranty/maintenance guarantees;
- parent-company guarantees;
- letters of credit / standby structures in international projects.

Guarantees consume one or more scarce resources:

- guarantee line capacity;
- bank credit capacity;
- cash collateral;
- securities collateral;
- fees;
- administrative attention;
- covenant/headroom capacity.

The value is therefore not only the explicit guarantee fee. A stale €5m guarantee can prevent capacity from being used for a new project even if its annual fee looks modest.

## 2. Belgian public procurement context

Belgian public procurement law can require/permit performance security (`borgtocht` / cautionnement) under contract rules, with release linked to contractual performance/acceptance stages. Exact percentages and exemptions depend on procurement/contract type and applicable rules.

For Ophir, the product requirement is not to hard-code one universal percentage. Each guarantee must be linked to:

- contract;
- applicable procurement/private contract terms;
- guarantee type;
- amount/formula;
- issue date;
- expiry/release conditions;
- provisional/final acceptance milestones;
- beneficiary;
- provider;
- collateral/credit-line impact.

## 3. Economic model

### Direct fee leakage

Illustrative portfolio:

```text
Outstanding guarantees:             €25m
Average annual guarantee fee:       1.00% [illustrative]
Annual explicit fee:                €250k
```

If 10% of the portfolio is unnecessarily outstanding for an average extra six months because release is not chased promptly:

```text
Stale amount:                       €2.5m
Fee × 0.5 year × 1.00%:             €12.5k
```

That alone does **not** clear the €100k filter.

### Collateral opportunity cost

If €5m of guarantee exposure requires cash collateral and that cash earns 0.25% while an eligible alternative/corporate treasury return would be 2.0%, the spread is:

```text
€5m × (2.00% - 0.25%) = €87.5k/year
```

Add guarantee fees and operational leakage and the use case can approach/exceed €100k.

But actual collateralisation varies materially by corporate credit quality and bank agreement. Large strong contractors may use unsecured guarantee lines, so this cannot be assumed.

### Capacity value

Suppose a contractor has:

```text
Guarantee facility limit:            €30m
Outstanding:                          €28m
Apparently stale/releasable:          €4m
New tender requires:                  €5m
```

Releasing €4m can be strategically worth much more than the saved fee if it allows the company to tender/execute without negotiating emergency additional capacity.

This is difficult to convert to a deterministic annual ROI but may be the highest business value.

## 4. Ophir product

### Guarantee register

Normalize across banks/entities/projects:

```text
guarantee_id
legal_entity
project
customer/beneficiary
provider
instrument_type
currency
original_amount
current_amount
issue_date
contractual_expiry
actual_bank_expiry
release_conditions
provisional_acceptance_date
final_acceptance_date
fee_rate
fee_frequency
collateral_required
collateral_type
collateral_amount
facility_id
facility_limit
status
source_documents
```

### Intelligence outputs

Ophir can surface:

- guarantees past expected release milestone;
- bank expiry later than contractual requirement;
- guarantees whose amount should step down after milestones;
- duplicate guarantees;
- upcoming facility-capacity crunch;
- cost by bank/provider/entity/project;
- collateral opportunity cost;
- guarantees with missing release evidence;
- expected guarantee demand from project pipeline/tenders;
- provider repricing opportunity.

### Example

```text
Guarantee #BG-4812
Project: Hospital X
Amount: €2,400,000
Provider: Bank A
Fee: 1.10% p.a.
Provisional acceptance: 43 days ago
Contract rule: 50% reduction after provisional acceptance
Bank guarantee still: €2,400,000
Expected amount: €1,200,000

Potential annualised fee saving: €13,200
Facility capacity released: €1,200,000

Action package:
- contractual clause
- acceptance certificate
- proposed reduction amount
- bank release/reduction instructions
- responsible company approver

[Prepare request]
```

The customer sends/approves the actual request. Ophir does not alter the bank guarantee.

## 5. Data architecture fit

Existing Ophir architecture can support this with additional adapters/data sources:

```text
ERP / project system
contract documents
bank guarantee statements
bank APIs/files
accounting
          │
          ▼
Guarantee & Collateral Ledger
          │
          ├─ contractual milestone engine
          ├─ fee engine
          ├─ facility capacity forecast
          ├─ collateral opportunity-cost engine
          └─ release/reduction preparation
```

This fits the current normalized-ledger + rules + documents + human-approval architecture.

## 6. Tokenization relevance

### Today

The strongest current product does **not require tokenization**.

Digital guarantees/e-guarantees can improve issuance, authenticity and lifecycle handling, but the primary value is data/process/capacity intelligence.

### Emerging regulated collateral use case

Institutional markets are increasingly allowing tokenized regulated funds/securities to remain yield-bearing while being pledged/used as collateral. This can reduce the opportunity cost of idle collateral in certain institutional contexts.

For a Belgian construction company, however, the gating question is not whether tokenized collateral exists globally. It is:

> **Will the company's actual guarantee bank accept that instrument as collateral, at what haircut, under what legal pledge/control structure, and with what Belgian accounting/tax treatment?**

Until a Belgian/EU bank product supports this for corporate guarantee facilities, tokenized collateral remains a future extension rather than the MVP wedge.

## 7. Belgian legal/tax/accounting gate

### Legal

Need to model:
- underlying construction contract/public procurement rules;
- guarantee wording;
- release/reduction rights;
- bank facility agreement;
- pledge/collateral agreement;
- entity authority/approvals.

Ophir should identify contractual facts and prepare actions, not issue legal opinions automatically where interpretation is ambiguous.

### Tax

Guarantee fees and collateral investment income have ordinary corporate-tax/accounting effects, but exact treatment depends on instrument/entity. Tokenized collateral adds separate instrument tax analysis.

### Accounting

Need to distinguish:
- contingent/off-balance-sheet guarantee disclosures;
- cash collateral/restricted cash;
- pledged securities;
- guarantee fees/accruals;
- intercompany guarantees.

Professional validation required before automated journal treatment.

## 8. Existing solution risk

This is not an empty market. Banks, treasury-management systems and guarantee-management platforms already manage parts of the lifecycle.

Ophir needs a sharper wedge than 'digital guarantee register'. Candidate wedge:

> **contract/project-aware guarantee intelligence** — connect project milestones and contractual release rules directly to bank guarantee exposure, facility capacity and collateral cost.

That is especially construction-native.

## 9. €100K verdict

### Mid-sized contractor

Potential annual direct savings may often be below €100k unless:
- guarantee portfolio is large;
- collateralisation is material;
- fee rates are high;
- lifecycle management is poor.

### Large contractor/infrastructure group

Plausible €100k+ value where there are:
- tens/hundreds of millions in guarantees;
- multiple banks/entities/countries;
- material cash collateral;
- frequent milestone reductions;
- scarce guarantee facility capacity.

### Verdict

`SECONDARY / POSSIBLE VERTICAL WEDGE`, not yet a universal killer use case.

The best next validation is to obtain real portfolio statistics from 3–5 construction groups:

- total guarantees outstanding;
- number of guarantees;
- annual guarantee fees;
- collateral percentage;
- average delay between contractual releasability and actual release;
- number of banks/facilities;
- guarantee capacity constraints experienced in last 24 months.

If these show €100k+ preventable annual leakage/capital cost, promote to `PRIORITY`.

## 10. Next €100K sprint

Proceed to **debt + idle-cash optimization**, where the mathematics suggest €100k+ opportunities emerge at relatively modest balance-sheet scale (e.g. €20m debt × 50 bp).
