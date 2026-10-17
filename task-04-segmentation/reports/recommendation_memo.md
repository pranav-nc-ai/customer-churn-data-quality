# Recommendation Memo — Customer Segmentation & Rule-Based Churn Risk

**Task:** 04 — Segmentation and Recommendation Model  
**Audience:** fictional subscription customer-success team  
**Dataset:** supplied synthetic sample, 15 records and 11 columns  
**Decision question:** Which customer groups should the team contact first to reduce avoidable churn?

## Executive recommendation

Prioritize a small, measured support-outreach pilot for **Early tenure + elevated support**. It contains **6 customers**, each with no more than 12 months of tenure and at least 3 support tickets. In this sample, 6 of these records are marked churned. This segment is a reasonable investigation priority because recent tenure and repeat support activity are actionable service signals. This is not evidence that those factors cause churn or that outreach will prevent it.

The score is a transparent, hand-set triage heuristic based on contract type, tenure, and support tickets. It is **not a probability, trained model, or validated forecast**. These 15 synthetic records are too few for reliable predictive-performance claims.

## Data scope and feature choices

The supplied CSV contains 15 records and fields for customer ID, gender, age, tenure, subscription type, monthly/total charges, contract, support-ticket count, payment method, and churn status. The source has 0 missing cells, 0 exact duplicate rows, and 0 duplicate customer IDs. The CSV contract labels are `Month-to-Month`, `One Year`, and `Two Year`; these are preserved rather than substituted with the task guide's different category words.

`CustomerID` is never a model feature. Gender and age are excluded because they are unnecessary for this service-triage rule and might create unfair or irrelevant prioritization. Monthly charges are used only to summarize the monthly charges associated with already-churned records, not as a risk driver. Payment method and subscription type are not given risk points because this tiny sample does not support defensible weights for them.

## Rule-based score definition

| Feature | Rule | Points |
|---|---|---:|
| Contract | Month-to-Month | 35 |
| Contract | One Year | 15 |
| Contract | Two Year | 5 |
| Tenure | 0–6 completed months | 25 |
| Tenure | 7–12 months | 18 |
| Tenure | 13–24 months | 8 |
| Tenure | 25+ months | 0 |
| Support tickets in prior 90 days | 5 or more | 25 |
| Support tickets in prior 90 days | 3–4 | 15 |
| Support tickets in prior 90 days | 1–2 | 5 |
| Support tickets in prior 90 days | 0 | 0 |

**Total score:** contract points + tenure points + support-ticket points; theoretical range **0–85**.

| Risk band | Score range | Suggested response |
|---|---:|---|
| High | 60–85 | Human-reviewed, proactive service check-in; verify account context first. |
| Medium | 35–59 | Targeted check-in or a reminder aligned to the customer's next decision point. |
| Low | 0–34 | Normal service and low-touch monitoring; do not assume zero risk. |

Weights and thresholds are policy choices for transparency, not coefficients learned from these 15 records. Review them with domain owners and calibrate only using a larger, representative dataset.

## Behavioral segments

Segments are mutually exclusive and assigned by this priority order using only contract, tenure, and tickets:

1. **Early tenure + elevated support:** tenure ≤12 months and ≥3 tickets. First group to consider for a support-oriented pilot.
2. **Month-to-month + continuing support signal:** Month-to-Month contract but not in segment 1. Offer a helpful pre-renewal check-in and understand the unresolved need before proposing a plan change.
3. **Established + low support demand:** tenure ≥13 months and ≤2 tickets. Use light-touch relationship maintenance and monitor as a comparison group.
4. **Mixed signals — monitor:** all other valid cases. Review the account manually before intervention.

### Observed results by risk band

| Risk band | Customers | Churned | Churn rate in sample | Monthly charges associated with churn |
|---|---:|---:|---:|---:|
| High | 6 | 6 | 100.0% | ₹329.94 |
| Medium | 1 | 1 | 100.0% | ₹79.99 |
| Low | 8 | 0 | 0.0% | ₹0.00 |

### Observed results by behavioral segment

| Segment | Customers | Churned | Observed churn rate | Avg tenure (months) | Avg support tickets | Monthly charges associated with churn |
|---|---:|---:|---:|---:|---:|---:|
| Established + low support demand | 8 | 0 | 0.0% | 29.1 | 1.0 | ₹0.00 |
| Early tenure + elevated support | 6 | 6 | 100.0% | 5.8 | 4.5 | ₹329.94 |
| Month-to-month + continuing support signal | 1 | 1 | 100.0% | 14.0 | 3.0 | ₹79.99 |

The overall sample contains **7 churned records (46.7%)**. The observed outcomes separate sharply by these account patterns. Same-sample rates must not be interpreted as out-of-sample accuracy: the rules are illustrative, and no independent/holdout validation was done. Churn labels are only used for post hoc descriptive checks, never as score inputs.

## Recommended next action and measurement

Run a time-limited, human-reviewed pilot for the early-tenure/elevated-ticket segment. Review ticket themes and resolution status, contact customers with a service-focused check-in, and log outreach plus outcomes. Define a comparable baseline or comparison cohort before interpreting effectiveness.

**Next measurement:** after a prespecified follow-up window, compare subsequent churn and ticket-resolution outcomes for contacted versus comparable non-contacted accounts, reporting sample size and uncertainty. Do not claim success based solely on this 15-row sample.

## Edge cases and controls

- Do not assign a numeric score if contract is missing or not one of the recognized CSV categories.
- Reject missing, negative, non-finite, or non-integer tenure and support-ticket counts.
- Validate score bounds 0–85 and risk-band cutoffs at 34/35 and 59/60.
- Keep a manual review path for invalid/incomplete records rather than silently assigning zero risk.
- Preserve every valid customer row and ID; do not silently remove records.

## Limitations

1. **Tiny synthetic sample:** 15 records are insufficient to estimate real population rates or validate a risk model.
2. **Selection/design bias:** synthetic data likely encode simplified relationships, potentially explaining the sharp pattern by contract and churn.
3. **No causal evidence:** associations do not prove that contract, tenure, or support tickets cause churn.
4. **No prospective validation:** score bands are summarized on the same records used to illustrate the rules, not an independent future cohort.
5. **Missing operational context:** ticket topic/severity, satisfaction, renewal date, outreach history, and post-contact outcomes are unavailable.

## Reproducibility

Run `notebooks/churn_segmentation_risk_model.ipynb` top to bottom. It reads `data/cleaned_customer_churn.csv`, applies the documented rule function, asserts the data and edge-case constraints, exports `outputs/customer_segment_assignments.csv`, and creates summary tables and plots.
