---

# 📌 Interpretable Retail Demand Forecasting using Machine Learning & Statistical Models

A complete end-to-end retail demand forecasting system built using **Time-Series Machine Learning, ARIMA/SARIMA models, XGBoost, and SHAP-based interpretability**.

---

## 🚀 Project Overview

This project forecasts **weekly retail demand** using the **Walmart Sales Forecasting Dataset**.
The objective is to **compare baseline, statistical, and machine learning models** and identify the most accurate and interpretable forecasting approach for real-world retail planning.

### 🔄 Workflow Summary

* 📊 Exploratory Time-Series Analysis
* 🧮 Feature Engineering (lags, rolling windows, seasonality extraction)
* 🧠 Model Building

  * Naive Baseline
  * Linear Regression
  * Random Forest
  * XGBoost
  * ARIMA / SARIMA
* 📉 Evaluation: RMSE, MAE, MAPE
* 🔍 SHAP Interpretability
* 🧾 Business Insights & Recommendations

---

## 🗂️ Dataset

**Source:** Walmart Weekly Sales Forecasting Dataset (Kaggle)

### Features Used

* `Store`
* `Dept`
* `Date`
* `Weekly_Sales`
* `IsHoliday`

After filtering:

* **Store:** 1
* **Department:** 1
* **143 weekly observations**

---

## 📊 1. Exploratory Data Analysis (EDA)

### Weekly Sales Time Series (Actual Visualization)

<img src="notebook/images/weekly_sales_store1_dept1.png" width="800">

### Key Observations

* Seasonal spikes around holidays
* No strong long-term trend
* Stable sales between holiday peaks
* High short-term autocorrelation

Sales patterns indicate:

* Momentum-driven behavior
* Seasonally reactive variations
* Irregular spike-heavy structure

---

## 🛠️ 2. Feature Engineering

To convert the time series into a supervised ML problem:

### 📌 Lag Features

* `Lag_1` (last week)
* `Lag_2`
* `Lag_4` (1 month prior)
* `Lag_12` (seasonal memory)

### 📌 Rolling Window Features

* `Rolling_Mean_4` — smooths short-term fluctuations

### 📌 Date Features

* `Month`
* `Week`

These features enable machine learning models to capture temporal dependencies effectively.

---

## 🧪 3. Train–Test Strategy

* **Train–Test Split:** 80% train, 20% test
* **No shuffling** → avoids time leakage
* **TimeSeriesSplit CV** used for Random Forest & XGBoost

---

## 🤖 4. Models Implemented

### 🔹 Naive Baseline

Predicts
**Next week = Last week (Lag_1)**
Works well because of strong autocorrelation.

### 🔹 Linear Regression

Simple model; struggles on nonlinear spikes.

### 🔹 Random Forest

Captures nonlinearity better than linear models.

### 🔹 XGBoost (🔥 Best Model)

Gradient boosting with tuned hyperparameters.
Best performance on **all** metrics:

* Lowest RMSE
* Lowest MAE
* Lowest MAPE

### 🔹 ARIMA & SARIMA

SARIMA failed due to inconsistent seasonality.
ARIMA improved but still far below ML models.

---

## 📈 5. Model Performance Comparison

| Model              | RMSE     | MAE     | MAPE      |
| ------------------ | -------- | ------- | --------- |
| Naive              | 1308     | 1077    | 5.73%     |
| Linear Regression  | 3037     | 1455    | 8.45%     |
| Random Forest      | 1336     | 966     | 4.92%     |
| **XGBoost (Best)** | **1114** | **782** | **4.01%** |
| SARIMA             | 14016    | 13310   | 75.32%    |
| ARIMA              | 10455    | 9664    | 55.59%    |

Winner: **XGBoost**

> ~65% improvement over linear regression and significantly beats statistical models.

---

## 🔍 6. SHAP Interpretability (Explainable ML)

SHAP was applied to explain XGBoost predictions.

### Key Insights

* **Lag_1** dominates (~57% importance)
* **Lag_2** also important
* `Rolling_Mean_4` raises predictions when recent momentum is high
* `Lag_12` contributes less (weak long-term seasonality)
* Holiday effects inconsistent

Conclusion:
Retail demand is **short-memory driven**, not long-term seasonal.

### SHAP Plot

<h3>SHAP Summary Plot</h3>
<img src="images/shap-summary1.png" width="550">

<h3>SHAP Bar Plot</h3>
<img src="images/shap-summary2.png" width="450">

<h3>SHAP Local Decision Plot</h3>
<img src="images/shap-summary3.png" width="800">

---

## 🧾 7. Business Insights

✔ Recent demand (Lag_1, Lag_2) is the strongest predictor
✔ Spikes caused by promotions/holidays are inconsistent
✔ ARIMA/SARIMA struggle with irregular retail behavior
✔ XGBoost handles spikes + nonlinearity exceptionally well

These findings help with:

* Better inventory planning
* Understanding demand momentum
* Avoiding over-reliance on classical forecasting models

---

## 🧱 8. Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* Statsmodels
* XGBoost
* SHAP

---

## 📂 Project Structure

```
Retail_Demand_Forecasting/
│── data/
│── notebook/
│   ├── 01_EDA.ipynb
│   ├── 02_Feature_Engineering.ipynb
│   ├── 03_Modeling.ipynb
│   ├── 04_Evaluation.ipynb
│   ├── 05_Interpretability_SHAP.ipynb
│── README.md
```

---

## 🧠 9. Key Learnings

* Time-series forecasting requires **data-aware splitting**
* Lag features outperform complex statistical models
* **Boosting > Bagging > Linear models** for nonlinear patterns
* SHAP is essential for **interpretable ML**
* Retail data is messy → classical ARIMA often fails

---

## 🏁 10. Final Summary

This project demonstrates a fully interpretable retail forecasting workflow covering:

✔ EDA
✔ Feature Engineering
✔ Model Comparison
✔ Time-Series CV
✔ SHAP Explainability
✔ Business Insights

**XGBoost is the most accurate & reliable forecasting model for retail demand.**

---

## ⭐ Support

If this repository helped you, please consider **starring the project**!

---


