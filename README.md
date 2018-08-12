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

## Plot ##

![LR](https://github.com/AdroitAnandAI/stockPrediction/blob/master/Images/stk.PNG)

## Conclusion: ##

We have used the above 3 indicators to train a linear regression model.  **Mean Absolute Error (MAE) is used as an error metric, because it intuitively denotes how "close" we are to the price.** A plot of predicted prices and actual prices on test data is plotted. It is almost linear which means the prediction is working. it can be improved with other models such as randomforest or using engineered features such as previous volume, highest/ lowest price in the past year etc.
