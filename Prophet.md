Using base data with no data excluded, ranging from 01/01/2023 to 25/10/2024, with Prophet's holidays configured to GB and changepoint_prior_scale=0.1, the forecast for the following 2 weeks has a correlation of 0.773629146192124 compared to the original manual forecast of 0.810389294726232.

A comparison of the datasets can be found below:
![image](https://github.com/user-attachments/assets/ff4900d3-a5c9-4f50-81fa-71ce8d42de13)

Changing changepoint_prior_scale=1 makes no difference to the accuracy of the forecast. 

Changing changepoint_prior_scale=0.001, which is below the default setting of 0.05, also makes no difference to the forecast.

Exploring changing n_changepoints=50. The default is 25. Changepoints are points in time where the trend of the time series changes significantly. Changing this to 50 changes nothing. Setting it to 100 also changes nothing

