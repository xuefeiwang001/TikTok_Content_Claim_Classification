# Insights & Recommendations — TikTok Claim vs Opinion Classification

## 1. Executive Summary
This project builds a classifier to predict whether a piece of TikTok content expresses a **claim** or an **opinion**.
The objective is to reduce moderation backlog by enabling **faster triage and smarter prioritization** of user reports.

Across baseline and tree-based approaches, the models demonstrate strong predictive performance.
However, extremely high validation scores may suggest **data leakage** under a random split, so production readiness requires
more robust validation design.

---

## 2. Key Insights (What the data suggests)
### 2.1 Label distribution and moderation relevance
- The outcome classes (claim vs opinion) are approximately balanced in the dataset, which simplifies training and evaluation.
- In real moderation pipelines, the business definition of “claim” should be aligned with policy and enforcement standards.

### 2.2 Content and engagement signals
- Engagement-related features (e.g., views, likes, shares, comments) often exhibit heavy-tailed distributions.
- Author/account metadata may correlate with claim likelihood, but can create shortcut learning and fairness risks.

### 2.3 Statistical evidence (where applicable)
- Hypothesis testing in the analysis suggests measurable differences between groups in key metrics.
- These tests help identify stable signals, but should be paired with causal caution (correlation ≠ causation).

---

## 3. Model Findings (What the models learned)
### 3.1 Baseline: Logistic Regression
- Provides an interpretable benchmark and is useful for understanding directional effects of features.
- Best for communicating “what drives predictions” to stakeholders.

### 3.2 Tree-based models: Random Forest & XGBoost
- Validation performance is very strong (RF ~1.00; XGBoost ~0.99 accuracy).
- **Risk:** unusually high performance can indicate leakage or non-independent samples between train/validation splits.

---

## 4. Recommendations
### 4.1 Operational recommendation: triage strategy
- Use model score to prioritize review queues:
  - High probability **claim** → higher review priority
  - Medium probability → sample-based auditing
  - Low probability → deprioritize or route to lighter-touch review
- Optimize threshold based on moderation capacity:
  - If backlog is severe → favor higher precision
  - If safety risk is high → favor higher recall for claims

### 4.2 Policy recommendation: definition alignment
- Establish a clear operational definition of “claim” vs “opinion” with policy teams.
- Create a consistent annotation guideline to reduce label noise and improve generalization.

### 4.3 Model governance recommendation: leakage & generalization controls
Before production deployment:
- Validate with **time-based split** (train past → test future)
- Use **author/video-level split** to prevent memorization
- Run cross-validation and monitor performance drift
- Add guardrails: monitor high-confidence false positives/negatives and retrain cadence

---

## 5. Limitations
- Random splits may overestimate performance if related samples leak between sets.
- Features available in the dataset may not reflect all real-time production signals.
- The model predicts labels, not policy violations — human moderation remains essential.

---

## 6. Next Steps
- Build a robust offline evaluation: time split + author/video split + calibration checks
- Add explainability: SHAP (for tree models) or coefficient analysis (for logistic baseline)
- Create a lightweight dashboard for moderators to track:
  - backlog size, precision/recall trends, false negative sampling audits
- Pilot deployment with A/B test on queue prioritization and measure impact on:
  - time-to-review, backlog reduction, and safety outcomes
