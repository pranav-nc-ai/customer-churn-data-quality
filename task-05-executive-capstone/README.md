# Task 05 — Executive Analytics Capstone

This capstone distills the customer churn analysis into an executive decision brief.

## Live proof link
**Executive capstone page:** https://pranav-nc-ai.github.io/customer-churn-data-quality/task-05/

The page links to the executive PDF, editable PowerPoint, and a narrated presentation video once the build workflow completes. The broader project dashboard remains at https://pranav-nc-ai.github.io/customer-churn-data-quality/.

## Source and reproducibility
- Source CSV: data/customer_churn_sample.csv (15 synthetic customer records).
- Generator: generate_capstone.py. It validates data assumptions, computes the key metrics, produces an editable 8-slide PPTX, exports the matching PDF, and creates a narrated MP4 from the slides.
- The public downloadable assets are generated into site/task-05/ by the Build Task 05 workflow.

## Executive recommendation
Investigate **early-tenure customers with repeated recent support tickets** through a small, human-reviewed, 30-day service pilot. Define a comparison group and success measures before outreach; scale only if subsequent churn and issue resolution improve.

## Five insights
1. 7 of 15 records are marked churned (46.7%).
2. Month-to-Month is 7/7 churned; One Year and Two Year are each 0/4.
3. Average tenure is 7.0 months among churned records versus 29.1 months among records not marked churned.
4. Average support tickets in the previous 90 days are 4.3 vs 1.0.
5. Monthly charges associated with churned records sum to ₹409.93. This is a historical proxy, not a forecast.

## Impact and limitations
Hypothetical reductions of 10%, 25%, and 50% applied to that ₹409.93 proxy give about ₹40.99, ₹102.48, and ₹204.97 in monthly charge-equivalent sensitivity. These are not expected savings or a causal estimate. The sample is tiny and synthetic; group rates are unstable, and contact history, costs, and intervention outcomes are unavailable.

The MP4 uses synthetic narration. Use presentation_script.md to record your own voice if required by the reviewer.
