**Task-4: Loan-default-risk-cost-optimization**<br>
A machine learning project that predicts loan default probability and optimizes the decision threshold using business cost analysis to minimize real-world financial losses.

**Task Objective:**<br>
Predict the likelihood of a loan default using the Home Credit Default Risk Dataset and optimize the classification threshold based on a cost-benefit framework — rather than standard accuracy metrics — to minimize total business loss from bad lending decisions.<br>

**Approach:**<br>
1. Data Cleaning & Preprocessing<br>

Loaded application_train.csv (~300k applicants, 120+ features)<br>
Dropped columns with more than 40% missing values<br>
Fixed known data anomaly: DAYS_EMPLOYED = 365243 is a sentinel value for "unemployed" — replaced with NaN and flagged separately<br>
Converted negative DAYS_* columns to absolute values for interpretability<br>
One-hot encoded low-cardinality categoricals; label encoded high-cardinality ones<br>
Imputed remaining nulls with column medians<br>
Used stratified train/validation/test splits to preserve the 8/92 class imbalance ratio<br>

2. Model Training
Logistic Regression (Baseline)<br>

Used StandardScaler to normalize features (required for LR)<br>
Set class_weight='balanced' to handle class imbalance<br>
Applied strong regularization (C=0.1) to prevent overfitting on wide data<br>

b)CatBoost (Main Model)
<br>
Trained 500 gradient boosted trees with learning_rate=0.05 and depth=6<br>
Set class_weights=[1, 10] to penalize missed defaults 10× more than false alarms<br>
Used early stopping on validation AUC to prevent overfitting (stopped at iteration 496)<br>

3. Business Cost Framework
Defined real-world costs for each type of prediction error:<br>
False Positive (FP)= Good customer wrongly denied a loan = $200 (lost interest revenue)<br>
False Negative (FN)= Defaulter wrongly approved for a loan = $2,000 (unrecovered loan loss)<br>
Swept all thresholds from 0.01 to 0.99 and selected the one minimizing:<br>
Total Cost = (FP count × $200) + (FN count × $2,000)<br>

5. Threshold Optimization<br>
<br>
Default threshold (0.50) was compared against the optimal threshold found by the cost sweep
Optimal threshold found at 0.47 — slightly lower than default, aggressively catching more defaulters given the 10× cost asymmetry<br>

**Results & Findings:**<br>
Model Performance
| Model | AUC-ROC | Improvement |
|-------|---------|-------------|
| Logistic Regression | 0.7389 | — |
| **CatBoost** | **0.7567** | **+0.0178** |
<br>
CatBoost improved AUC by +0.0178 over the baseline — confirming that non-linear interactions between features (e.g. high debt ratio is only risky when income is also low) exist in the data and are captured by gradient boosting.<br>
<br>
Final Test Set Evaluation (at Optimal Threshold 0.47)<br>
| Metric | Value | Interpretation |
|--------|-------|----------------|
| AUC-ROC | 0.7567 | Ranks defaulters above non-defaulters 75.67% of the time |
| PR-AUC | 0.2427 | Expected low for 8/92 imbalanced dataset |
| Precision (Default) | 0.17 | 1 in 6 flagged loans is an actual default |
| Recall (Default) | 0.66 | Catches 66% of all real defaulters |
| Accuracy | 0.71 | Misleading metric — ignore due to class imbalance |

Confusion Matrix:<br>
| | Predicted: No Default | Predicted: Default |
|--|----------------------|--------------------|
| **Actual: No Default** | 40,403  True Negative | 16,135  False Positive |
| **Actual: Default** | 1,668  False Negative | 3,297  True Positive |

The model catches 66% of all real defaulters while maintaining a manageable false alarm rate. Low precision (0.17) is expected and acceptable — in this domain, missing a defaulter costs 10× more than wrongly flagging a good customer.<br>

**Business Cost Summary**<br>
| Threshold | Total Cost | vs Default |
|-----------|------------|------------|
| Default (0.50) | $6,573,600 | — |
| **Optimal (0.47)** | **$6,563,000** | **-$10,600** |
| **Savings** | **$10,600** | **0.16% reduction** |

The saving appears modest because the optimal threshold was already close to 0.50. At production scale (millions of loans annually), the same optimization yields proportionally larger savings.<br>

**Top 10 Most Predictive Features**<br>
| Rank | Feature | Importance | What It Captures |
|------|---------|------------|-----------------|
| 1 | EXT_SOURCE_3 | 14.24% | External credit bureau score 3 |
| 2 | EXT_SOURCE_2 | 12.68% | External credit bureau score 2 |
| 3 | AMT_CREDIT | 6.55% | Total loan amount |
| 4 | AMT_GOODS_PRICE | 5.89% | Price of goods the loan finances |
| 5 | DAYS_BIRTH | 5.84% | Applicant age |
| 6 | AMT_ANNUITY | 4.82% | Monthly repayment amount |
| 7 | DAYS_EMPLOYED | 4.20% | Length of current employment |
| 8 | DAYS_LAST_PHONE_CHANGE | 3.02% | Stability indicator |
| 9 | CODE_GENDER_M | 2.96% | Gender |
| 10 | DAYS_ID_PUBLISH | 2.89% | Days since ID was reissued |
<br>
EXT_SOURCE_2 and EXT_SOURCE_3 together account for ~27% of all predictive power — external credit bureau scores are far more valuable than any internal bank feature. Applicants with no bureau history significantly reduce model confidence.<br>

**Key Takeaway:**<br>
The default threshold of 0.50 is almost never optimal for business problems. The correct threshold depends entirely on the asymmetry of costs in the domain. In loan default prediction, where a missed defaulter costs 10× more than a false alarm, the optimal threshold shifts lower — catching more defaulters at the expense of occasionally denying good customers.
