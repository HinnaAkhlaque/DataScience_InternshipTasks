**Task-3: Household Energy Consumption Time Series Forecasting**
 
**Project Overview:** <br>
This project focuses on forecasting short-term household energy consumption using historical time-series data. The goal was to analyze temporal consumption patterns and compare the performance of multiple forecasting techniques, including statistical, probabilistic, and machine learning approaches.<br>
<br>
**Task Objective:** <br>
The main objectives of this project were to:<br>
<br>
Parse and preprocess time-series energy consumption data<br>
Resample energy usage into hourly intervals<br>
Engineer temporal features such as:<br>
Hour of the day<br>
Day of the week<br>
Weekend indicators<br>
Lag features<br>
Rolling averages<br>
<br>
Implement and compare multiple forecasting models:<br>
ARIMA<br>
Prophet<br>
XGBoost<br>
<br>
Evaluate model performance using:<br>
Mean Absolute Error (MAE)<br>
Root Mean Squared Error (RMSE)<br>
Visualize actual vs forecasted household energy consumption<br>

**Approach:** <br>
1. Data Preprocessing<br>
The dataset was loaded and cleaned by:
<br>
Handling missing values (?)<br>
Converting energy consumption values to numeric format<br>
Parsing date and time columns into a datetime index<br>
Resampling the data into hourly averages<br>
<br>
The target variable used for forecasting was: Global_active_power<br>
<br>
_2. Feature Engineering_<br>
To improve forecasting performance, several time-based and historical features were created:<br>
Temporal Features
Hour of day<br>
Day of week<br>
Month<br>
Weekend/weekday indicator<br>
<br>
Lag Features<br>
Previous energy consumption values were included to help the models learn temporal dependencies.
<br>
Examples:<br>
Lag 1 hour<br>
Lag 24 hours<br>

Rolling Statistics<br>
A 24-hour rolling mean was added to capture short-term trends and smooth fluctuations.<br>

_3. Forecasting Models_<br>
**ARIMA**<br>
ARIMA(p,d,q)<br>
ARIMA was used as a traditional statistical baseline model for time-series forecasting. It captures autoregressive and moving-average relationships in sequential data.<br>
**Prophet**<br>
Prophet was used to model trend and seasonality patterns in household energy consumption.<br>
**XGBoost**<br>
XGBoost was implemented as a machine learning forecasting model using engineered temporal features.<br>

**Results and Findings:**<br>
Model Performance<br>

| Model   | MAE    | RMSE   |
| ------- | ------ | ------ |
| ARIMA   | 0.6845 | 0.9066 |
| Prophet | 0.7073 | 0.9421 |
| XGBoost | 0.3187 | 0.4918 |

**Key Findings:**<br>

*XGBoost Achieved the Best Performance*<br>
XGBoost significantly outperformed both ARIMA and Prophet models.
<br>
Reasons for Better Performance:<br>
Successfully captured nonlinear energy consumption behavior<br>
Leveraged engineered temporal features effectively<br>
Modeled short-term fluctuations and spikes more accurately<br>
<br>
*ARIMA Performance*<br>
ARIMA was able to capture the general trend of household energy usage but struggled with highly volatile fluctuations and nonlinear patterns.<br>
*Prophet Performance*<br>
Prophet successfully modeled recurring seasonal trends and daily cycles but produced smoother forecasts than the actual observations.<br>

**Conclusion:**<br>

This project demonstrated the effectiveness of machine learning approaches for short-term household energy forecasting.
<br>
Among all evaluated models, XGBoost produced the most accurate forecasts with the lowest MAE and RMSE values. The results indicate that combining feature engineering with machine learning techniques provides superior forecasting performance compared to traditional statistical methods.
