# ML Problem-Framing Memo — Customer Churn

## 1. Problem statement
Explore whether basic account-usage information can help identify customers labelled as churned in the supplied educational dataset. The current file has only 12 rows, so this is a learning exercise, not a production-ready prediction system.

## 2. Decision and intended action
Potential future use: offer voluntary support or retention assistance to customers who may be at risk. The prediction should support a human decision, not automatically trigger penalties, price changes, or service restrictions.

## 3. Prediction target
`churned`: 1 = churned; 0 = not churned.

## 4. Unit of observation
One row per customer (`customer_id` is unique in the supplied file).

## 5. Prediction time and action window
The supplied file does not state a prediction timestamp, churn definition, or action window. Before model training for a real use case, define a cutoff date (when features are known) and a future horizon (for example, whether churn occurs in a specified future period). Confirm these definitions with the dataset provider; do not assume the current labels support a particular horizon.

## 6. Candidate input features
- `tenure_months`
- `support_tickets`
- `monthly_spend_inr`
- `last_login_days`
- `plan_type`

Exclude `customer_id` from the model inputs. Confirm all candidate features were recorded before the prediction cutoff.

## 7. Non-ML baseline
Always predict the majority class, `churned = 0`. In this dataset that would label all 12 rows as not churned and achieve 7/12 (58.3%) accuracy on these same rows. This is a descriptive baseline only, not a valid held-out evaluation.

## 8. Success measures
Report the confusion matrix, precision, recall, F1-score, and balanced accuracy, treating `churned = 1` as the positive class. Business success should eventually be measured by whether a voluntary retention intervention helps customers and is cost-effective, not by model accuracy alone. Costs of false positives and false negatives must be agreed with the business owner.

## 9. Main limitations and risks
- Only 12 records; results are highly unstable.
- Data source, consent/licence, time period, and churn definition are not supplied.
- Potential temporal leakage if activity fields were recorded after the churn event.
- No subgroup information for fairness evaluation.
- False positives can cause unwanted outreach; false negatives can miss customers needing help.

## 10. Recommendation
Complete exploratory checks and a clearly labelled baseline notebook for the internship deliverable. Do not deploy or make operational claims. Request a larger, representative, permission-cleared dataset and a precise prediction horizon before any real-world evaluation.
