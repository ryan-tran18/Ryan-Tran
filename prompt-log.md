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

# Stage 3 Prompt Log Entry — Scenario 19 (`api-ingredients`)

**Date:** 2026-10-25

## Prompt used

> Build the Excel workbook specified by `capabilities/fx-hedging/spec.md` for Scenario 19 (`api-ingredients`). Include the cover page and data provenance, Legend/Key, all named ranges, formula-driven calculations, forward hedge, money-market hedge in three explicit steps, EUR put and call comparison with USD premium costs, a formula-driven ±5% sensitivity table in 1% increments with chart, and visible validation checks. Use input/assumption/formula/output color conventions. Do not hard-code calculated results. If the market inputs are inconsistent, expose the failed check and document it rather than forcing a pass.

## Review / fix iteration

- Added explicit money-market intermediate steps and named ranges.
- Added the 11-row formula-driven sensitivity table and chart.
- Added visible validation checks and a data provenance note.
- Audit found the forward parity check fails with current provisional spot and interest-rate inputs. The workbook flags this issue for Stage 4 market-data reconciliation rather than changing the inputs to manufacture a pass.
