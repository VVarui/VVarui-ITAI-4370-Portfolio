# Lab 4: Comparing Time Series Models for Network Traffic Forecasting

**Notebook:** [`lab4-time-series-forecasting.ipynb`](../labs/lab4-time-series-forecasting.ipynb)

## Problem Statement
Different forecasting techniques make different tradeoffs between simplicity, interpretability, and predictive accuracy. This lab compares three distinct modeling approaches — a classical statistical model (ARIMA), a feature-engineered linear model, and a deep learning model (LSTM) — to determine which best forecasts network traffic (Mbps) over time.

## Methods and Tools
- **Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn, statsmodels (ARIMA, seasonal decomposition, ADF test), scikit-learn (Linear Regression), TensorFlow/Keras (LSTM)
- **Data:** A full year (8,760 hourly points) of synthetic network traffic data, mean ≈ 167 Mbps, std ≈ 48 Mbps.
- **Pipeline:**
  1. **EDA:** Computed summary statistics, performed seasonal decomposition, and ran an Augmented Dickey-Fuller (ADF) test to check stationarity (ADF statistic = -12.83, p ≈ 0.000 → series is stationary).
  2. **Chronological train/test split:** 7,008 training samples (Jan 1–Oct 19) / 1,752 test samples (Oct 20–Dec 31).
  3. **Model 1 — ARIMA(2,1,2):** A classical autoregressive model fit directly on the traffic series.
  4. **Model 2 — Linear Regression with engineered features:** 16 engineered features including moving averages (e.g., `ma_3`).
  5. **Model 3 — LSTM neural network:** Sequence length of 24 hours, single LSTM layer (50 units, 10,451 total parameters), trained to predict the next hour's traffic.

## Results
| Model | Key Metric(s) |
|---|---|
| ARIMA(2,1,2) | AIC = 61,215.8, BIC = 61,250.1 |
| Linear Regression (engineered features) | Test R² = 1.0000, Test MSE ≈ 0.00 |
| LSTM | MSE = 322.58, MAE = 13.38, RMSE = 17.96 |

## Interpretation
The linear regression model's near-perfect R² is a red flag rather than a success — it strongly suggests **data leakage**, most likely because a feature like `ma_3` (a moving average) was computed using information that overlaps with the target value itself. A model that perfectly predicts test data should be treated with suspicion, not celebrated; this is a valuable, realistic lesson about validating feature engineering pipelines rather than trusting a headline metric.

The LSTM produced a more believable and interpretable error profile (RMSE ≈ 18 Mbps against a mean of ~167 Mbps, roughly 11% typical error), showing it captured meaningful temporal structure without any leakage risk. The ARIMA model provided a solid classical baseline and confirmed the series was stationary, which validated the assumptions needed for a well-specified ARIMA model.

**Takeaway:** more complex models aren't automatically better — the real skill demonstrated in this lab was diagnosing *why* a model's results looked too good to be true, and understanding what each modeling family (statistical vs. engineered-feature vs. deep learning) is suited for.
