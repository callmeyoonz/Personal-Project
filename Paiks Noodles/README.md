📊 Paik's Noodles — Restaurant Revenue Forecasting
Tools: Python · pandas · statsmodels · matplotlib · scikit-learn
I work part-time at a Korean noodle restaurant in the Netherlands. I had access to 13 months of real POS sales data (March 2025 – March 2026) and decided to build a forecasting model from scratch as a self-learning exercise.
The analysis is split into two parts:

OLS regression (log_revenue ~ weekday + is_peak) — confirm that weekday and seasonality effects are statistically real
State space model (UCM) with exogenous regressors — model the full time series and forecast April 2026 daily revenue

What I did:

Parsed raw monthly Excel blocks from the POS export and engineered features (is_peak, is_holiday via the Dutch holidays package)
Confirmed strong weekday effects via OLS (weekend coefficients significant at p < 0.001)
Fit an Unobserved Components Model decomposing revenue into a local level, weekly seasonal, and AR(1) component
Improved forecast MAPE from 31.9% → 21.3% on a held-out April 2026 test set by adding peak-season and public holiday indicators as exogenous regressors
Investigated a peak × weekend interaction term but rejected it after identifying data scarcity as the root cause (~44 peak-season weekend days in training)
Validated model fit through residual diagnostics (Ljung-Box, Q-Q plot, ACF) and confirmed well-calibrated uncertainty: 94.1% of actuals fell inside the 95% confidence interval

What I learned:

How to think carefully about what a model can't know (weather, walk-ins, one-off events) and how that sets a realistic floor on MAPE
That a more complex model isn't always better — and being able to explain why it isn't is just as important as building it
End-to-end pipeline from messy real-world data to a validated forecast
