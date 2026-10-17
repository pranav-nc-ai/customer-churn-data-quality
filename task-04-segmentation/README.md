# Task 04 — Segmentation and Recommendation Model

This folder contains a beginner-friendly, reproducible segmentation and rule-based churn-risk exercise using the supplied synthetic customer churn sample.

## Deliverables
- `notebooks/churn_segmentation_risk_model.ipynb` — feature rationale, transparent scoring rules, segmentation, data checks, edge-case tests, summary tables, and plots.
- `outputs/customer_segment_assignments.csv` — one row per customer with score components, total score, risk band, behavioral segment, explanation, and suggested action.
- `reports/recommendation_memo.md` — decision-focused memo with audience, supporting metrics, uncertainty, next measurement, and limitations.
- `data/cleaned_customer_churn.csv` — self-contained analysis input.

## Main findings
- Records: 15; churned: 7 (46.7%).
- Scoring features: contract type, tenure months, support-ticket count in the previous 90 days.
- Score is manually specified and transparent; it is not a probability and is not trained.
- The sample is synthetic and tiny, so observed churn rates are descriptive only.

## Run
Install `pandas`, `numpy`, and `matplotlib`, then open the notebook in Jupyter and run all cells. It regenerates the assignment CSV and summary tables.

## Important interpretation
Do not make causal claims or present same-sample separation as predictive accuracy. Validate any intervention on a larger, representative cohort using a predefined comparison and follow-up outcome.
