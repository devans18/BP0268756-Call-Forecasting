**Forecast 1:** Using base data with no data excluded, ranging from 01/01/2023 to 25/10/2024, with Prophet's holidays configured to GB and changepoint_prior_scale=0.1, the forecast for the following 2 weeks has a correlation of 0.930597300083405 compared to the original manual forecast of 0.975367148696651.

A comparison of the datasets can be found below:
![image](https://github.com/user-attachments/assets/ff4900d3-a5c9-4f50-81fa-71ce8d42de13)

**Forecast 2:** Changing changepoint_prior_scale=1 makes no difference to the accuracy of the forecast. 

**Forecast 3:** Changing changepoint_prior_scale=0.001, which is below the default setting of 0.05, also makes no difference to the forecast.

**Forecast 4:** Exploring changing n_changepoints=50. The default is 25. Changepoints are points in time where the trend of the time series changes significantly. 
**Forecast 5:** Setting it to 100 also changes in the base forecast, however there is more definition to yhat_upper. 
**Forecast 6:** Attempting with 1000 as the value produces no change.

**Forecast 7:** Forcing seasonality also makes no change.

**Forecast 8:** _EUREKA!_ A breakthrough that has caused the forecast to change and add some detail to the daily pattern is adding a custom seasonality of "daily" using the following code --> m.add_seasonality(name="intraday", period=1, fourier_order=15)
Here it sets a seasonality period of 1, the period being in days, and configures the fourier_order. From the Prophet Github "For reference, by default Prophet uses a Fourier order of 3 for weekly seasonality and 10 for yearly seasonality.", https://facebook.github.io/prophet/docs/seasonality,_holiday_effects,_and_regressors.html#specifying-custom-seasonalities.

The science behind this is linked to Fourier Series, a mathematical technique that allows us to represent any periodic function as a sum of sine and cosine functions. In simpler terms, it's a way to decompose a complex wave into a series of simpler sine and cosine waves. The more complex a fourier series, the higher the order and in turn, the **N**umber of partial sums. 

![image](https://github.com/user-attachments/assets/5f2ecaf4-b916-48aa-9cbe-c3ccf16b7295)

As a result of defining the "intraday" seasonality with fourier_order=15, the correlation between the forecast and the actuals increases from 0.930597300083405 to 0.933950189798526, a marginal yet noticable increase. 

**Forecast 9:** Increasing the Fourier_order to 30 results in an increase to 0.935389595
![image](https://github.com/user-attachments/assets/8afd4bc6-3ff9-433e-a48f-2134d8f159ba)

**Forecast 10:** Testing the model to a further extreme, setting the Fourier_order to 100 results in a drop in correlation to 0.935212166507764 and appears it may be overfitting the model. 

**Forecast 11:** Reviewing what happens if daily_seasonality=False, weekly_seasonality=20 and intraday fourier_order=100, the correlation increases to 0.970932007232751
![image](https://github.com/user-attachments/assets/b097f424-332a-4bcf-af54-1c9a5a4b0f51)

**Forecast 12:** Turning daily_seasonality back to True, results in a slight reduction in correlation to 0.970925272350753

**Forecast 13:** Setting the weekly_seasonality=50, the correlation increases again to 0.971895510395694

**Forecast 14:** Establishing a custom monthly seasonality m.add_seasonality(name="monthly", period=30.5, fourier_order=50) and adjusting the daily, weekly and monthly fourier_orders to 50. This results in a correlation of 0.960054641115374. Processing time has increased to 4 minutes.

**Forecast 15:** Turning these fourier_orders up to 100, correlation is decreased to 0.959567980256983. Processing time is now 7 minutes.
