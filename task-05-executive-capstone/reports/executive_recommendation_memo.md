# Executive Recommendation Memo — Customer Churn

## Decision question
Which customer groups should a fictional subscription team contact first to investigate avoidable churn?

## Recommendation
Approve a small, human-reviewed, 30-day support pilot for **early-tenure customers with repeated recent support tickets**. Review ticket themes and resolution status, offer a service-first check-in, and compare subsequent churn and issue resolution with a pre-defined baseline before scaling.

## Five decision-relevant insights
1. **Observed churn:** 7 of 15 records are marked churned (46.7%).
2. **Contract pattern:** Month-to-Month is 7/7 churned (100%); One Year is 0/4 (0%); Two Year is 0/4 (0%). Group sizes are tiny.
3. **Tenure:** mean tenure is 7.0 months for churned records versus 29.1 months for those not marked churned.
4. **Support activity:** mean support tickets in the previous 90 days are 4.3 for churned records versus 1.0 for retained records.
5. **Historical charge exposure:** MonthlyCharges total ₹409.93 among records marked churned. This is not a forecast of recoverable revenue.

## Impact sensitivity
If a future comparable cohort hypothetically reduced the monthly charge exposure associated with churn by:
- 10%: ₹40.99 monthly charge-equivalent
- 25%: ₹102.48 monthly charge-equivalent
- 50%: ₹204.97 monthly charge-equivalent

**Assumption:** percentages are applied arithmetically to ₹409.93. The results are illustrative sensitivities, not expected savings or causal treatment estimates. They exclude outreach costs, gross margin, future customer mix, and uncertainty.

## 30-day pilot
- **Week 1:** define the cohort (tenure ≤12 months and ≥3 support tickets in prior 90 days), review ticket themes, and set success measures and comparison baseline.
- **Weeks 2–3:** a customer-success owner conducts helpful, human-reviewed check-ins; log attempted contact, response, issue theme, and resolution.
- **Week 4+:** compare subsequent churn, ticket resolution, customer feedback, and outreach cost against the pre-defined baseline/comparison.

## Limitations
The sample has 15 synthetic records. Results are not representative estimates, the contract groups are very small, and no contact history, satisfaction measures, intervention outcomes, renewal timing, or margin data are supplied. Associations do not prove causation. The analysis is descriptive; no prospective or holdout model validation has been performed.

## Next measurement
Use a larger representative cohort and report subsequent churn, issue resolution, contact success, cost, sample size, and uncertainty over a pre-specified follow-up period. Revise or stop the pilot if outcomes do not improve.
