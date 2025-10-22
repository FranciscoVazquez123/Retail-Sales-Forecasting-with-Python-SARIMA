# Retail Sales Forecasting with Python & SARIMA


## Executive Summary

This project analyzes historical sales data from a superstore (2015-2018) to develop a predictive forecasting model for monthly sales. By leveraging time series analysis techniques, we successfully identified strong annual seasonality and a consistent upward trend in sales.

A **SARIMA (Seasonal Autoregressive Integrated Moving Average)** model was developed, configured, and trained on data from 2015-2017. The model's predictive accuracy was then validated against the unseen data from 2018, achieving a final **Root Mean Squared Error (RMSE) of 11025.29**. The resulting forecast closely tracked the actual sales data, proving its capability to capture complex seasonal patterns. The final deliverable is a validated forecasting tool that serves as a foundational component for data-driven decision-making.

---

## Business Problem

A large retail company experiences fluctuating sales, making it difficult to plan for inventory effectively. This results in two costly problems:

* **Overstocking:** Excess capital is tied up in inventory that isn't selling, leading to high holding costs and potential obsolescence.
* **Stockouts:** Underestimating demand for popular products leads to lost sales and customer dissatisfaction.

The company's current planning relies on simple historical averages, which fail to account for complex growth trends and seasonal spikes in demand. The business objective is to answer the question: **"Can we accurately forecast future sales to create a more efficient and proactive planning strategy?"**

---

## Data Source

The dataset used for this project is the **"Superstore Sales Dataset"** (commonly found on Kaggle). It contains 9,800 sales records from a US-based superstore, spanning from 2015 to 2018.

* **File:** `train.csv`
* **Key Columns Used:** `Order Date`, `Sales`

---

## Methodology

This project was conducted in a Jupyter Notebook. The time series analysis followed these sequential steps:

1.  **Data Loading & Preprocessing:**
    * Loaded the `train.csv` dataset into a pandas DataFrame.
    * Converted the `Order Date` column from an `object` type to a `datetime` format.
    * Aggregated the data by month (using `.resample('MS')`) to create a stable, monthly time series.

2.  **Exploratory Data Analysis (EDA):**
    * Plotted the monthly sales data to visually confirm a strong upward **trend** and a clear annual **seasonality**.
    * Used `statsmodels.tsa.seasonal_decompose` to formally separate the time series into its Trend, Seasonal, and Residual components.

3.  **Stationarity Check:**
    * Performed the **Augmented Dickey-Fuller (ADF) Test** on the monthly data to check for stationarity, which is a prerequisite for many time series models.

4.  **Model Identification & Training:**
    * Plotted the **Autocorrelation Function (ACF)** and **Partial Autoregulation Function (PACF)** to identify optimal parameters for the SARIMA model.
    * Split the data into a **training set** (Jan 2015 - Dec 2017) and a **test set** (Jan 2018 - Dec 2018).
    * Defined and trained the `SARIMAX` model on the training data.

5.  **Model Evaluation:**
    * Used the trained model to forecast sales for the 12-month period of the test set.
    * Calculated the **Root Mean Squared Error (RMSE)** to quantify the model's prediction error against the actual 2018 sales data.

---

## Key Findings

* **Seasonal Pattern:** The time series decomposition revealed a clear seasonal pattern in the monthly sales data, with peaks typically occurring towards the end of the year. This suggests that sales are strongly influenced by cyclical factors within a 12-month period.
* **Trend:** An upward trend was observed in the overall sales data from 2015 to 2017, indicating a general growth in sales over this period.
* **Stationarity:** The Augmented Dickey-Fuller (ADF) test confirmed that the monthly sales series is stationary (p-value < 0.05), which is a necessary condition for applying many time series forecasting models.
* **SARIMA Model Performance:** The SARIMA(1, 0, 1)(1, 1, 0, 12) model was fitted to the training data, yielding a Root Mean Squared Error (RMSE) of approximately 15309.69 on the test set. This metric provides a quantitative measure of the model's forecasting accuracy.

---

## Business Recommendations

Based on the validated forecasting model, the following actions are recommended:

* **Integrate the Forecast:** Use the model to generate a 12-month rolling forecast for sales targets and financial budgeting.
* **Inform Procurement:** Share the forecast with the purchasing department to anticipate seasonal demand spikes, allowing them to negotiate better prices and secure capacity in advance.
* **Dynamic Inventory Planning:** Use the forecast as the primary input for inventory models to move from a reactive to a proactive inventory policy.
