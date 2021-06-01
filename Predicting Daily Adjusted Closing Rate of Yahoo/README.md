# Predicting Daily Adjusted Closing Rate of Yahoo

<img src="https://rapidapi.com/blog/wp-content/uploads/2019/09/stock-chart.jpg"></img>

Janice was the daughter of a millionaire
businessman, and she had approached us after hearing speculations that the market
was expected to grow with escalating economic conditions. She was interested in taking
a long-term risky position to enjoy potentially high returns on investment. However, this
quarter she had seen a dip in her returns despite a good outlook in the capital market.


After having a look at janice's portfolio ,We figured
out that the reason for the mismatch between the portfolio’s return and the expected
returns was a huge residual in Yahoo stock forecasts. This forecast error would have had
a minimal impact had the number of shares been a tiny chunk of the entire portfolio, but
that was not the case in this scenario.

### Plotting Adj Closing rates of Yahoo
![plot1](https://user-images.githubusercontent.com/69857637/120366865-ccb09000-c32d-11eb-8543-705aeeee90d5.png)

We can see definitive upward trend exists. Moreover, it is seen that a seasonality exists (i.e., downward dip), repeating itself every 4.5-month interval.

### Evaluating Stationary Nature

![plot2](https://user-images.githubusercontent.com/69857637/120367324-59f3e480-c32e-11eb-9aec-ef9d2700df1d.png)

Results of Dickey-Fuller Test:

Test Statistics                 -1.106051

p-value                          0.712653

We can see that despite variation in rolling standard deviation being small , rolling mean clearly seems to relatively vary a lot. Hence our time series is non stationary. Moreover , we see that our p-value is greater than 0.05, thus we fail to reject our null hypothesis and accept that our time series is non-stationary.

#### making log transformation

![plot3](https://user-images.githubusercontent.com/69857637/120367339-5e200200-c32e-11eb-8ec3-e8908474f457.png)

 Our best results of non-stationarity was given by lo transformed data. Hence, log transformed data will be used for further analysis.
 
### Estimating Trend and Removing it from original Series
 
At first we need to estimate the trend and then remove it from yahoo stock time series object. We have two great methods of estimating trends.

- Moving Average Smoothing
- Exponentially weighted moving average

**Moving Average Smoothing**

![plot4](https://user-images.githubusercontent.com/69857637/120367980-21083f80-c32f-11eb-81fd-4f639ed75cc0.png)

 The red line shows the rolling mean , i.e. estimated trend from moving averages. Now we have to subtract trend from log transformed time series.We are taking window of 15 because rolling mean for 14 obs are nan.
 
 ![plot5](https://user-images.githubusercontent.com/69857637/120368073-409f6800-c32f-11eb-8a11-b876a014e473.png)

Results of Dickey-Fuller Test:

Test Statistics                 -4.192603

p-value                          0.000678


Now we can see that our rolling mean and rolling std are close to constant an d our hypothesis test is also proving our hypothesis. since p-value < 0.05.
we will go with log transformed trendless time series.

Removing just the trend have given us significant result. Lets try removing both seasonality and trend.

### Removing sesonality and trend

**Differencing**

#### 1st order differencing
![image](https://user-images.githubusercontent.com/69857637/120368393-a390ff00-c32f-11eb-8ef0-c28be61f856a.png)

Results of Dickey-Fuller Test:

Test Statistics               -1.528243e+01

p-value                        4.558437e-28


#### 2nd order differencing

![image](https://user-images.githubusercontent.com/69857637/120368580-daffab80-c32f-11eb-8218-7c64265fa6f2.png)

Results of Dickey-Fuller Test:

Test Statistics                 -5.083676

p-value                          0.000015

#### 3rd order differencing

![image](https://user-images.githubusercontent.com/69857637/120368747-126e5800-c330-11eb-917c-85541930740b.png)

Results of Dickey-Fuller Test:

Test Statistics                 -3.361731

p-value                          0.012335

We can see that 2nd order results are proving much better , our test statistics is also significantly smaller than critical values and our rolling mean and rolling std are also constant.

### Decomposing the time series into trend, seasonality and residuals.

![image](https://user-images.githubusercontent.com/69857637/120368854-32058080-c330-11eb-80bb-1d39d6c5d2da.png)

#### Checking Autocorrelation

The durbin-watson statistics was 2.019 , it means we have no autocorrelation in our time series.

![image](https://user-images.githubusercontent.com/69857637/120368983-54979980-c330-11eb-8afb-038b661edbfd.png)

#### Forecasting

![image](https://user-images.githubusercontent.com/69857637/120369259-a3ddca00-c330-11eb-9ec5-99c0457b1fd3.png)


Our ARIMA model after merging AR and MA models gave a RSS score of 0.0151 which indicates good model.

![image](https://user-images.githubusercontent.com/69857637/120369401-d687c280-c330-11eb-8101-2335017df2ad.png)

------------------------------------------------------------------------------------------------------------------------------------------------------------------










