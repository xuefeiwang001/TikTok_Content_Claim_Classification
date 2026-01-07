# TikTok Content Claim Classification (Claims vs Opinions)

## Overview
TikTok receives a high volume of user reports flagging videos/comments that may contain **claims** (vs. opinions).  
Manual review creates backlogs, so this project builds a **predictive model** to classify content as **claim** or **opinion**, enabling:
- faster triage,
- smarter prioritization,
- reduced moderation backlog.

This repository is structured like a real analytics deliverable: notebooks for analysis + a business-facing memo for decisions.

📄 **Final deliverable:**  
- `05_insights_and_recommendations.md`

---

## Business Problem
**Goal:** Predict whether a video contains a **claim** or expresses an **opinion**, so moderation teams can prioritize reviews more efficiently.

**Success criteria (example):**
- High recall for claims (to minimize harmful claims slipping through),
- Reasonable precision (to keep reviewer workload manageable),
- Clear model interpretability + risk controls (to avoid gaming / bias).

---

## What’s Inside
### Notebooks (end-to-end workflow)
- `notebooks/01_tiktok_claims_eda_and_data_quality.ipynb`  
  Data understanding, cleaning, missing values/outliers, label distribution, initial insights.

- `notebooks/02_tiktok_claims_statistical_analysis.ipynb`  
  Descriptive statistics + hypothesis testing (e.g., group differences) to identify meaningful signals.

- `notebooks/03_tiktok_claims_baseline_logistic_regression.ipynb`  
  Interpretable baseline model (Logistic Regression) to establish a benchmark and feature directionality.

- `notebooks/04_tiktok_claims_tree_models_random_forest_xgboost.ipynb`  
  Higher-performance models (Random Forest, XGBoost), evaluation, and discussion of generalization risks.

---

## Key Results (from validation set)
- **Random Forest** achieved near-perfect performance on the validation split  
  (Precision/Recall/F1 ≈ **1.00**).
- **XGBoost** achieved similarly strong performance  
  (Accuracy ≈ **0.99**, class-level Precision/Recall ≈ **0.99–1.00**).

✅ **Important note (maturity signal):**  
Such exceptionally high scores can indicate **data leakage** or overly easy splits.  
In production, we would validate using:
- time-based split (train on past, test on future),
- author/video-level split to avoid memorization,
- robust cross-validation and monitoring.

---

## Reproducibility
- Python 3.9+
- Install dependencies: `requirements.txt`
- Run notebooks sequentially from `01` to `04`

No external APIs or credentials are required.

---

## Skills Demonstrated
- Data cleaning & EDA (pandas, numpy)
- Statistical analysis & hypothesis testing (scipy)
- Feature engineering for text signals (vectorizers)
- Modeling & evaluation (scikit-learn, xgboost)
- Business framing: turning ML outputs into moderation workflow recommendations

---

## Author  
#### Dual Master's Degrees in Data Science  ####
  - MSc in Data Analytics & Artificial Intelligence  
  - MSc in Statistics  

#### Profile Summary ####
A data-driven professional with strong analytical foundations and hands-on experience in end-to-end data projects — from ETL & dashboarding to statistical modelling and AI-powered insights.   
Passionate about transforming raw operational data into actionable business strategies.

📧 Contact: xuefei.wang.fr@gmail.com
