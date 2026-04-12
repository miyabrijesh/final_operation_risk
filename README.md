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
- Certain return reasons are **exclusive fraud indicators**  
- Fraud patterns are **non-linear in nature**  

---

# 🔍 Inferences

1. **Fraud is the primary driver of operational delay**  
   Fraudulent returns take significantly longer to process (≈3.6×), proving that fraud directly impacts warehouse efficiency rather than just financial loss.

2. **Warehouse load amplifies fraud risk**  
   Fraud rates increase drastically during high-load conditions (16.9% → 48.8%), suggesting that fraudsters exploit peak operational stress.

3. **Manual inspection bottleneck**  
   Nearly **88% of fraudulent returns require human inspection**, creating a resource bottleneck and slowing down overall processing.

4. **Strong rule-based fraud signals exist**  
   Certain return reasons (e.g., empty box, fake defect claims) appear exclusively in fraud cases, enabling immediate rule-based filtering before ML intervention.

5. **Fraud detection is non-linear**  
   Logistic Regression performed poorly (AUC ≈ 0.57), indicating that fraud patterns cannot be captured using linear decision boundaries.

6. **Tree-based models are more effective**  
   Random Forest achieved high performance (AUC ≈ 0.96), making it suitable for real-world deployment.

7. **Class imbalance must be handled carefully**  
   Fraud cases are fewer but critical. Applying SMOTE only on training data ensured balanced learning without evaluation bias.

8. **Real-world validation supports simulation**  
   The Olist dataset (~4.6% fraud rate) aligns with expected industry benchmarks, validating the simulated dataset’s realism.

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
| XGBoost | 1.00 | 1.00 | 1.00 |

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
- Non-linear models preferred over linear  

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
- XGBoost  
- Pandas  
- NumPy  
- Matplotlib / Seaborn  

---

# 🚀 Key Contribution

This project integrates:
- **Operations Analytics** (efficiency, load handling)  
- **Fraud Analytics** (risk detection)  

→ Delivering a **real-time decision-support system** for e-commerce warehouses  

---

# 📌 Conclusion

Fraud is not just a financial issue — it is a **critical operational bottleneck**.  
By combining fraud detection with warehouse decision logic, this system improves efficiency, reduces delays, and optimizes resource allocation.

---

# 📬 Future Scope

- Real-time API deployment  
- Explainable AI (SHAP integration)  
- Live transaction data integration  
- Multi-warehouse scalability  
