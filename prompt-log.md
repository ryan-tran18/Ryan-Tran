# Prompt Log

## 2026-09-27 — Portfolio Repository Setup

**What I asked:**  
How to complete the GitHub portfolio onboarding assignment and set up the required repository files.

**What was produced:**  
Created guidance and draft content for the portfolio README, resume, AI conventions, Claude instructions, Gitignore, and prompt log.

**What was wrong:**  
The initial setup needed to be aligned more closely with the instructor's required portfolio structure, including the personal AI skill and the canonical AGENTS.md setup.

**How it was caught:**  
Reviewed the course onboarding and portfolio repository instructions before committing the files.

## Stage 2 — FX Hedging Model Specification

**Scenario:** 19 — api-ingredients

**Work completed:**
- Developed the FX hedging model specification.
- Defined the required inputs, assumptions, and named ranges.
- Identified forward, money-market, put-option, and call-option hedge strategies.
- Established adverse, unchanged, and favorable exchange-rate scenarios.
- Defined formula requirements and validation checks.

**Draft gap identified:** The original specification needed clearer separation between the capability overview and the detailed model requirements.

**Correction made:** Moved the detailed specification into `capabilities/fx-hedging/spec.md` and replaced the README with a concise capability overview and engagement table.

**Next step:** Build and audit the Excel workbook using the specification.

# Stage 3 Prompt Log Entry — Scenario 19 (`api-ingredients`)

**Date:** 2026-10-25

## Prompt used

> Build the Excel workbook specified by `capabilities/fx-hedging/spec.md` for Scenario 19 (`api-ingredients`). Include the cover page and data provenance, Legend/Key, all named ranges, formula-driven calculations, forward hedge, money-market hedge in three explicit steps, EUR put and call comparison with USD premium costs, a formula-driven ±5% sensitivity table in 1% increments with chart, and visible validation checks. Use input/assumption/formula/output color conventions. Do not hard-code calculated results. If the market inputs are inconsistent, expose the failed check and document it rather than forcing a pass.

### Stage 4 – Market Data and CIP Analysis

AI assistance was used to identify and review market data sources for the Stage 4 FX hedging analysis. AI helped identify the ECB EUR/USD reference exchange rate and reference interest rate sources for the U.S. dollar and euro. It also assisted in selecting appropriate one-year interest rate proxies for the 91-day hedging period and explaining the assumptions and limitations of using these reference rates.

AI was also used to independently check the covered interest parity (CIP) calculation using the spot exchange rate, U.S. interest rate, euro interest rate, and 91/360 day-count convention. The calculated CIP-implied forward rate was approximately **1.10347 USD/EUR**. This was compared with the scenario forward rate of **1.1653 USD/EUR** to identify and document the difference.

All market data, assumptions, calculations, and AI-generated analysis were reviewed before being incorporated into the workbook. The scenario forward quote and assigned option premiums were retained as provided in the assignment.

## Review / fix iteration

- Added explicit money-market intermediate steps and named ranges.
- Added the 11-row formula-driven sensitivity table and chart.
- Added visible validation checks and a data provenance note.
- Audit found the forward parity check fails with current provisional spot and interest-rate inputs. The workbook flags this issue for Stage 4 market-data reconciliation rather than changing the inputs to manufacture a pass.
