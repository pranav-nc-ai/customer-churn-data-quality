# Customer Churn — Data Quality & Exploratory Analysis

Beginner-friendly internship task for the Data Analytics track.

## Objective
Audit and clean the supplied synthetic customer churn dataset, document decisions, and describe initial patterns without making causal or predictive claims.

## Repository contents
- `data/raw/customer_churn_sample.csv` — original input, preserved unchanged.
- `data/processed/cleaned_customer_churn.csv` — cleaned CSV export.
- `notebooks/churn_quality_eda.ipynb` — reproducible audit and EDA notebook.
- `reports/data_quality_report.md` — findings, assumptions, limitations, and recommendation.
- `requirements.txt` — Python dependencies.
- `data_dictionary.md` — field definitions.

## Run locally
Python 3.10+ recommended.

```bash
python -m venv .venv
# Windows:
.venv\\Scripts\\activate
# macOS/Linux:
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/churn_quality_eda.ipynb
```

Run all notebook cells. The notebook checks quality rules, writes the processed CSV, and displays summary tables and charts.

## Key results
See `reports/data_quality_report.md` for the detailed quality audit and metrics. The dataset has only 15 synthetic records, so findings are illustrative, not representative. The analysis is descriptive and does not establish causation or produce predictions.

## Data handling
The raw file is retained. Cleaning is conservative: trim text whitespace, standardize selected category casing, validate key fields, and do not silently drop rows. No missing cells, duplicate rows/IDs, domain-invalid numeric values, arithmetic mismatches, or IQR outliers were identified by the documented checks.
