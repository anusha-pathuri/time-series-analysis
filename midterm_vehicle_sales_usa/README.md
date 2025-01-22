# Unveiling the Dynamics of Historical Vehicle Sales in the U.S.

## Motivation

The automotive industry is a crucial sector of the U.S. economy, contributing significantly to employment, economic output, and innovation. Vehicle sales data serves as a key economic indicator, often reflecting the broader health of the economy. Trends in vehicle sales can be influenced by various factors, including economic cycles, consumer confidence, fuel prices, and technological advancements. Understanding these trends is vital for stakeholders ranging from policymakers to manufacturers and dealers.

With this motivation, we carry out a time series analysis guided exploration of the U.S. vehicle market. The dataset for this project is sourced from the U.S. Bureau of Economic Analysis (BEA) and records the total vehicle sales in the United States, measured on a monthly basis from January 1, 1976, to January 1, 2024 ([U.S. Bureau of Economic Analysis, Total Vehicle Sales \[TOTALNSA\], retrieved from FRED, Federal Reserve Bank of St. Louis](https://fred.stlouisfed.org/series/TOTALNSA)). This longitudinal data spans nearly five decades, offering a robust foundation for analyzing temporal patterns, trends, and cyclical behaviors in vehicle sales.

![image](https://github.com/user-attachments/assets/3b2a4006-39f6-4704-88ae-3ac87d82c7a7)


## Methods

We start by looking at the sample autocorrelation function (ACF), which reveals a periodic pattern in the data:

<p align="center">
<img src="https://github.com/user-attachments/assets/2843a204-c117-486d-8406-6fe8f4a5a7ab" alt="acf-pacf" width="800" />
</p>

From the Seasonal and Trend Decomposition by Loess (STL Decomposition), we observe non-stationarity, which we handle by de-trending the data:

<p align="center">
<img src="https://github.com/user-attachments/assets/dd63146e-8bf0-4102-8ff6-67cd34c35e64" alt="detrending" />
</p>

We then conduct a spectral analysis using a smoothed periodogram to determine the periodicity of fluctuations in the de-trended data:

<p align="center">
<img src="https://github.com/user-attachments/assets/aa71ab14-9af4-45db-8db7-61432f8f98cf" alt="smoothed-periodogram" width="500" />
</p>

-  The dominant frequency is 0.0833 cycles per month, which corresponds to an estimated seasonal period of 1 year.

These insights guide our modeling decisions. We start with the class of autoregressive moving average (ARMA) models and then incorporate seasonal influences using SARMA. Through meticulous exploration and model fitting, the optimal SARMA model is determined to be a **$\mathrm{SARIMA}((1,0,0)×(3,0,2)_{12})$**. This is the model that achieves maximal predictive power as measured by the Akaike Information Criterion (AIC) which balances goodness of fit and model complexity.

![image](https://github.com/user-attachments/assets/ee8cdb9e-236b-4dbb-89f2-15d5717840e6)



## Conclusion

Time series analysis provides valuable insights into the historical patterns of total vehicle sales, allowing us to understand trends, seasonality, and periodicity, and build time series models. This project in particular underscores the efficacy of SARMA in modeling vehicle sales. Now that we have understood our data, the next logical step would be to use it as a forecasting tool to guide decision-making and future planning in the automotive industry. 

However, external factors such as economic conditions, consumer confidence, industry innovation, regulatory changes and other unforeseen events (pandemics!) play an important role in affecting vehicle sales. These factors may introduce fluctuations and changes that may not be predicted by purely historical data. So while time series analysis is a powerful tool for understanding past behavior, a comprehensive analysis must also consider the broader context affecting the automotive industry.
