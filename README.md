# 🛒 E-Commerce Return Fraud & Warehouse Efficiency Analysis  
### Operations Analytics & Risk/Fraud Analytics Project

**Course:** MGT3014 — Operations Analytics  
**Institution:** VIT Chennai  
**Guide:** Dr. Balaji J  

**Team:**  
22MIA1067 · 22MIA1084 · 22MIA1165 · 22MIA1174 · 22MIA1197  

🔗 **Live App:** https://finaloperationrisk-taczj2drhzvdcqpxptapbt.streamlit.app  

---

# 📌 Problem Statement

E-commerce platforms face significant operational inefficiencies due to fraudulent return requests. These fraudulent returns:
- Increase warehouse processing time  
- Overload inspection systems  
- Reduce service efficiency for genuine customers  

This project builds a **decision-support system** to:
1. Detect fraudulent return requests  
2. Predict processing effort  
3. Recommend warehouse actions  

---

# 🎯 Objectives

- Identify fraud patterns in return transactions  
- Quantify operational impact of fraud  
- Build predictive ML models for fraud detection  
- Optimize warehouse decision-making  

---

# 📊 Datasets Used

| Dataset | Description | Role |
|--------|------------|------|
| `QuickCommerce_ReturnFraud_Dataset.xlsx` | Simulated quick-commerce dataset | Model training |
| `final_return_dataset.csv` | Real-world Olist dataset (~111K rows) | EDA & validation |
| `Consumer_Survey.xlsx` | User behavior survey | Contextual insights |

---

# 📊 Key Insights

- Fraudulent returns take **3.6× longer** to process  
- Fraud rate increases from **16.9% → 48.8%** under high warehouse load  
- **88% of fraud cases require manual inspection**  
- Certain return reasons act as strong fraud indicators  
- Fraud patterns are **non-linear in nature**  

---

# 🔍 Inferences

1. **Fraud is the primary driver of operational delay**  
   Fraudulent returns take significantly longer to process, proving fraud impacts operations beyond financial loss.

2. **Warehouse load amplifies fraud risk**  
   Fraud rates increase sharply during peak load, indicating exploitation of operational stress.

3. **Manual inspection bottleneck**  
   A large proportion of fraud cases require manual or intensive inspection, reducing system efficiency.

4. **Fraud detection is non-linear**  
   Logistic Regression performed poorly (AUC ≈ 0.57), indicating complex feature interactions.

5. **Tree-based models are more effective**  
   Decision Tree and Random Forest significantly outperform linear models.

6. **Random Forest is the most reliable model**  
   It provides the best balance of precision, recall, and ROC-AUC without overfitting.

7. **Class imbalance handling is critical**  
   SMOTE ensured fair learning while maintaining real-world evaluation integrity.

8. **Real-world validation supports simulation**  
   Olist dataset (~4.6% fraud rate) aligns with industry expectations.

---

# 📈 Machine Learning Models

## 🔹 Fraud Detection Model
- Algorithm: Random Forest  
- Accuracy: **88%**  
- ROC AUC: **0.96**  
- Balanced Precision & Recall  

## 🔹 Processing Prediction Model
- Algorithm: Random Forest  
- Output: Low / Medium / High effort  

---

# 📊 Model Comparison

| Model | Accuracy | F1 Score | ROC AUC |
|------|--------|---------|--------|
| Logistic Regression | 0.58 | 0.49 | 0.57 |
| Decision Tree | 0.86 | 0.76 | 0.89 |
| Random Forest | **0.88** | **0.82** | **0.96** |

---

# ⚠️ Note on XGBoost

XGBoost initially achieved perfect performance (100% across all metrics). However, this indicated **overfitting due to the small test set size (N=50)**.  

To ensure realistic and generalizable results, it was excluded from final evaluation, and **Random Forest was selected as the production model**.

---

# ⚙️ Risk-Based Decision System

| Fraud Probability | Risk Level | Action |
|------------------|----------|--------|
| < 30% | Low | Fast-track — basic inspection |
| 30–55% | Medium | Manual verification required |
| ≥ 55% | High | Intensive inspection — hold return |

---

# 🧪 Methodology

- Data cleaning & preprocessing  
- Exploratory Data Analysis (EDA)  
- Feature encoding  
- Train-test split  
- SMOTE for class balancing  
- Model training & comparison  

### Evaluation Metrics:
- Accuracy  
- Precision  
- Recall  
- F1 Score  
- ROC-AUC  

---

# 📊 Statistical Validation

- Independent T-test conducted on processing time  
- Result: **p < 0.001 → statistically significant**  
- Confirms fraud significantly impacts operational efficiency  

---

# ⚠️ Important Modeling Decisions

- SMOTE applied only on training data (to avoid data leakage)  
- Post-decision variables removed from features  
- Real-world dataset used for validation  
- Linear models rejected due to poor performance  
- Tree-based ensemble model selected for deployment  

---

# 📁 Project Structure

.
├── app.py  
├── fraud_model.pkl  
├── processing_model.pkl  
├── encoders.pkl  
├── ecommerce_returns_dashboard.html  
├── final_return_dataset.csv  
├── QuickCommerce_ReturnFraud_Dataset.xlsx  
├── Consumer_Survey.xlsx  
├── operations_analytics_review2.ipynb  
└── README.md  

---

# 🛠️ Tech Stack

- Python  
- Streamlit  
- Scikit-learn  
- Pandas  
- NumPy  
- Matplotlib / Seaborn  

---

# 🚀 Key Contribution

This project integrates:
- **Operations Analytics** (efficiency, workload optimization)  
- **Fraud Analytics** (risk detection)  

→ Delivering a **practical decision-support system** for warehouse management  

---

# 📌 Conclusion

Fraud is not just a financial issue — it is a **critical operational bottleneck**.  
By integrating fraud detection with warehouse decision-making, this system improves efficiency, reduces delays, and optimizes resource allocation.

---

# 📬 Future Scope

- Real-time API deployment  
- Explainable AI (SHAP integration)  
- Live transaction data integration  
- Multi-warehouse scalability  
