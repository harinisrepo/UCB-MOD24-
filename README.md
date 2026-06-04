# UCB-MOD24-
Final Capstone project: Semiconductor Failure Prediction for Automotive Reliability
🚗 Semiconductor Failure Prediction for Automotive Reliability
Harini Tadinada

✅ Executive Summary
✅ Project Overview and Goals
The goal of this project is to develop a machine learning–based classification system to identify failing semiconductor units during manufacturing. The model uses parametric test data to classify devices as Pass (0) or Fail (1).
This problem is particularly critical for automotive applications, where product reliability is essential and failure in the field can lead to safety risks, recalls, and financial loss.
The objective of this project is:
	✅ Minimize escape rate (False Negatives → FN ≈ 0)
	⚠️ Reduce overkill (False Positives → FP) where possible
Multiple models were trained, evaluated, and compared using metrics aligned with reliability engineering requirements.

✅ Findings
After cleaning, feature engineering, dimensionality reduction, and class imbalance handling, the following results were achieved:
### Model Comparison

| Model | FN | FP | Escape (%) | Overkill (%) | AUC |
|------|----|----|------------|--------------|------|
| Logistic Regression (Balanced) | 0 | 874 | 0.00% | 98.31% | 0.682 |
| SVM (Balanced) | 9 | 261 | 31.03% | 29.36% | 0.749 |
| Decision Tree (Balanced) | 7 | 305 | 24.14% | 34.31% | 0.781 |
| Gradient Boosting | 15 | 57 | 51.72% | 6.41% | 0.807 |
| ✅ XGBoost | **0** | **852** | **0.00% ✅** | 95.84% | 0.809 |


✅ ROC Curve Interpretation
From the ROC curve provided:
	• Gradient Boosting achieves the highest AUC (~0.807)
	• XGBoost achieves a very close AUC (~0.809) with better FN control
	• Logistic Regression has the lowest AUC (~0.682), indicating weak separability
👉 This shows that while some models separate data better statistically, they do not meet reliability requirements.

✅ Final Results and Conclusion
The final selected model is:
	✅ XGBoost
Final Confusion Matrix:
             Pred Pass   Pred Fail
Actual Pass       37           852
Actual Fail        0            29
Final Metrics:
FN = 0 ✅  
FP = 852  
Escape % = 0.00% ✅  
Overkill % ≈ 95.84%  
AUC ≈ 0.809  


✅ Automotive Reliability Justification
In automotive semiconductor applications:
Cost of Failure Escape (FN) >> Cost of Overkill (FP)
	• ❌ Escape → Field failure → Safety risk → Recall
	• ✅ Overkill → Scrap / re-test → Controlled cost
👉 Therefore:
	✅ A model achieving zero escape is required, even at the cost of higher overkill
Although XGBoost has high overkill, it guarantees detection of all failing units, making it the most appropriate model.

✅ Key Insight
This project demonstrates:
	❗ It is not possible to minimize both FN and FP simultaneously
This is due to overlapping distributions between pass and fail units, which limits separability.
👉 Therefore:
	✅ A tradeoff must be made — prioritizing reliability over efficiency

✅ Impact of Class Imbalance Handling
Class imbalance was a major challenge in the dataset.
After applying:
	• scale_pos_weight (XGBoost)
	• class_weight='balanced' (other models)
	• Threshold tuning
Results improved significantly:
	• Logistic Regression improved from FN = 11 → FN = 0
	• SVM and Decision Tree reduced FN substantially
However:
	✅ XGBoost still achieved the best overall performance

✅ Future Work and Recommendations
To reduce overkill (FP), the following approaches are recommended:
✅ 1. Two‑Stage Screening System
	• Stage‑1: High sensitivity (FN = 0)
	• Stage‑2: Reduce FP using refined model
✅ 2. Feature Engineering
	• Aggregate correlated features
	• Create stability-based features
✅ 3. Probability Banding
	• High-risk → FAIL
	• Low-risk → PASS
	• Medium → further screening
✅ 4. Domain-Based Rules
	• Analyze false positives and apply targeted overrides

✅ Rationale
Semiconductor devices used in automotive systems must meet extremely high reliability standards. A single defective unit escaping into the field can lead to severe consequences.
Machine learning enables improved screening accuracy by analyzing large-scale manufacturing data and identifying failure patterns early.

✅ Research Question
	What machine learning model best detects failing semiconductor units while ensuring zero escape rate and acceptable overkill?

✅ Data Sources
	• Semiconductor manufacturing dataset
	• ~3,059 samples
	• ~34,657 initial features
	• Target: Pass (0), Fail (1)

✅ Data Cleaning and Preparation
	• Removed ID and non-informative columns
	• Converted all features to numeric
	• Replaced sentinel values (-999, -777, etc.)
	• Removed columns with 100% missing data
	• Imputed missing values
	• Handled infinite and extreme values

✅ Exploratory Data Analysis (EDA)
EDA revealed:
	• Strong class imbalance (Pass >> Fail)
	• High feature correlation
	• Overlapping distributions
	• Weak separability in raw data

✅ Feature Engineering
	• Difference features (e.g., DD1 − RADIUS)
	• Ratio features (e.g., DD1 / RADIUS)
These improved representation of nonlinear relationships.

✅ Dimensionality Reduction
	• Reduced features from ~34,657 → 300
This step was critical for:
	• Removing noise
	• Improving model stability
	• Preventing overfitting

✅ Methodology
	• Stratified train/test split
	• Cross-validation
	• Threshold tuning (0.02)
	• Multi-model comparison

✅ Handling Class Imbalance
	• XGBoost: scale_pos_weight
	• Logistic, SVM, Tree: class_weight='balanced'
	• Stratified sampling
	• Threshold adjustment

✅ Model Evaluation
Models were evaluated using:
	• Confusion matrices
	• ROC curves (included)
	• AUC
	• Escape rate (FN)
	• Overkill (FP)

✅ Key Observations
	• Gradient Boosting achieves best AUC but fails reliability requirement
	• Logistic reaches FN = 0 but with worst overkill
	• XGBoost provides best tradeoff between FN, FP, and AUC

✅ Project Structure
	• Jupyter Notebook: Complete modeling pipeline: https://github.com/harinisrepo/UCB-MOD24-.git
  Project Input file: https://drive.google.com/file/d/1tPveQCpECjwQpfxFykbD2mr2LwT2hL2V/view?usp=sharing
	• README: Summary of findings and conclusions

✅ Final Takeaway
	In automotive semiconductor applications, eliminating escape failures is the highest priority. XGBoost provides the most reliable solution by achieving zero escape while maintaining strong predictive capability, even at the cost of higher overkill.
