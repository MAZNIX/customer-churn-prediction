# Risk Register — Customer Churn Demonstration

| ID | Risk | Likelihood / impact | Safeguard | Evidence or follow-up |
|---|---|---|---|---|
| R1 | Tiny dataset produces unstable metrics | High / High | Label results illustrative; obtain more representative records | Current file has 12 rows |
| R2 | Customer ID leaks ordering or identity signals | Medium / Medium | Exclude `customer_id` from model features; restrict row-level sharing | 12 unique IDs |
| R3 | Feature values occur after churn/prediction time | Unknown / High | Define prediction cutoff and label horizon; audit timestamps | Timing metadata not supplied |
| R4 | Unknown source, consent, or licence | Unknown / High | Confirm provenance and permitted use with provider | Not documented in supplied CSV |
| R5 | False-positive churn flag leads to unwanted contact | Medium / Medium | Use optional, supportive outreach and human review | Agree costs with business owner |
| R6 | False negatives miss customers who need help | Medium / Medium | Keep standard support available; monitor missed cases | Review errors on larger validation data |
| R7 | Unequal performance across customer groups | Unknown / High | Assess lawful and appropriate subgroup metrics when data supports it | No subgroup data supplied |
| R8 | Predictions are misused for penalties or service denial | Low–Medium / High | Prohibit punitive use; require human review and documented purpose | Governance decision needed |
