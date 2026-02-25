# Time_series_Yes_bank-OHLC-

---

# 📊 Yes Bank Time Series Forecasting (OHLC)

## 📌 Project Overview
This project applies **Machine Learning models** to Yes Bank’s OHLC (Open, High, Low, Close) time‑series data.  
The goal is to forecast price behavior across both **stable** and **crash regimes**, evaluate performance using multiple metrics, and ensure interpretability through feature engineering and explainability tools.

---

## ⚙️ Workflow Steps
1. **Data Preparation**
   - Collected OHLC data with dates.
   - Split into **pre‑crash (training)** and **post‑crash (testing)** datasets to avoid leakage.
   - Applied scaling using only training data.

2. **Feature Engineering**
   - `lag1` → Previous day’s close (momentum).
   - `High_Low` → Intraday volatility spread (High − Low).
   - `High_Close` → Ratio of High to Close (bullish sentiment).
   - `Low_Close` → Ratio of Low to Close (bearish sentiment).
   - `EMA3` → 3‑day rolling volatility (short‑term clustering).
   - `bull` → Binary flag (Close > Open).

   👉 These features capture **momentum, volatility, and regime shifts**, making the model more robust than raw OHLC inputs.

3. **Model Training**
   - Compared **Linear Regression, Lasso, and Random Forest**.
   - Trained only on pre‑crash data.
   - Evaluated on crash and full periods.

4. **Evaluation Metrics**
   - **Accuracy** → Overall correctness.
   - **Recall** → Capturing risk events (critical for business impact).
   - **F1 Score** → Balance between precision and recall.
   - **RMSE** → Forecast error in continuous values.
   - **Confusion Matrix** → Classification breakdown.

5. **Explainability**
   - Used **SHAP plots** to interpret feature importance.
   - Confirmed `lag1`, `EMA3`, and `High_Low` as dominant drivers.

---

## 📈 Key Findings
- **Best Model:** Linear Regression  
  - Post‑cutoff Accuracy: **0.78**  
  - F1 Score: **0.75**  
  - Recall: **0.75**  
  - Confusion Matrix:  
    ```
    [[42 10]
     [10 30]]
    ```
  - RMSE: **15.60 (crash period)**, **7.56 (full period)**

- **Business Impact:**  
  - Recall ensures **risk events are not missed**.  
  - RMSE ensures **forecast error is minimized**.  
  - Together, they provide actionable insights for financial decision‑making.

---

## 📊 Visualizations
- **Prediction Graphs:** Actual vs. Predicted values with crash date marked.  
- **Confusion Matrix Heatmap:** Classification performance.  
- **SHAP Summary Plot:** Feature importance and direction of influence.  
- **Boxplots / Violin Plots:** Statistical tests for volatility regimes.

---

## 🔬 Statistical Hypothesis Tests
1. **Bearish Regimes:** Close is significantly closer to Low than High.  
2. **Bullish Regimes:** ≥3 green candles out of 4 → significantly higher Close prices.  
3. **Volatility Regimes:** High EMA3 → significantly larger High‑Low ranges.  

👉 All three tests confirmed **statistically significant differences** (p < 0.05).

---

## 🚀 Future Work
- Benchmark **ElasticNet** and **Gradient Boosting (XGBoost/LightGBM)**.  
- Explore **LSTM/GRU** for sequential dependencies.  
- Enhance features with **drawdown indicators, rolling skewness/kurtosis**.  
- Package preprocessing + model into a **deployment pipeline** (pickle/joblib).  
- Implement **production monitoring** for recall and RMSE.

---

## ✅ Conclusion
This project shows that with **careful feature engineering, leakage‑free training, and robust evaluation**, even a simple **Linear Regression model** can outperform more complex alternatives.  
By prioritizing **recall, RMSE, and explainability**, the model not only predicts well but also delivers meaningful business impact.
