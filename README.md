# 🧠 Retail Customer Income Prediction & Marketing Segmentation System

A business-oriented machine learning system that improves **marketing decision quality** — not just prediction accuracy — by combining purchasing power prediction with interpretable customer segmentation.

---

## 📌 Project Motivation

Traditional retail marketing follows a mass outreach strategy:

- Same promotion sent to everyone
- High marketing cost
- Low conversion rate
- Customer irritation
- Brand trust degradation

The real business problem is not prediction.

**The problem is:**
> Who should we contact, how should we contact them, and when should we NOT contact them?

This project builds a decision-support system that enables targeted and responsible marketing instead of blanket campaigns.

---

## 🎯 Business Objective

We design a system that answers three questions:

| Question | Model Component |
|--------|------|
| Who is worth contacting? | Income Classification Model |
| How should we approach them? | Customer Segmentation Model |
| Should we avoid contacting them? | Threshold Optimization + Economic Evaluation |

The goal is marketing efficiency, not raw model accuracy.

---

## 📊 Dataset

**U.S Census Income Dataset (1994–1995)**

- 199,523 individuals
- 42 demographic & employment attributes
- Income label (>50K / ≤50K)

The dataset represents purchasing power proxy, not actual purchasing behavior.

---

## 🧹 Data Preparation

### Handling Survey Data Issues
- Removed trailing spaces
- Converted "?" → "Unknown"
- Preserved observations (no aggressive deletion)

### Feature Engineering
Created business meaningful features:

- `has_children` indicator
- stable employment indicators

### Removed Leakage Features
Removed variables unavailable during marketing decisions:

- Capital gains
- Capital losses
- Wage per hour
- Detailed industry codes
- Residence history

The model simulates real deployment conditions, not lab accuracy.

---

## ⚠️ Critical Dataset Characteristic

Only ~6% of customers are high income.

A naive model predicting everyone as low income achieves ~94% accuracy.

Therefore:
**Accuracy is misleading → Optimize F1 & business impact**

---

## 🧪 Train / Validation / Test Split

| Split | Ratio |
|----|----|
| Train | 60% |
| Validation | 20% |
| Test | 20% |

Stratified sampling preserved income distribution.

---

## 🤖 Model 1 — Income Classification

### Baseline: Logistic Regression
Purpose: verify predictive signal exists.

Results:
- Accuracy ~95%
- F1 ≈ 0.44

Conclusion: nonlinear relationships exist.

---

### Final Model: LightGBM

Reasons for selection:
- Handles tabular data well
- Captures feature interactions
- Robust to class imbalance
- Interpretable feature importance

### Imbalance Handling
`scale_pos_weight` applied.

---

## 🎚 Threshold Optimization

Default threshold = 0.5  
Final threshold = 0.85

Optimized for stable business performance rather than accuracy.

---

## 📈 Final Model Performance

| Metric | Value |
|------|------|
| Accuracy | ~94% |
| Precision | 0.52 |
| Recall | 0.59 |
| F1 Score | 0.56 |
| PR-AUC | ~0.57 |

---

## 📉 Confusion Matrix

|  | Pred Low | Pred High |
|----|----|----|
| Actual Low | 36,081 | 1,348 |
| Actual High | 1,015 | 1,461 |

---

## 💰 Economic Evaluation

Assumptions:
- Contact cost = $1
- Conversion profit = $40

| Strategy | Contacts | Conversions | Cost | Revenue | Net Profit |
|------|------|------|------|------|------|
| Mass Marketing | 39,905 | 2,476 | $39,905 | $99,040 | $59,135 |
| Model Targeting | 2,809 | 1,461 | $2,809 | $58,440 | $55,631 |

### Key Insight
The model:
- Reduces outreach by 93%
- Keeps 59% of valuable customers
- Maintains nearly same profit

Value = efficiency, not revenue maximization.

---

## 🧠 Model Explainability

Top predictive features:

- Age
- Weeks worked
- Number of employers
- Education level
- Sex

Key finding:
Employment stability predicts purchasing power more than education.

---

## 👥 Model 2 — Customer Segmentation

Prediction identifies who to target.  
Segmentation determines how to target.

K-Means clustering applied.

---

### Choosing K

| K | Silhouette Score |
|----|----|
| 2 | 0.2257 |
| 3 | 0.2320 |
| 4 | 0.2335 |
| 5 | 0.1757 |

Selected: K = 3 (interpretable & stable)

---

## 🧩 Customer Personas

### Inactive / Retired
Very low purchase probability  
Strategy: awareness only

### Working Professionals
Highest purchasing potential  
Strategy: premium offers

### Late Career Planners
Moderate income  
Strategy: savings & warranty products

---

## ⚖️ Fairness Evaluation

False Positive Rate:

| Group | FPR |
|----|----|
| Female | 0.132 |
| Male | 0.283 |

Threshold adjusted to avoid aggressive demographic targeting.

Fairness treated as design constraint.

---

## 🏆 Final Business Value

Mass Marketing → Strategic Marketing

Benefits:
- Reduced marketing spend
- Higher relevance
- Lower customer irritation
- Long-term trust

---

## 🚀 Future Improvements

- Add purchase history
- Feedback learning loop
- Periodic retraining
- Uplift modeling

---
> 📄 For a complete explanation of the business reasoning, modeling decisions, economic evaluation, fairness analysis, and detailed interpretation, please read the full project report: [Client_Report.pdf](Client_Report.pdf)



