# Data Quality Report — Customer Churn

## Objective and decision question
Audit and clean the supplied synthetic customer churn dataset, document reproducible quality checks, and inspect initial patterns. The task-guide decision question is: **Which customer groups should a fictional subscription team contact first to investigate avoidable churn?**

## Dataset scope
- Source: `data/raw/customer_churn_sample.csv`
- Size: **15 rows × 11 columns**
- Outcome field in the uploaded CSV: `Churn` (`Yes`/`No`)
- The dataset is synthetic. With only 15 records, subgroup percentages are unstable and should not be generalized to real customers.

### Note on source-field naming
The task guide names fields `customer_id`, `tenure_months`, `monthly_charge`, `support_tickets`, `contract_type`, and `churned`. The supplied CSV instead uses `CustomerID`, `TenureMonths`, `MonthlyCharges`, `SupportTickets`, `ContractType`, and `Churn`, plus additional fields. This analysis uses the supplied CSV's actual column names and keeps them unchanged. The supplied contract categories are `Month-to-Month`, `One Year`, and `Two Year`; they are not silently recoded to the guide's Monthly/quarterly/annual wording.

## Quality audit

| Check | Result | Decision |
|---|---:|---|
| Missing cells | 0 | No imputation required. |
| Exact duplicate rows | 0 | No rows removed. |
| Duplicate customer IDs | 0 | Identifier uniqueness check passes. |
| Age outside broad 0–120 validation range | 0 | No invalid age detected by this rule. |
| Negative tenure | 0 | No invalid tenure detected. |
| Negative monthly or total charges | 0 | No negative charges detected. |
| Negative support-ticket counts | 0 | No invalid counts detected. |
| `TotalCharges` differs from `MonthlyCharges × TenureMonths` by more than ₹0.01 | 0 | Charge arithmetic is consistent for all rows. |
| IQR outlier flags: Age | 0 | No observations flagged by the 1.5×IQR rule. |
| IQR outlier flags: TenureMonths | 0 | No observations flagged by the 1.5×IQR rule. |
| IQR outlier flags: MonthlyCharges | 0 | No observations flagged by the 1.5×IQR rule. |
| IQR outlier flags: TotalCharges | 0 | No observations flagged by the 1.5×IQR rule. |
| IQR outlier flags: SupportTickets | 0 | No observations flagged by the 1.5×IQR rule. |

IQR is a screening heuristic, not a proof that every value is valid; outlier flags are not grounds for automatic deletion.

## Cleaning decisions
1. Preserve the original CSV under `data/raw/`.
2. Trim leading/trailing whitespace from text values.
3. Standardize simple category casing for `Gender`, `SubscriptionType`, and `Churn`; keep the supplied contract labels as they appear.
4. Validate non-null unique customer IDs, allowed churn labels, plausible age bounds, and non-negative tenure, charges, and support-ticket counts.
5. Compare `TotalCharges` with `MonthlyCharges × TenureMonths`, allowing ₹0.01 for rounding.
6. Retain all **15** rows. No missing values, duplicates, impossible values under the documented rules, or IQR flags were found, so no records are dropped and no values are imputed.

## Initial descriptive findings
- **Observed churn rate:** **46.7%** (7 of 15 records).
- **Average tenure:** **7.0 months** for churned customers vs **29.1 months** for non-churned customers.
- **Average support tickets:** **4.3** for churned customers vs **1.0** for non-churned customers.
- **Average monthly charges:** **₹58.56** for churned customers vs **₹107.49** for non-churned customers.
- **Contract group rates:** Month-to-Month **100%** (7 of 7); One Year **0%** (0 of 4); Two Year **0%** (0 of 4).

These rates describe this tiny sample only. The all-churn result for Month-to-Month contracts may reflect how the synthetic sample was constructed and is not a reliable estimate of real-world churn risk.

## Recommendation
A cautious follow-up investigation could review **recent-tenure, month-to-month customers with multiple support tickets** to learn whether proactive support might help. This is a hypothesis for a measured pilot, not a conclusion that the group will churn or that outreach will prevent it.

- **Audience:** customers on month-to-month contracts with shorter tenure and recent support activity.
- **Decision:** test whether a structured support follow-up is worth piloting.
- **Supporting metrics:** 46.7% overall sample churn; mean tenure 7.0 vs 29.1 months; mean tickets 4.3 vs 1.0; month-to-month churn 7/7 in this sample.
- **Uncertainty:** only 15 synthetic records; segment rates are highly unstable. Descriptive association does not show causation.
- **Next measurement:** evaluate a larger, representative cohort; define an appropriate baseline/comparison group and measure subsequent churn and support-contact outcomes.

## Limitations
- A single record changes the sample percentage materially.
- Synthetic data may encode intentionally simple relationships that do not appear in real customer populations.
- No outreach/intervention outcomes, customer satisfaction measure, or longitudinal event history is provided.
- This work is descriptive EDA, not a prediction model; it does not prove that contract type or support tickets cause churn.

## Reproducibility
Open `notebooks/churn_quality_eda.ipynb` and run the cells. The notebook loads the preserved raw CSV, profiles quality, runs validation assertions, exports `data/processed/cleaned_customer_churn.csv`, prints summaries, and draws charts.
