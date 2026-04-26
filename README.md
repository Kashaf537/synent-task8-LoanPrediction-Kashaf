# 💳 Credit Default Prediction Model

## 📌 Problem Statement
Predict whether a borrower will default on their loan based on their financial profile.

Financial institutions face significant losses due to loan defaults. By predicting default risk before loan approval, lenders can:

- Reduce financial losses from bad loans  
- Offer appropriate interest rates based on risk  
- Make data-driven lending decisions  
- Comply with regulatory requirements  

### 🎯 Business Question
Given a borrower’s **employment status**, **bank balance**, and **annual salary**, can we predict whether they will default?

---

## 📊 Dataset Details

- **Source File:** `Default_Fin.csv`  
- **Total Records:** 10,000 loan applicants  
- **Features:** 3 input variables + 1 target variable  

### Variables

| Variable        | Type              | Description |
|-----------------|------------------|-------------|
| Employed        | Binary           | 1 = Currently employed, 0 = Not employed |
| Bank Balance    | Continuous       | Current bank account balance |
| Annual Salary   | Continuous       | Yearly income |
| Defaulted?      | Binary (Target)  | 1 = Defaulted, 0 = Paid as agreed |

---

## 📈 Dataset Statistics

| Feature         | Mean      | Std Dev   | Min   | Max |
|-----------------|----------|----------|------|------|
| Bank Balance    | $10,482  | $6,947   | $0   | $32,000+ |
| Annual Salary   | $499,000 | $142,000 | $30,000 | $860,000 |

### Class Distribution

| Class | Count | Percentage |
|------|------|------------|
| No Default (0) | 9,798 | 97.98% |
| Default (1) | 202 | 2.02% |

> ⚠️ Highly imbalanced dataset (~50:1 ratio), requiring special handling during modeling.

---

# 🔍 Approach

## Data Preprocessing

| Step | Description |
|------|------------|
| Missing Value Check | No missing values found |
| Feature Scaling | StandardScaler applied for Logistic Regression |
| Train-Test Split | 80/20 split with stratification |
| Class Imbalance | `class_weight='balanced'` |

---

## 📊 Exploratory Data Analysis

### Default Rate by Employment

| Employment Status | Default Rate |
|------------------|-------------|
| Employed | 1.8% |
| Not Employed | 3.2% |

➡️ Unemployed borrowers show **78% higher risk**.

### Average Values Comparison

| Feature | Non-Defaulters | Defaulters | Difference |
|--------|---------------|-----------|-----------|
| Bank Balance | $10,515 | $5,478 | -48% |
| Annual Salary | $501,000 | $150,000 | -70% |

### Correlation with Default

| Feature | Correlation |
|--------|------------|
| Annual Salary | -0.18 |
| Bank Balance | -0.12 |
| Employed | -0.04 |

---

# 🤖 Models Tested

| Model | Description | Parameters |
|------|------------|-----------|
| Logistic Regression | Baseline linear model | `class_weight='balanced'` |
| Decision Tree | Simple tree model | `max_depth=5` |
| Random Forest | Ensemble model | `n_estimators=100, max_depth=10` |
| XGBoost | Gradient boosting | `scale_pos_weight adjusted` |

---

# 📏 Evaluation Metrics

- **Accuracy** → Overall correctness  
- **Precision** → Predicted defaults that were correct  
- **Recall** → Actual defaults successfully identified  
- **F1-Score** → Balance between Precision & Recall  
- **AUC-ROC** → Ability to separate classes  
- **RMSE** → Root Mean Squared Error  

---

# 📈 Results

## Model Performance Comparison

| Model | Accuracy | Precision | Recall | F1-Score | AUC-ROC | RMSE |
|------|----------|----------|-------|---------|--------|------|
| Logistic Regression | 97.7% | 0.21 | 0.23 | 0.22 | 0.67 | 0.152 |
| Decision Tree | 96.9% | 0.16 | 0.28 | 0.20 | 0.63 | 0.176 |
| Random Forest | 98.1% | 0.33 | 0.23 | 0.27 | 0.75 | 0.137 |
| XGBoost | 98.2% | 0.35 | 0.27 | 0.30 | 0.78 | 0.133 |

---

## 🌟 Feature Importance (Random Forest)

| Feature | Importance |
|--------|-----------|
| Annual Salary | 58% |
| Bank Balance | 31% |
| Employed | 11% |

---

# ⚙️ Tuned Random Forest Model

### Best Parameters

| Parameter | Value |
|----------|------|
| max_depth | 10 |
| min_samples_leaf | 4 |
| min_samples_split | 5 |
| n_estimators | 200 |

### Performance at Optimal Threshold (0.07)

| Metric | Value |
|-------|------|
| Accuracy | 97.9% |
| Precision | 0.38 |
| Recall | 0.41 |
| F1-Score | 0.39 |

---

# 💡 Key Insights

- **Annual Salary** is the strongest predictor.  
  A $100,000 increase in salary reduces default probability by **~40%**.

- **Employment Status** has less impact than expected.  
  Being employed reduces risk by only **1.4 percentage points**.

- **Bank Balance** has moderate predictive power.  
  Every $10,000 increase reduces default risk by **~15%**.

### Typical Defaulter Profile

- Lower salary (**$150k avg vs $500k**)  
- Lower bank balance (**$5.5k avg vs $10.5k**)  
- Higher unemployment rate (**3.2% vs 1.8%**)  

---

# ✅ Conclusion

Among all models tested, **XGBoost** achieved the best performance, while **Random Forest** offered strong interpretability and competitive results.  

This project demonstrates how machine learning can help financial institutions reduce risk and make smarter lending decisions.
