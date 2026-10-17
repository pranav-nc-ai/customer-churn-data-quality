# Customer Churn — Data Quality & Exploratory Analysis

Beginner-friendly internship task for the Data Analytics track.

## Objective
Audit and clean the supplied synthetic customer churn dataset, document data-quality decisions, and summarize initial patterns without making causal or predictive claims.

## Repository contents
- `data/raw/customer_churn_sample.csv` — supplied CSV, preserved as the raw input.
- `data/processed/cleaned_customer_churn.csv` — cleaned dataset export.
- `notebooks/churn_quality_eda.ipynb` — reproducible audit, validation checks, statistics, and charts.
- `reports/data_quality_report.md` — quality audit, cleaning decisions, results, recommendation, and limitations.
- `data_dictionary.md` — field definitions and source-alignment notes.
- `requirements.txt` — Python dependencies.

## Run locally
Python 3.10+ recommended.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/churn_quality_eda.ipynb
```

Run all cells. The notebook reads the raw CSV, profiles the data, validates assumptions, writes the cleaned CSV, and displays summary tables and charts.

## Initial findings
- 15 rows and 11 columns.
- 7 of 15 records are marked churned (46.7%).
- Average tenure is 7.0 months among churned records vs 29.1 among non-churned records.
- Average support tickets are 4.3 among churned records vs 1.0 among non-churned records.
- In this sample, the Month-to-Month group has 7/7 churned records; the One Year and Two Year groups each have 0/4.

These are patterns in a tiny synthetic sample, not reliable real-world estimates. The analysis is descriptive and does not prove causation or make predictions. See the report for limitations and a cautious follow-up recommendation.

## Important source note
The task guide uses names such as `customer_id`, `tenure_months`, `monthly_charge`, `support_tickets`, `contract_type`, and `churned`. The supplied CSV uses `CustomerID`, `TenureMonths`, `MonthlyCharges`, `SupportTickets`, `ContractType`, and `Churn`, and contains additional columns. This project keeps the actual supplied column names and documents the mismatch rather than silently renaming or recoding them.

## Data-quality decisions
The source has no missing cells, exact duplicate rows, duplicate IDs, negative counts/charges/tenure, broad age-range violations, charge-arithmetic mismatches beyond ₹0.01, or numeric IQR outliers. Cleaning is conservative: trim text whitespace, standardize selected category casing, validate the output, and do not silently drop rows.


## Business KPI Dashboard (Task 03)

The interactive dashboard source is in [`site/index.html`](site/index.html). It includes contract, tenure, and payment-method filters; churn and retention KPIs; monthly revenue exposure; average tenure; segment charts; a performance table; and filtered CSV export.

### Publish the dashboard online

GitHub Pages deployment workflow: [`.github/workflows/deploy-dashboard.yml`](.github/workflows/deploy-dashboard.yml).

**One-time setup required:** open **Settings → Pages** in this repository and select **GitHub Actions** as the build and deployment source. The connected automation can commit project files but cannot enable the repository's Pages setting on its own. After enabling Pages, rerun the failed **Deploy Business KPI Dashboard** workflow from the Actions tab (or push another change under `site/`).

When the workflow succeeds, the public dashboard URL should be:
**https://pranav-nc-ai.github.io/customer-churn-data-quality/**

### KPI definitions
- **Churn rate:** customers with `Churn = Yes` divided by all customers in the current filtered slice.
- **Retention rate:** customers with `Churn = No` divided by all customers in that slice.
- **Monthly revenue at risk (proxy):** sum of `MonthlyCharges` where `Churn = Yes`; this is historical exposure, not a forecast.
- **Average tenure:** mean of `TenureMonths` for the currently filtered group.

All dashboard figures are computed from 15 synthetic records. Interpret segment rates cautiously; the dashboard describes associations and does not establish causation.


## Task 04 — Segmentation and Recommendation Model

The Task 04 deliverables are in [task-04-segmentation/](task-04-segmentation/):

- [Reproducible segmentation and risk-score notebook](task-04-segmentation/notebooks/churn_segmentation_risk_model.ipynb)
- [Customer-by-customer scored segment table](task-04-segmentation/outputs/customer_segment_assignments.csv)
- [Recommendation memo](task-04-segmentation/reports/recommendation_memo.md)
- [Task 04 README and run instructions](task-04-segmentation/README.md)

The rule-based score uses contract type, tenure, and support tickets. It is a transparent triage heuristic, not a probability or validated prediction. The sample contains only 15 synthetic records; same-sample churn patterns must not be treated as evidence of generalization or causation.
