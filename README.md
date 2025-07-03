# 🏦 Credit Risk Modeling – Bati Bank

Welcome to the Credit Scoring Model project for Bati Bank, a leading financial institution partnering with an eCommerce platform to launch a Buy Now, Pay Later (BNPL) service.

As part of the Analytics Engineering team, your mission is to build a credit scoring model to assess the risk level of new customers using transaction behavior data.

---

## 📌 Project Objective

Build a robust and interpretable credit scoring system using customer transactional behavior. The system will:

1. Define a proxy default variable for risk classification
2. Select relevant features predictive of risk
3. Train a risk prediction model for new customers
4. Assign a credit score from the predicted risk
5. Estimate the optimal loan amount and duration based on risk

---

## 📂 Project Structure

credit-risk-model/
├── .github/workflows/ci.yml # CI/CD pipeline  
├── data/  
│   ├── raw/ # Raw data (gitignored)  
│   └── processed/ # Processed data for modeling  
├── notebooks/  
│   └── 1.0-credit_risk_business_understanding.ipynb  
├── src/  
│   ├── init.py  
│   ├── data_processing.py # Feature engineering scripts  
│   ├── train.py # Model training  
│   ├── predict.py # Prediction/inference logic  
│   └── api/  
│       ├── main.py # FastAPI app for serving predictions  
│       └── pydantic_models.py # Data validation for API  
├── tests/  
│   └── test_data_processing.py # Unit tests  
├── Dockerfile  
├── docker-compose.yml  
├── requirements.txt  
├── .gitignore  
└── README.md  

---

## 📊 Credit Scoring Business Understanding

### 1. Basel II Accord and Model Interpretability 🎯

The Basel II Accord mandates financial institutions to maintain sufficient capital to cover risks, including credit risk, by using internal risk models. These models must be:

- Transparent and auditable
- Based on clearly defined assumptions and historical data
- Documented with traceable input–output logic

The use of internal ratings-based (IRB) approaches like PD (Probability of Default), LGD (Loss Given Default), and EAD (Exposure at Default) requires banks to justify and explain model decisions to both internal risk teams and external regulators.

👉 Our implication: We need to build an interpretable, auditable, and explainable model to meet regulatory expectations.

---

### 2. Why a Proxy Variable Is Necessary — and Its Business Risks ⚠️

Since our dataset lacks an explicit default label, we must create a proxy variable to classify users into high-risk (bad) or low-risk (good). This could be derived from behavioral patterns such as:

- Fraud flags (FraudResult)
- Refund or negative balance behaviors
- RFM (Recency, Frequency, Monetary) patterns

📉 Risks of using a proxy:

- Misclassification: Incorrectly labeling non-defaulting customers as risky
- Bias: Over-reliance on past patterns might discriminate against new users or minorities
- Lack of explainability: Regulators may question the validity of the proxy
- Customer impact: Wrong decisions might lead to customer churn or reputation damage

✅ Solution: Design the proxy based on strong business logic, and validate it with subject matter experts and testing.

---

### 3. Trade-offs: Logistic Regression vs. Gradient Boosting 🧠

| Feature                    | Logistic Regression + WoE         | Gradient Boosting (e.g. XGBoost)       |
|---------------------------|-----------------------------------|----------------------------------------|
| Interpretability          | High                              | Low                                    |
| Compliance-ready          | Yes                               | Needs explainability tools (e.g. SHAP) |
| Performance               | Moderate                          | High                                   |
| Overfitting Risk          | Low                               | Higher without tuning                  |
| Deployment Simplicity     | Easy                              | Requires model serving infra           |
| Scorecard Ready           | Yes                               | Needs transformation pipeline          |

⚖️ Takeaway: In regulated environments, interpretable models (like Logistic Regression with Weight of Evidence) are preferred. For internal experimentation or performance gains, boosted models can be used with explainability tools.

---

## 🔗 References

- [Basel II Accord PDF](https://www3.stat.sinica.edu.tw/statistica/oldpdf/A28n535.pdf)  
- [Alternative Credit Scoring - HKMA](https://www.hkma.gov.hk/media/eng/doc/key-functions/financial-infrastructure/alternative_credit_scoring.pdf)  
- [World Bank Credit Scoring Guide](https://thedocs.worldbank.org/en/doc/935891585869698451-0130022020/original/CREDITSCORINGAPPROACHESGUIDELINESFINALWEB.pdf)  
- [Scorecard Development Guide – TDS](https://towardsdatascience.com/how-to-develop-a-credit-risk-model-and-scorecard-91335fc01f03)  
- [Credit Risk Overview – Corporate Finance Institute](https://corporatefinanceinstitute.com/resources/commercial-lending/credit-risk/)  
- [Credit Risk Regulation – Risk Officer](https://www.risk-officer.com/Credit_Risk.htm)

---

## 🚀 Next Steps

> Now that business understanding is documented, proceed to:
- Define your proxy target
- Engineer relevant features
- Train & evaluate your first model
- Serve the model via API

---

📬 Contact:  
Analytics Engineering Team – Bati Bank  
📧 support@batibank.com
