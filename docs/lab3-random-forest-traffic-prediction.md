# Lab 3: Predicting Network Traffic with Random Forest Regression

**Notebook:** [`lab3-random-forest-traffic-prediction.ipynb`](../labs/lab3-random-forest-traffic-prediction.ipynb)

## Problem Statement
Telecom operators need to anticipate network traffic loads (measured in Gbps) to plan capacity, avoid congestion, and allocate bandwidth efficiently. This lab investigates whether a machine learning model can accurately predict hourly network traffic using historical patterns and time-based features.

## Methods and Tools
- **Tools:** Python, NumPy, Pandas, Matplotlib, scikit-learn (`RandomForestRegressor`)
- **Data:** A synthetic hourly traffic dataset (Jan–Dec 2023) engineered to reflect realistic patterns — daily cycles, weekly cycles, and a business-hours boost (9 AM–5 PM, weekdays).
- **Feature engineering:**
  - `hour`, `day_of_week`, `is_weekend`, `is_business_hours`
  - `traffic_lag_1h` and `traffic_lag_24h` (previous hour and previous day's traffic)
  - `traffic_rolling_7d` (7-day rolling average)
- **Modeling approach:**
  1. Cleaned the dataset (dropped rows with NaNs introduced by lag/rolling features), resulting in 8,570 usable samples.
  2. Split chronologically into training and test sets (80/20, no shuffling, to respect time order).
  3. Trained a `RandomForestRegressor` (100 trees, max depth 10).
  4. Evaluated using MSE and R².
  5. Analyzed feature importance to understand which inputs drove predictions.

## Results
| Metric | Training | Testing |
|---|---|---|
| MSE | 17.59 | 34.64 |
| R² | 0.946 | 0.893 |

**Top predictive features:**
1. `traffic_lag_1h` (81.6% importance) — traffic one hour ago
2. `hour` (7.8%)
3. `traffic_lag_24h` (3.6%)
4. `day_of_week` (2.8%)
5. `traffic_rolling_7d` (2.3%)

## Interpretation
The model explained about 89% of the variance in unseen test data (R² = 0.893), showing that traffic is highly autocorrelated — the single best predictor of traffic right now is traffic one hour ago. This is a common and useful insight in telecom forecasting: short-term traffic prediction benefits most from recent history rather than long-term seasonal features. The gap between training R² (0.946) and testing R² (0.893) also shows mild overfitting, a limitation worth addressing (e.g., with regularization or a simpler model) in future iterations.
