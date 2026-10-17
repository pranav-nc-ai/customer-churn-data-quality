# Data Dictionary

The internship source guide explicitly defines the customer identifier, tenure, monthly charge, support tickets, contract type, and churn outcome. Descriptions for additional columns below are inferred from the supplied CSV values and should be confirmed with the data owner if reused elsewhere.

| CSV field | Description | Type / handling |
|---|---|---|
| `CustomerID` | Synthetic unique customer identifier; use to identify records, never as a numeric measure. Corresponds to guide field `customer_id`. | Text; expected unique and non-missing |
| `Gender` | Gender category in the synthetic sample. | Category |
| `Age` | Customer age in years, inferred from column name. | Numeric; check broad plausible range |
| `TenureMonths` | Completed months since signup. Corresponds to guide field `tenure_months`. | Integer-like numeric; non-negative |
| `SubscriptionType` | Subscription tier, e.g. Basic, Pro, Enterprise. | Category |
| `MonthlyCharges` | Fictional monthly amount in INR per the source guide. Corresponds to `monthly_charge`. | Numeric; non-negative |
| `TotalCharges` | Total recorded charges; inferred from column name. Arithmetic check compares it with monthly charges multiplied by tenure. | Numeric; non-negative |
| `ContractType` | Contract duration/category. The CSV values are Month-to-Month, One Year, and Two Year. Corresponds to guide field `contract_type`, although category wording differs. | Category; original labels preserved |
| `SupportTickets` | Support ticket count in the previous 90 days according to the source guide. Corresponds to `support_tickets`. | Count; non-negative |
| `PaymentMethod` | Payment method recorded for the customer. | Category |
| `Churn` | Whether the fictional customer left during the observation period. Corresponds to guide field `churned`; values are Yes/No. | Category / binary outcome |

## Source-alignment note
The guide uses snake_case names such as `customer_id` and `churned`, while the supplied file uses title-case names such as `CustomerID` and `Churn`. The analysis deliberately keeps the original CSV columns. `SubscriptionType`, `Gender`, `Age`, `TotalCharges`, and `PaymentMethod` are present in the CSV but are not defined in the guide excerpt, so their descriptions are inferred rather than authoritative.
