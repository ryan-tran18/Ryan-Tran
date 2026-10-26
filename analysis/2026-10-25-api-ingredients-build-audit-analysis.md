# Stage 3 Build Audit — Scenario 19 (`api-ingredients`)

- **Date:** 2026-10-25
- **Workbook:** `capabilities/fx-hedging/model.xlsx`
- **Specification:** `capabilities/fx-hedging/spec.md`
- **Build method:** AI-assisted workbook generation; formulas and named ranges inspected programmatically after generation.
- **Audit status:** Structural checks passed; market parity check is expected to fail with current provisional inputs and requires resolution in Stage 4.

## Findings

### 1. Named-range contract and formulas

- **Checked:** Workbook named ranges and the main calculation cells.
- **Found:** The workbook includes named ranges for `FC_AMT`, `S0_in`, `F0_in`, `R_USD`, `R_FC`, `T_DAYS`, `BASIS`, `K_PUT`, `K_CALL`, `PREM_PUT`, and `PREM_CALL`, plus `STEP_FRAC`, `BASIS_USD`, `BASIS_FC`, and money-market intermediate names. Core calculation cells are formulas rather than pasted result values.
- **Action:** Named ranges are defined against the intended input cells or formula intermediate cells. Excel recalculation on open is enabled.
- **Remaining check:** Open in Excel and use Formulas → Name Manager to visually confirm the names and change an input to test recalculation.

### 2. Forward proceeds arithmetic

- **Checked:** Forward proceeds formula and units.
- **Found:** The formula uses `=FC_AMT*F0_in`, with EUR amount multiplied by USD per EUR.
- **Action:** The workbook uses formula-driven proceeds. The correct arithmetic is €8,200,000 × 1.1653 = **$9,555,460** (before costs).

### 3. Money-market hedge sequence

- **Checked:** Whether the model shows the required three explicit steps.
- **Found:** The workbook separately calculates (1) EUR borrowing equal to the present value of the receivable, (2) conversion of borrowed EUR at spot, and (3) investment of USD to maturity.
- **Action:** Each step is formula-driven and uses named ranges, with intermediate values visible.

### 4. Sensitivity table and chart

- **Checked:** Number of scenarios, formula structure, and chart data range.
- **Found:** The table contains 11 settlement scenarios from -5% to +5% in 1% steps, with settlement rates and strategy outcomes calculated by formulas. A line chart is tied to the sensitivity table.
- **Action:** The settlement rows are formula-driven rather than manually entered outcome values.

### 5. Parity check — unresolved data inconsistency

- **Checked:** Forward quote versus the theoretical forward implied by the selected spot and proxy interest rates.
- **Found:** Using spot 1.1193, USD proxy rate 4.04%, EUR proxy rate 2.666%, 91 days, and a 360-day simple-interest convention, the implied forward is approximately **1.1232 USD/EUR**. The supplied indicative forward is **1.1653**, so the relative discrepancy is approximately **3.75%**, far above the 0.05% tolerance.
- **Action:** The workbook exposes the parity check and flags it as a failure instead of forcing a pass. The likely issue is that the spot/rate proxies do not match the date, instrument, maturity, or conventions behind the scenario's forward quote.
- **Next step:** In Stage 4, validate comparable-date spot, forward, and borrowing/deposit rates. Do not make a final hedge recommendation until the discrepancy is understood.

### 6. Option payoff interpretation

- **Checked:** Premium sign and option role for a EUR receivable.
- **Found:** The EUR put payoff is modeled as the greater of settlement spot and strike, less the future value of the premium. The call overlay is shown separately as the spot value of the receivable plus the EUR call payoff, less premium; it does not establish a downside floor.
- **Action:** The workbook labels the call as an upside overlay/comparison and carries both option premiums as costs.

## Summary

The workbook has the requested tab structure, named ranges, formulas, three-step money-market hedge, option calculations, sensitivity table/chart, and visible validation checks. **The parity validation does not pass with the current provisional market inputs.** This is a substantive audit finding, not a cosmetic issue. Resolve it with validated market data and document the correction before treating the workbook as final.
