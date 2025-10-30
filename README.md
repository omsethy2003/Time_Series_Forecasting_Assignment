# Time Series Forecasting using SARIMA Model

## 1. Introduction
Time series forecasting is an essential statistical technique used to predict future values based on previously observed data. It plays a crucial role in business, finance, retail, manufacturing, and other industries where understanding future trends is vital for decision-making.

This report presents a comprehensive analysis and forecasting of weekly foot traffic data using the **SARIMA (Seasonal AutoRegressive Integrated Moving Average)** model. The main objective of this project is to identify patterns, trend, and seasonality in the dataset, make the series stationary, and build a robust forecasting model that can predict future customer traffic with reasonable accuracy.

Through this project, the key concepts of **exploratory data analysis (EDA)**, **stationarity testing**, **model identification**, **training–testing split**, **forecasting**, and **performance evaluation** have been applied in a structured workflow.

---

## 2. Dataset Description
The dataset used for this analysis is titled `foot_traffic.csv`, containing 1,000 observations representing weekly average customer visits to a retail store. Each observation corresponds to one week, making the data roughly equivalent to 20 years of weekly traffic data (52 weeks × 20 years ≈ 1,000 points).

Although this dataset is simulated, it closely resembles a real-world time series dataset. The values fluctuate moderately around a mean of approximately 500, showing a slight upward trend and minor variations that mimic realistic business conditions.

The dataset consists of a single numerical column named `foot_traffic`. There is no explicit date column; instead, the row index (0–999) represents sequential weeks. This makes it straightforward to treat the data as a continuous time series.

---

## 3. Exploratory Data Analysis (EDA)
The first step in the analysis involved visualizing the time series to gain insights into its structure. A line plot of the `foot_traffic` variable revealed a mild upward trend and periodic fluctuations, suggesting the presence of seasonality. These features are typical in business or retail data, where customer flow tends to vary cyclically over time.

To formally assess whether the data was stationary, the **Augmented Dickey–Fuller (ADF)** test was applied. The initial test produced a p-value greater than 0.05, indicating non-stationarity. To correct this, first-order differencing was applied. After differencing, the ADF test was repeated and the p-value dropped below 0.05, confirming that the differenced series was now stationary and suitable for modeling.

**Autocorrelation Function (ACF)** and **Partial Autocorrelation Function (PACF)** plots were also generated for the differenced series. These helped identify the lag terms for the ARIMA parameters.

---

## 4. Model Selection and Training
Since the dataset showed both short-term dependencies and potential seasonality, the **SARIMA** model was chosen. Unlike ARIMA, which handles only trend and noise, SARIMA incorporates seasonal effects through additional parameters.

The general form of the SARIMA model is:  
**SARIMA(p, d, q)(P, D, Q, s)**  
where *p, d, q* are the non-seasonal parameters, and *P, D, Q, s* are the seasonal parameters.

For this dataset, a **SARIMA(1,1,1)(1,1,1,52)** model was selected, with *s = 52* representing one year of weekly data.

The data was split into an **80% training set** (first 800 weeks) and a **20% testing set** (last 200 weeks). The model was fitted using the **Maximum Likelihood Estimation** method, and the coefficients confirmed the appropriateness of the selected parameters.

---

## 5. Model Evaluation
After training, the model was evaluated on the test set using **Mean Absolute Error (MAE)** and **Root Mean Squared Error (RMSE)**. Both metrics indicated low errors, meaning the SARIMA model accurately captured both short-term fluctuations and long-term patterns in the data. A comparison plot between actual and forecasted values showed that the predictions closely followed the observed series.

---

## 6. Forecasting Results
Once validated, the model was extended to forecast the next 50 time steps, equivalent to nearly one year of future weekly foot traffic. The forecasts showed a continuation of the general upward trend with periodic fluctuations consistent with the historical data. The confidence intervals widened slightly over time, reflecting natural uncertainty in long-term predictions.

---

## 7. Conclusion
This project successfully implemented a complete time series forecasting workflow. The SARIMA model effectively modeled both short-term and seasonal dependencies. The analysis confirmed that the data exhibited trend and seasonality, which were appropriately handled through differencing and seasonal modeling.

The methodology used in this project can be applied to a wide range of real-world forecasting tasks such as sales forecasting, demand estimation, and website traffic prediction. Overall, the SARIMA model proved reliable, interpretable, and accurate for the given dataset.

---

## 8. References
1. [Statsmodels Documentation](https://www.statsmodels.org/)  
2. VanderPlas, J. (2016). *Python Data Science Handbook*. O’Reilly Media.  
3. [Kaggle Datasets – Publicly available time series data sources](https://www.kaggle.com/)
