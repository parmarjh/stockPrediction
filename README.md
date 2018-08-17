# Stock Prediction #

## Objective ## 

In this project, we'll be working with data from the S&P500 Index. The S&P500 is a stock market index. Stocks are traded daily, and the price can rise or fall from the beginning of a trading day to the end based on demand. Indexes aggregate the prices of multiple stocks together, and allow you to see how the market as a whole is performing. For example, the Dow Jones Industrial Average aggregates the stock prices of 30 large American companies together. The S&P500 Index aggregates the stock prices of 500 large companies. 

**We'll be using historical data on the price of the S&P500 Index to make predictions about future prices.** Predicting whether an index will go up or down will help us forecast how the stock market as a whole will perform. **Since stocks tend to correlate with how well the economy as a whole is performing, it can also help us make economic forecasts. **

Traders who make money by buying and selling Exchange Traded Funds (ETFs) buy and sell indexes like stocks. An accurate forecast would help the traders "buy" S&P500 Index ETF when the price is low, and sell when it's high, to make profit.

In this mission, **we’ll be working with a csv file containing index prices. Each row in the file contains a daily record of the price of the S&P500 Index from 1950 to 2015**. The dataset is stored in sphist.csv.

Data Source: https://github.com/AdroitAnandAI/stockPrediction/blob/master/sphist.csv

## Attribute Information ##

The columns of the dataset are:
* Date -- The date of the record.
* Open -- The opening price of the day (when trading starts).
* High -- The highest trade price during the day.
* Low -- The lowest trade price during the day.
* Close -- The closing price for the day (when trading is finished).
* Volume -- The number of shares traded.
* Adj Close -- The daily closing price, adjusted for corporate actions.

## Analysis ##

**We’ll be using this dataset to develop a predictive model. We’ll train the model with data from 1950-2012, and try to make predictions from 2013-2015.**

Stock market data is sequential, and each observation comes a day after the previous observation. Thus, the observations are not all independent. Hence we must be careful not to inject future knowledge, otherwise it will just make our model look good but when you're training and testing it, but will make it fail in the real world. The time series nature of the data means that can generate indicators. 

**Hence we have created new columns** that contains:
* The **average price** for the past 365 days.
* The **ratio between the average price** for the past 5 days, and the average price for the past 365 days.
* The **standard deviation of the price** over the past 365 days

## Prediction of Stock Prices: Week Ahead ##

To predict % change in stock price after a week, we can use features averaging previous ’n’ days coupled with % change in stock price after a week, as the response variable, y as training data. In test data also, a 7-day forward shift in the closing price is introduced to compare the % change against prediction.

### Plot ###

![stkwk](https://github.com/AdroitAnandAI/stockPrediction/blob/master/Images/stkweek.PNG)

Mean Absolute Error (MAE) = 1.4682141984586512
Median Absolute Percentage Error (MAPE) = 93.0%

## MAE vs MAPE Error Metric ##

MAE error metric is not interpretable, since the value of MAE can range from 0 to infinity. We can’t understand how good the model performed. Hence it would be better to compute Percentage error and even better would be to compute median (instead of mean) so that the perturbation caused by outliers could be eliminated. Median Absolute Percentage Error (MAPE) would be a far more intrepretable metric, resilient to outliers.

## Prediction of Stock Prices: Day Ahead ##

Percentage error for weekly prediction is unacceptably high. This was expected as stock prediction is an extremely hard problem, to get even a better than random model. Lets try to predict % change in stock price prior to a day. We can use features, mean and standard deviation of previous 365 days & The ratio between the average price for the past 5 days, and the average price for the past 365 days. The response variable, y, would be the closing price. A 1-day forward shift in the closing price, so that the closing price of the present day (future data) shouldn’t be included in prediction.

### Plot ###

![stk](https://github.com/AdroitAnandAI/stockPrediction/blob/master/Images/stk.PNG)

Mean Absolute Error (MAE) = 98.94921147104225
Median Absolute Percentage Error (MAPE) = 6.0%

** MAPE of 6.0% is a much better prediction result than the previous weekly prediction attempt.**

## Conclusion: ##

1. In daily forecast, Actual and Predicted prices are almost linear. Hence the daily prediction model is working fine, though the error can be further reduced with a better model such as randomforest or using feature engineering techniques such as previous volume, highest/ lowest price in the past year etc.

2. For a financial company, another way to reframe this problem would be to perceive the problem as a classification problem, instead of regression problem. If we can predict, whether the price of a particular stock would go up or down, on next day or a period of time
then such a system is very useful.

3. There was a Kaggle competition on similar lines and all of the good solutions just predicted 0% change in price most of the times.

## Potential Improvements ##

1. Learn the domain more and engineer very domain specific features.

2.  Implement this paper for a Deep Learning based momentum trading strategy: Applying Deep Learning To Enhance Momentum Trading Strategies In Stocks by Lawrence Takeuchi

http://cs229.stanford.edu/proj2013/TakeuchiLee-ApplyingDeepLearningToEnhanceMomentumTradingStrategiesInStocks.pdf
