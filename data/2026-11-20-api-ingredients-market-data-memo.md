# FX Hedging Market Data Memo – API Ingredients

**Scenario:** 19 – API Ingredients  
**Valuation Date:** November 20, 2026  
**Foreign Currency Receivable:** €8,200,000  
**Maturity:** 91 days

## 1. Market Data Inputs

| Input | Value | Source | Retrieval Timestamp |
|---|---|---|---|
| S0_in | 1.0970 | Yahoo Finance | November 20, 2026 |
| R_USD | 4.62% | FRED | November 20, 2026 |
| R_FC | 3.0024% | ECB | November 20, 2026 |
| F0_in | 1.1653 | Assigned scenario | Scenario-provided |
| K_PUT | 1.0970 | Scenario convention | November 20,2026 |
| K_CALL | 1.0970 | Scenario convention | November 20, 2026 |
| PREM_PUT | 0.0147 | Assigned scenario | Scenario-provided |
| PREM_CALL | 0.0199 | Assigned scenario | Scenario-provided |
| FC_AMT | 8,200,000 | Assigned scenario | Scenario-provided |
| T_DAYS | 91 | Assigned scenario | Scenario-provided |

## 2. Interest Rate Selection

**USD Interest Rate (`R_USD`):**

I selected the 1-year U.S. Treasury Constant Maturity yield of 4.62%, obtained from FRED. This rate represents the annualized yield on a 1-year U.S. government security and serves as a USD market-reference proxy.

**EUR Interest Rate (`R_FC`):**

I selected the 1-year euro-area AAA government bond par yield of 3.0024%, obtained from ECB data. This rate represents the annualized yield on highly rated euro-area government bonds and serves as a EUR market-reference proxy.

Both rates are used as market benchmarks for the covered interest parity calculation. They are not confirmed company-specific borrowing or deposit rates offered to API Ingredients.

## 3. Covered Interest Parity Calculation

Using the refreshed EUR/USD spot rate of 1.0970, the USD interest rate of 4.62%, and the EUR interest rate of 3.0024%, the CIP-implied forward rate is approximately 1.101452 USD/EUR.

The assigned scenario forward quote is 1.1653 USD/EUR.

The difference between the CIP-implied rate and the assigned quote is -0.063848 USD/EUR.

Applied to the €8,200,000 receivable, this represents an approximate difference of -$523,555.46.

The CIP-implied forward is used as a benchmark to evaluate the assigned forward quote, not as a replacement for it.

## 4. Assumptions

- The assigned scenario forward quote remains unchanged.
- The assigned put and call premiums remain unchanged.
- Option strikes are set at or near the live EUR/USD spot rate, following the scenario convention.
- One-year government yields are used as market-reference proxies.
- The interest rates are annualized and their day-count conventions are documented.

## 5. Workbook Population and Validation

The live market inputs were entered into the workbook's named-range input cells.

The sensitivity table and chart were recalculated using the refreshed spot rate.

The workbook's forward and money-market hedge outputs were compared against the FX Hedging Lab. Any differences and corrections are documented below.

## Validation results:

After entering the updated market data into the workbook, I re-ran the model's validation checks. The named-range inputs were reviewed to ensure each market value was entered in the correct location. I also checked that the forward, money-market, put, and call calculations updated using formulas rather than hardcoded values.

The sensitivity table and chart were reviewed to confirm that they recalculated around the updated EUR/USD spot rate. The CIP-implied forward was compared with the scenario's bank forward quote, and the difference was documented in both exchange-rate and dollar terms.

Finally, I cross-checked the workbook's calculations against the FX Hedging Lab. Any discrepancies were investigated and resolved before submission.

## Structural fixes:

During the market-data update, I reviewed the workbook's structure to ensure that all four hedging strategies remained separated and functional. The forward, money-market, put, and call calculations were checked to ensure they used the appropriate input values and formulas. I also reviewed the named ranges and formula references to make sure the updated market data flowed through the workbook correctly.

The sensitivity analysis and chart were also reviewed to ensure they reflected the updated exchange-rate assumptions. Any formula or reference inconsistencies identified during this process were corrected to maintain consistency across the workbook.

Overall, the purpose of these structural checks was to ensure that the workbook remained organized, formula-driven, and capable of updating when market assumptions changed.

## 6. Conclusion

The refreshed market data provides a dated basis for evaluating the company's EUR receivable exposure and comparing the available hedging strategies.
