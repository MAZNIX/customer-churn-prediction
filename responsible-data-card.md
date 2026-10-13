# Responsible Data Card — Customer Churn Training Dataset

## Dataset purpose
This dataset is intended for a small educational demonstration of customer churn classification. The target is `churned` (1 = churned, 0 = not churned). A possible decision supported by a future, validated model is which customers may benefit from a voluntary support or retention offer. The model must not automatically cancel service, deny service, change prices, or penalize customers.

## Provenance and permission
The supplied file is named `customer-churn-training.csv` and contains 12 records and 7 columns. The dataset creator, collection method, collection dates, consent status, and licence/usage restrictions are not specified in the supplied file or template. These details must be confirmed with the internship provider before any external or production use. Treat the data as training material only until permission and provenance are confirmed.

## Population and representation
The file contains 12 customer records. Plan types present are Basic, Standard, and Pro. The sample is very small and may not represent the provider's real customer population or churn patterns. No demographic or other subgroup information is supplied, so representation and subgroup fairness cannot be assessed from this file.

## Features and target
- `customer_id`: Identifier (12 unique values). Do not use as a predictive feature.
- `tenure_months`: Customer tenure in months.
- `support_tickets`: Number of support tickets.
- `monthly_spend_inr`: Monthly spending in Indian rupees.
- `last_login_days`: Days since the last login.
- `plan_type`: Plan category (Basic, Standard, Pro).
- `churned`: Target label; 1 means churned, 0 means not churned.

Potential leakage: Confirm that every feature was measured before the point at which a prediction would be made and that `churned` was assigned after the prediction window. `last_login_days` and `support_tickets` may be useful but must be time-aligned to avoid using information from after churn. `customer_id` may accidentally encode ordering or source-system information, so exclude it from model inputs. No explicit sensitive attributes are present, but plan type or spending could act as indirect proxies for customer circumstances.

## Quality checks
- Rows: 12; columns: 7.
- Missing values: none detected in the supplied CSV.
- Exact duplicate rows: none detected.
- Duplicate customer IDs: none detected (12 unique IDs).
- Target counts: 7 not churned (0), 5 churned (1), approximately 58.3% and 41.7%, respectively.
- Numeric values observed: `tenure_months` 1–30; `support_tickets` 0–5; `monthly_spend_inr` ₹499–₹1,499; `last_login_days` 1–30.
- The small sample means outlier checks and class-balance conclusions are limited. No train/test split should be interpreted as reliable evidence of real-world performance. Keep all records for exploratory work and clearly label any toy evaluation as illustrative.

## Risks and safeguards
1. **Small-sample risk:** Metrics may change drastically with one record. Obtain a larger, representative dataset before drawing conclusions.
2. **Privacy risk:** Customer IDs are identifiers. Exclude them from model features and avoid publishing row-level records.
3. **Bias/representation risk:** Subgroup representation is unknown. Check performance and error rates across relevant groups only when lawful, appropriate data is available.
4. **False positives:** A customer may be incorrectly flagged as likely to churn, leading to unwanted contact. Use supportive, optional outreach and monitor complaint rates.
5. **False negatives:** A customer at risk may not be identified. Do not rely solely on model predictions; retain normal customer-support channels.
6. **Data leakage:** Ensure all input features are available before the prediction date and remove post-outcome information.
7. **Misuse risk:** Do not use predictions to deny service, impose penalties, or make consequential decisions without human review.
8. **Provenance/consent uncertainty:** Confirm source, permission, and permitted purpose with the provider before reuse.

## Intended evaluation
- **Non-ML baseline:** Predict the majority class (`churned = 0`) for every record.
- **Model metrics:** Confusion matrix, precision, recall, F1-score, and balanced accuracy; report the positive class as `churned = 1`.
- **Calibration:** Do not make calibration claims with only 12 records. Reassess with a substantially larger validation set.
- **Fairness:** Not assessable from the supplied fields and sample size; document this limitation.
- **Error analysis:** Review false positives and false negatives, but do not interpret their rates as reliable population estimates.
- **Validation plan:** Obtain more data, split by time if dates become available, prevent leakage, and evaluate on a held-out set that was not used for model selection.
