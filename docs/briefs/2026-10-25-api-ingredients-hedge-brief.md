---
type: brief
engagement: api-ingredients
capability: fx-hedging
date: 2026-10-25
status: committed
hypothesis: "I expect the forward hedge to provide the most predictable USD proceeds, while the EUR put may justify its $120,540 premium if retaining upside is valuable."
---

# FX Hedging Executive Brief — API Ingredients

**Created by:** Ryan Tran  
**Updated by:** Ryan Tran  
**Date Created:** October 25, 2026  
**Date Updated:** October 25, 2026  
**Version:** 1.1  
**LLM Used:** GPT-6 (OpenAI)

## Executive Summary

A U.S. active pharmaceutical ingredient manufacturer expects to receive €8,200,000 from an Italian contract manufacturer in 91 days. If the euro weakens before payment, converting the receivable into dollars will generate less USD revenue. This brief frames the exposure and compares forward, money-market, and options hedges. At the indicative forward rate of $1.1653 per euro, the company could lock in approximately $9,557,460 before costs. The analysis will compare certainty, downside protection, premiums, financing requirements, and potential upside. No final hedge recommendation will be made until the model and market inputs are verified.

## Background & Objectives

The company has a fixed euro receivable but uncertain dollar proceeds. A 5% decline from the indicative forward-rate benchmark would reduce the equivalent proceeds by approximately $477,873, from $9,557,460 to $9,079,587. This is an illustrative stress test, not a forecast or a calculation from a verified spot quote.

The objective is to identify how each hedge affects expected USD proceeds and downside risk. The analysis will also consider cash-flow predictability, opportunity cost, and implementation constraints.

## Methods

Three hedge families will be compared:

- **Forward/futures hedge:** Agree to sell euros at a predetermined rate. **Pro:** Locks in a predictable conversion value. **Con:** Sacrifices gains if the euro strengthens; futures may also involve margin requirements.
- **Money-market hedge:** Borrow euros against the future receivable, convert the borrowed euros at spot, and invest the resulting dollars until settlement. **Pro:** Can establish predictable USD proceeds using borrowing and investment rates. **Con:** Uses financing capacity and depends on available rates and transaction costs.
- **Options hedge:** Buy a EUR put with a strike at the verified spot rate, providing the right to sell euros at that strike. **Pro:** Protects against euro weakness while retaining upside if the euro strengthens. **Con:** The premium is payable regardless of whether the option is exercised. At $0.0147 per euro, the put premium totals $120,540. The supplied EUR call premium is $0.0199 per euro, or $163,180, but a call on euros is generally less directly suited to hedging a euro receivable.

The model will use a verified spot quote, comparable 91-day USD and EUR interest rates, and documented assumptions. It will compare net dollar proceeds under adverse, unchanged, and favorable exchange-rate scenarios.

## Assumptions

The receivable is collected in full in 91 days; the stated forward rate and option premiums are indicative; and transaction costs, credit risk, and financing constraints remain unverified. The spot quote and interest rates must be sourced and dated before final calculations.

## Hypothesis

I expect the forward hedge to provide the most predictable USD proceeds because it fixes the conversion rate. The EUR put may be preferable if retaining upside is worth its $120,540 premium.

## How I Would Know I Was Wrong

The hypothesis would be challenged if verified model results show that the money-market hedge produces better net proceeds at comparable risk, or that the put's downside protection and retained upside justify its premium more effectively than the forward.

## Limitations & Next Steps

Ryan Tran will complete the analysis in stages: **Stage 2** will specify the model, inputs, formulas, and validation checks; **Stage 3** will build and audit the workbook; **Stage 4** will populate it with sourced, timestamped market data; and **Stage 5** will independently validate the results and prepare the final decision memo. The recommendation will follow the evidence rather than precede it.

## References

Stauffer, A. W. (2026). *Stage 1 — Executive Brief: FX Hedging*. https://adamwstauffer.github.io/ai-lms/fx-hedging-stage1.html

Stauffer, A. W. (2026). *Deliverable Templates*. https://adamwstauffer.github.io/ai-lms/deliverable-templates.html
