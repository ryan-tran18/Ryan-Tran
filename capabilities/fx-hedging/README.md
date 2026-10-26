University of Hawaiʻi at Mānoa · Shidler College of Business
FIN 321: International Finance and Securities
FX Transaction Hedging Project — Technical Specification

# API Ingredients — FX Transaction Hedge Model · Technical Specification

> Technical specification for the FX transaction hedge model — the named-range contract, calculation flow, and validation checks, precise enough that an AI or a colleague could build (or rebuild) the workbook from this document alone. This spec is the input the AI-assisted build works from.

| **Field** | **Value** |
|---|---|
| **Created by** | Ryan Tran |
| **Updated by** | Ryan Tran |
| **Date Created** | 2026-10-25 |
| **Date Updated** | 2026-10-25 |
| **Version** | 0.2 |
| **LLM Used** (optional) | ChatGPT (GPT-6) — assisted with drafting and refining the technical specification |
| **Role** | Treasury Analyst |
| **Audience** | CFO / Director of Treasury |
| **Companion Workbook** | student build — Scenario 19 (`api-ingredients`) |

---

## 1. Problem Statement

A U.S. manufacturer of active pharmaceutical ingredients has invoiced an Italian contract manufacturer in euros. The U.S. company expects to receive **€8,200,000 in 91 days**. Because its reporting currency is USD, a decline in EUR/USD would reduce the USD value of the receivable.

The model will compare four approaches:

1. No hedge.
2. Forward contract.
3. Money-market hedge.
4. EUR put option, with an EUR call option included as a comparison rather than assumed to be an effective downside hedge.

The objective is to estimate USD proceeds, compare outcomes under different settlement exchange rates, and identify the trade-offs between certainty, flexibility, and cost.

## 2. Inputs (Known Variables)

### 2.1 Scenario inputs

| Named range | Value | Classification |
|---|---:|---|
| `FC_AMT` | 8,200,000 | Known scenario input |
| `T_DAYS` | 91 | Known scenario input |
| `F0_in` | 1.1653 USD/EUR | Indicative forward quote |
| `PREM_PUT` | 0.0147 USD/EUR | Known scenario input |
| `PREM_CALL` | 0.0199 USD/EUR | Known scenario input |
| `S0_in` | 1.1193 USD/EUR | ECB reference-rate proxy, October 23, 2026 |
| `R_USD` | 4.04% annualized | Provisional U.S. 3-month Treasury-rate proxy |
| `R_FC` | 2.666% annualized | Provisional 3-month Euribor proxy |
| `K_PUT` | `=S0_in` | Strike at spot |
| `K_CALL` | `=S0_in` | Strike at spot |
| `BASIS` | 360 | Modeling convention; confirm against source conventions |

**Source notes**

- ECB reference exchange rates: https://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.eu.html
- U.S. Treasury/Federal Reserve rate data: https://www.federalreserve.gov/releases/h15/
- Euribor information: https://www.emmi-benchmarks.eu/euribor-org/euribor-rates.html

The ECB rate is a reference rate, not an executable dealing quote. The Treasury yield and Euribor are proxies, not necessarily the company's actual borrowing or deposit rates. Record the exact source observation, date, and convention in the workbook. Replace these proxies if the instructor requires executable bank quotes or a different rate convention.

## 3. Assumptions & Constraints

- The full receivable is collected at the end of day 91.
- The model uses annualized simple interest with `BASIS = 360` for its initial calculations.
- Option premiums are quoted in USD per EUR and paid at inception.
- Premiums are carried to maturity using the USD discount/growth factor for comparability.
- The forward quote is treated as indicative and available for modeling, not as a guaranteed executable quote.
- Transaction fees, credit spreads, collateral, bid-ask spreads, taxes, and counterparty limits are excluded unless separately entered.
- The money-market hedge assumes the company can borrow EUR and invest USD at the modeled rates. Actual bank borrowing and deposit rates may differ.
- A EUR put is the natural option hedge for a EUR receivable because it establishes a minimum conversion rate while retaining upside if EUR strengthens.
- A long EUR call does not, by itself, protect the downside of an existing EUR receivable. Show it as a comparison and do not label it the recommended protective hedge.
- The model's output is a decision aid, not an executable trade instruction.

## 4. Calculation Flow

### Step 1 — Interest factors

`DF_USD = 1 + R_USD * T_DAYS / BASIS`

`DF_FC = 1 + R_FC * T_DAYS / BASIS`

### Step 2 — No hedge

`USD_NO_HEDGE = FC_AMT * S_T`

At the base case, set `S_T = S0_in`.

### Step 3 — Forward hedge

`USD_FWD = FC_AMT * F0_in`

The forward outcome is fixed for the modeled maturity, assuming the quoted forward can be executed and the contract is held to settlement.

### Step 4 — Money-market hedge

For a foreign-currency receivable, borrow the present value of the EUR receivable, convert the borrowed EUR into USD at spot, and invest the USD until maturity.

`EUR_BORROW = FC_AMT / DF_FC`

`USD_MM = EUR_BORROW * S0_in * DF_USD`

Compare the money-market result with the forward result. Because the market quotes are indicative proxies and may use different conventions, a difference does not automatically indicate a formula error.

### Step 5 — EUR put option

`FV_PREM_PUT = -PREM_PUT * FC_AMT * DF_USD`

`USD_PUT = FC_AMT * MAX(S_T, K_PUT) + FV_PREM_PUT`

This models the EUR receivable protected by a put at the strike, less the premium's future value.

### Step 6 — EUR call comparison

`FV_PREM_CALL = -PREM_CALL * FC_AMT * DF_USD`

For a separately purchased EUR call held alongside the receivable:

`USD_CALL_COMPARISON = FC_AMT * S_T + FC_AMT * MAX(S_T - K_CALL, 0) + FV_PREM_CALL`

This shows the receivable's spot value plus the call payoff, less the premium's future value. It is an illustrative comparison, not a downside-protection strategy.

### Step 7 — Sensitivity grid

Create 11 settlement-rate scenarios from 95% to 105% of `S0_in`, in 1% increments:

`S_T_grid = S0_in * (1 + scenario_change)`

Calculate all strategy outcomes at each settlement rate. Keep full precision in formulas and round only displayed results.

## 5. Outputs

The workbook must display:

- Base-case USD proceeds under each strategy.
- USD differences versus the unhedged receivable.
- EUR put premium cost at inception and its modeled future value.
- Settlement-rate sensitivity table and comparison chart.
- A summary of the principal trade-off for each strategy.
- A warning where inputs are proxies or assumptions remain unverified.

### Initial reference calculations

| Output | Initial result |
|---|---:|
| Unhedged value at reference spot | $9,178,260 |
| Forward proceeds | $9,555,460 |
| Forward less unhedged reference value | $377,200 |
| EUR put premium paid at inception | $120,540 |
| Modeled future value of put premium | Approximately $121,771 |
| Money-market hedge | Approximately $9,209,924 |
| Put hedge at `S_T = S0_in` | Approximately $9,056,489 |
| Call comparison at `S_T = S0_in` | Approximately $9,013,414 |

These results use the provisional rates and a 360-day basis. They are illustrative model outputs, not confirmed transaction quotes. The forward calculation is `€8,200,000 × 1.1653 = $9,555,460`.

## 6. Model Review

Review the workbook after the first implementation and record at least one review-and-fix iteration in `prompt-log.md`.

### Review questions

- Are all inputs clearly separated from formulas?
- Are exchange-rate units consistently USD per EUR?
- Are premium costs negative and applied exactly once?
- Does the EUR put establish the intended minimum conversion rate?
- Is the EUR call clearly labeled as a comparison rather than a protective hedge?
- Are the money-market borrow/invest steps correct for a receivable?
- Do sensitivity outputs change as expected when `S_T` changes?
- Are proxy sources, observation dates, and conventions documented?
- Are calculations using named ranges instead of unexplained cell references?

### Validation checks

- `FC_AMT` must be positive.
- `T_DAYS` must be positive.
- Exchange rates and discount factors must be positive.
- Premiums must be nonnegative input values; their modeled cash-flow effect must be negative.
- At `S_T = K_PUT`, put proceeds should equal strike conversion value less the carried premium.
- Forward proceeds should not change across the settlement sensitivity grid.
- Check the money-market result against the forward rate implied by the selected spot and interest-rate assumptions. Investigate differences, but do not force equality when the input rates and conventions are not comparable.

## 7. Sensitivity Plan

Vary settlement EUR/USD from 95% to 105% of the reference spot rate in 1% increments. Compare:

- Unhedged proceeds.
- Forward proceeds.
- Money-market proceeds.
- EUR put proceeds.
- EUR call comparison proceeds.

The analysis should show that the unhedged receivable moves directly with spot; the forward locks the modeled rate; the put limits downside but incurs a premium; and the call comparison does not establish a minimum value for the receivable.

Also test alternative USD and EUR interest rates once more suitable borrowing/deposit rates are obtained.

## 8. Limitations & Next Steps

The model currently relies on an ECB reference spot rate and proxy interest rates. Before making a recommendation, verify:

1. The spot quote available to the company on the relevant valuation date.
2. Comparable 91-day USD and EUR borrowing/deposit rates, including their day-count conventions.
3. Whether the indicative forward quote is executable and what transaction costs apply.
4. The option contract's premium payment terms, expiry, and settlement conventions.
5. Whether counterparty credit limits or collateral requirements affect the available strategies.

The workbook should make uncertainty visible rather than presenting proxy-based calculations as exact market outcomes.

## 9. Workbook Design Requirements

Use the Stage 2 workbook architecture:

- **Cover:** scenario, purpose, model date, and status.
- **Legend/Key:** input, assumption, formula, and cross-sheet reference color conventions.
- **Inputs:** all scenario values, market data, sources, dates, and assumptions.
- **Hedge calculations:** separate calculations for unhedged, forward, money-market, and option strategies.
- **Sensitivity:** 11 settlement-rate scenarios and a comparison chart.
- **Notes & Assumptions:** source notes, model limitations, validation checks, and review history.

Color conventions:

- Yellow: user-entered inputs.
- Blue: assumptions or provisional values.
- Black: formulas.
- Green: cross-sheet links.

Use named ranges throughout the workbook. Keep source notes adjacent to the relevant inputs.

## 10. How This Sets Up Stages 3–5

- **Stage 3:** build the workbook from this specification and verify formulas, named ranges, and formatting.
- **Stage 4:** audit the model, test sensitivities, and correct any errors found during review.
- **Stage 5:** use the validated outputs to prepare the final recommendation, documenting limitations and the rationale for the chosen hedge.

### Appendix A — Change Log

| Version | Date | Change |
|---|---|---|
| 0.1 | 2026-10-25 | Initial Scenario 19 technical specification; market inputs left pending. |
| 0.2 | 2026-10-25 | Added reference spot and provisional interest-rate proxies, source notes, initial outputs, and clearer treatment of the EUR call comparison. Corrected forward proceeds to $9,555,460. |
