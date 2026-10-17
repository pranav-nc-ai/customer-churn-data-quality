# Task 05 — Executive Analytics Capstone

This capstone distills the supplied synthetic customer churn analysis into an executive decision brief.

## Live proof link
**Executive capstone page:** https://pranav-nc-ai.github.io/customer-churn-data-quality/task-05/

The public page links to the executive PDF, editable PowerPoint, and narrated MP4 generated during the GitHub Pages build. The prior interactive KPI dashboard remains at https://pranav-nc-ai.github.io/customer-churn-data-quality/.

## Deliverables
- `reports/executive_recommendation_memo.md` — five insights, recommendation, impact sensitivities, pilot, and limitations.
- `presentation_script.md` — narration script for an approximately three-minute executive briefing.
- `reports/limitations.md` — KPI definitions, assumptions, and evidence boundaries.
- `impact_scenarios.csv` — transparent sensitivity assumptions.
- `data/customer_churn_sample.csv` — supplied synthetic source data.
- `build.py` — reproducible builder for the eight-slide PPTX, matching PDF, and narrated video.

## Five key insights
1. 7 of 15 records are marked churned (46.7%).
2. Month-to-Month is 7/7 churned; One Year and Two Year are each 0/4.
3. Mean tenure is 7.0 months for churned records versus 29.1 months for records not marked churned.
4. Mean tickets in the previous 90 days are 4.3 versus 1.0.
5. Monthly charges associated with churned records total ₹409.93. This is a historical charge-exposure proxy, not a forecast.

## Recommendation
Run a small, human-reviewed, 30-day service pilot for early-tenure customers with repeated recent support tickets. Predefine a comparison group, success measures, and follow-up window before outreach; measure subsequent churn, issue resolution, feedback, and cost before deciding whether to scale.

## Impact sensitivities
Hypothetical 10%, 25%, and 50% reductions applied to the ₹409.93 proxy yield ₹40.99, ₹102.48, and ₹204.97 in monthly charge-equivalent sensitivity. These are not forecasts, causal estimates, or guaranteed savings.

## Limitations
The sample has only 15 synthetic records; group rates are unstable. The results do not establish causation or validate a predictive model, and contact history, intervention outcomes, customer satisfaction, margin, and outreach cost are unavailable. The MP4 uses synthetic narration; use the script to record your own voice if the reviewer requires a personal recording.
