# Zillow Home Values Forecasting (Time Series Analysis)

This repository contains **custom time series utility functions** and a **complete ARIMA modeling workflow** to forecast Zillow home values by state.  
It includes data preprocessing, exploratory time series analysis, stationarity checks, model training, evaluation, and forecasting with confidence intervals.

---

##  Features

### Custom Functions
- **`plot_forecast()`**  
  Plots training data, test data, forecasted values, and confidence intervals.
  
- **`get_adfuller_results()`**  
  Wrapper for the **Augmented Dickey-Fuller (ADF) test** to check stationarity.  
  Returns results as a DataFrame for easier interpretation.

- **`regression_metrics_ts()`**  
  Prints and/or returns regression metrics for time series forecasts:  
  MAE, MSE, RMSE, R², and MAPE (%).

- **`get_sig_lags()`**  
  Finds statistically significant **ACF (Autocorrelation Function)** or **PACF (Partial Autocorrelation Function)** lags.

- **`plot_acf_pacf()`**  
  Plots ACF and PACF with optional annotations for significant lags and seasonal patterns.

---

##  Data

- **Source:** Zillow home values dataset (`zillow_home_values-zipcode.csv`)  
- The data is reshaped into a long format with the following key columns:
  - `RegionID`, `State`, `City`, `Metro`, `CountyName`
  - `Date`, `Home Value`

- Missing values are handled by:
  - Filling categorical columns (`City`, `Metro`, `CountyName`) with defaults
  - Interpolating missing `Home Value` values

- A filtered subset of states is used: **California, Washington, Oregon, Arizona, Nevada**

---

##  Workflow

1. **Preprocessing**  
   - Reshape with `pd.melt`  
   - Handle missing values  
   - Convert `Date` to datetime and set as index  
   - Filter for states of interest and years 2010–2020  
   - Export cleaned data for Tableau visualization

2. **Exploratory Analysis**  
   - Line plots of yearly average home values per state  
   - Seasonal decomposition to assess seasonality  
   - Stationarity check using ADF test

3. **Model Preparation**  
   - Differencing applied (`d=2`) to achieve stationarity  
   - ACF and PACF used to suggest ARIMA order

4. **Modeling**  
   - Initial ARIMA(1,2,1) model  
   - Diagnostics of residuals  
   - Evaluation on 2018 test data (12 months)

5. **Forecasting & Evaluation**  
   - Forecast with confidence intervals  
   - Metrics: R² ≈ 0.982, RMSE ≈ 756, MAE ≈ 690  
   - Auto-ARIMA confirmed ARIMA(1,2,1) as optimal model

6. **Final Forecast**  
   - Predicts 12 months beyond training data (2019)  
   - **~330,500** average home value by end of 2019  
   - **+5.12%** increase compared to start of forecast period

