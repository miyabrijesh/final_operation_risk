# E-Commerce Returns Fraud vs Warehouse Efficiency
### MGT3014 — Operations Analytics | VIT Chennai

**Team:** 22MIA1067 · 22MIA1084 · 22MIA1165 · 22MIA1174 · 22MIA1197  
**Guide:** Dr. Balaji J, Associate Professor, VIT Business School

**Live App:** https://finaloperationrisk-taczj2drhzvdcqpxptapbt.streamlit.app

---

## Project Overview

A decision-support system that analyzes e-commerce return transactions to detect fraud and predict operational processing load in quick-commerce warehouse environments (Blinkit / Swiggy Instamart).

The system predicts:
- Fraud risk of an incoming return request (binary: Genuine / Suspected Fraud)
- Processing category (Low / Medium / High effort)
- Recommended warehouse action based on risk level

---

## Datasets

| Dataset | Source | Records | Role |
|---|---|---|---|
| `QuickCommerce_ReturnFraud_Dataset.xlsx` | Primary (simulated QC) | 250 | ML modelling |
| `final_return_dataset.csv` | Olist / Kaggle | 1,11,702 | EDA & real-world validation |
| `Consumer_Survey.xlsx` | Primary survey | 80 | Behavioural context |

---

## Key Findings (from Analysis)

| Finding | Value |
|---|---|
| Avg processing time — genuine returns | 20.7 min |
| Avg processing time — suspected fraud | 74.2 min |
| Fraud processing overhead | **3.6× slower** |
| T-test significance | t = −17.44, p = 5.2×10⁻⁴⁵ |
| Fraud rate under high warehouse load | **48.8%** (vs 16.9% under low load) |
| Fraud returns requiring intensive inspection | **50.6%** |
| Fraud returns requiring manual inspection | **37.6%** |
| Real-world fraud rate (Olist dataset) | **4.62%** (5,163 of 1,11,702 orders) |
| Survey respondents agreeing returns hurt efficiency | **71.8%** |

---

## Inferences

1. **Fraud is the dominant cause of warehouse delay.** Suspected fraud returns take 3.6× longer than genuine ones. This is confirmed by an independent samples T-test (p = 5.2×10⁻⁴⁵) — the difference is not sampling noise.

2. **High warehouse load is a fraud-risk amplifier.** The fraud rate climbs from 16.9% (low load) to 48.8% (high load). Peak operational periods are simultaneously the most fraud-vulnerable, suggesting fraudsters exploit stretched staff attention.

3. **88% of fraud requires a human inspector** (50.6% intensive + 37.6% manual). Every fraudulent return blocks inspector capacity that could otherwise serve legitimate returns, compounding delays during busy periods.

4. **Five return reasons are exclusive fraud signals:** Empty Box Return, Fake Defect Claim, False Damage Claim, Product Substitution, and Used Item Return appear only in suspected fraud records. These can be hard-routed to intensive inspection without any ML inference.

5. **The fraud–processing relationship is non-linear.** Logistic Regression achieved an AUC of 0.57 (barely above random), proving a linear boundary cannot separate the classes. Tree-based models are required.

6. **Random Forest (AUC 0.96) is the reliable production model.** It achieves balanced precision and recall of 0.82 for both classes, making it suitable for deployment. XGBoost scored perfect 1.00 on the 50-sample test set — promising, but requires validation on a larger holdout before production use.

7. **SMOTE was necessary and applied correctly.** The 66/34 class split (165 genuine, 85 fraud) would bias models toward the majority class. SMOTE was applied only to training data after the train/test split, keeping the test set entirely real — the methodologically correct approach to avoid synthetic data leakage into evaluation.

8. **Six columns were excluded to prevent data leakage:** `Fraud_Risk_Score`, `Return_Outcome`, `Inspector_Required`, and `Processing_Time_min` are all post-decision variables not available at prediction time. Including them would have inflated scores artificially without the model learning anything real.

9. **The Olist dataset validates the simulation.** A 4.62% fraud rate across 1,11,702 real Brazilian e-commerce orders is consistent with industry benchmarks, confirming the QuickCommerce simulation parameters are grounded in realistic data.

---

## Machine Learning Models

### Fraud detection model (`fraud_model.pkl`)
- Algorithm: Random Forest Classifier (300 trees, fraud class weighted 3×)
- Input features: `Product_Category`, `Return_Reason`, `Inspection_Level`, `Warehouse_Load`
- Output: fraud probability (0.0–1.0)
- Test accuracy: 88% | ROC AUC: 0.96 | Fraud recall: 82%

### Processing category model (`processing_model.pkl`)
- Algorithm: Random Forest Classifier (200 trees, balanced class weights)
- Input features: `Product_Category`, `Return_Reason`, `Warehouse_Load`
- Output: Low / Medium / High processing category

### Model comparison (test set, N=50)

| Model | Accuracy | F1 Score | ROC AUC |
|---|---|---|---|
| Logistic Regression | 0.58 | 0.49 | 0.57 |
| Decision Tree | 0.86 | 0.76 | 0.89 |
| Random Forest | 0.88 | 0.82 | 0.96 |
| XGBoost | 1.00 | 1.00 | 1.00 |

---

## Risk Routing Logic

| Fraud probability | Classification | Recommended action |
|---|---|---|
| < 30% | Low risk | Fast-track — basic inspection only |
| 30–55% | Medium risk | Manual verification required |
| ≥ 55% | High risk | Intensive inspection — hold return |

---

## Project Structure

.
├── app.py                          # Streamlit application
├── fraud_model.pkl                 # Fraud detection model
├── processing_model.pkl            # Processing category model
├── encoders.pkl                    # LabelEncoders for all features
├── ecommerce_returns_dashboard.html # Analytics dashboard
├── final_return_dataset.csv        # Olist dataset (EDA)
├── QuickCommerce_ReturnFraud_Dataset.xlsx  # Modelling dataset
├── Consumer_Survey.xlsx            # Survey data
└── operations_analytics_review2.ipynb     # Full analysis notebook

---

## Tech Stack

Python · Streamlit · scikit-learn · XGBoost · imbalanced-learn · pandas · joblib · Chart.js

---

## Methodology Notes

- Datasets kept separate — Olist used for EDA only due to `return_reason` data leakage
- SMOTE applied post-split on training data only
- All post-decision features excluded from model inputs
- T-test used to statistically validate the processing time difference between return types
