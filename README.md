# Time Series Forecasting - Web Traffic

This is a repository of models built to forecast the web traffic of wikipedia\
pages online. The source data files comes directly from [Kaggle](https://www.kaggle.com/c/web-traffic-time-series-forecasting).

For this project, a time series analysis was performed on the Machine Learning\
wikipedia page (EN) and a forecast model was built using that data using SARIMA\
(see notebook for [code](https://github.com/leekahung/time_series_forecasting_web_traffic/blob/main/notebooks/time_series_modeling_web_traffic.ipynb)).

# Details and Results

The end result of this analysis was a SARIMA model for forecasting web traffic.\
Of the 550 data points in the data set, it accounts for 18 month between July\
2015 and December 2016. The model was made stationary through differencing and\
and was decomposed for seasonal components (7 day cycles). Stationality was\
confirmed visually and statistically through the Dicky-Fuller Test with a\
p-value of 1.3E-12 after first differencing (d=1). Seasonality was removed\
through first seasonal differencing after first differencing.

To obtain the SARIMA model we want for our forecast model, the pmdarima library\
was used to obtain the ordering for p, q, P, and Q. The orderings with the best\
AIC criterion was the SARIMA(2,1,0)(5,1,1)<sub>7</sub>. The residuals are\
somewhat correlated, based on test summaries, Prob(Q) > 0.05. However, this\
could not be helped given its seasonal nature when modeling with ARIMA.

Overall, the one step ahead forecasting is pretty close to that of the actual\
time series it was trained on with a mean absolute error (MAE) of ~471. Dynamic\
forecasting was worse at 2258.

When applied to the unseen test data (the last month of 2016) the forecasted MAE\
came out to be around 603.Most of the forecast line fell within 1 standard\
deviation of the test data with the cyclic peaks being well modeled (minus the\
last week) and the cyclic troughs being qualitatively captured despite its\
underesimate (minus the last week). The final week of the year appears to be a\
unique case where activity decreases, which is reasonable considering it's\
holiday season for many people.

![Image of SARIMA model](https://github.com/leekahung/time_series_forecasting_web_traffic/blob/main/images/time_series_modeling.png)
