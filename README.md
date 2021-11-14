![image](https://user-images.githubusercontent.com/74972980/141377147-6a64b9da-a9bb-4896-9056-fe66ed0f394f.png)

# Bitcoin Cryptocurrency Forecast
You constantly hear both on news, financial outlets, and social media about investment in cryptocurrency, more specifically, Bitcoin. Bitcoin is a decentralized digital currency that you can buy, sell and exchange directly, without an intermediary like a bank. Bitcoin today is the largest known cryptocurrency in the world holding the largest value. Similar to other cryptocurrencies, the value is extremely volatile, affected by a myriad of factors such as governance, regulation, social media, political influencers, social influences, etc. 

A few examples of influences on Bitcoin price:
1. In March 2021, Tesla announced that it would accept Bitcoin.
2. In September 2021, El Salvador announed it would adopt Bitcoin as a legal tender. 
3. In September 2021, China banned the exchange and trade of all cryptocurrency.

With this constant noise and change in Bitcoin today, can a the price of Bitcoin be predicted with some accuracy, if so, can a financial strategy be formed to assess the investment incentive and duration on the coin and individual for a period of 7 days. 

> In other words, can the price of Bitcoin be predicted 7 days into the future from the end of the dataset with some confidence to decide whether an investor should buy or sell Bitcoin?

## Data Wrangling
Bitcoin's historical price can be found through varying degrees on multiple locations. I chose to use [Yahoo](https://finance.yahoo.com/quote/BTC-USD/history/) finance as it obtained a massive history of the coin dating back to September of 2014. The date range has to be manually set to its earliest availability before it can be retrieved if you are not following the notebook. 

The data is comes in clean and organized for you. Making it easier for those new to interact with.


![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Data%20Wrangling%20-%20Original.png)


## Exploratory Data Analysis
New additions had to be made to the current dataset. First was adding a 'Return' column that was the percentage of change on the 'Adjusted Close' price to the day before. Secondly, a column interpreting the date to the day of the week. With this information we see which days the largest amount of bitcoin trade by volume are conducted. 

The final seven days of the dataset with the inclusion of the added 'Return' and 'Day of Week' columns.

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Actual%20Last%207%20days.png)

By grouping all of the dates through their respective days, we can see; unsurprisingly, the largest day for Bitcoin trade by volume is on Sunday. Unlike the traditional stock market, cryptocurrencies can be traded 24/7 as the market is always open, generally an infinite amount of times. Sunday tends to be the day people are relaxing and have more time to be involved in things not in their everyday life, such as investing. 

A package called mplfinance was used to create the graph below where the last 120 days were assessed based on price and volume. 

`!pip install mpl_finance` or 

`!pip install --upgrade mplfinance` if you already have the package installed.


![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/EDA%20mplfinance.png)

From the last 120 days, we see the price continues to fluctuate. The potential direction of each price is easily viewed based on the color and range of each value. A decrease in price occurred during the month of September 2021 and has since been on the rise again.


## Preprocessing and Training
> [Prophet](https://facebook.github.io/prophet/) is an open source library published by Facebook that is based on decomposable models. It provides the ability to make time series predictions with good accuracy using simple intuitive parameters and has support for including impact of custom seasonality and holidays! 

Prophet must first be installed. In my case with Python:

`pip install pystan==2.19.1.1` and 

`pip install prophet`.

To see the model in action, without performing any type of tuning, how would the model see the current data? Initial processing and training was conducted on the entire dataset minus the final year which were used for to test the model performance. The black dots represent a specific date, the shaded blue represent the upper and lower uncertainty, and the blue line represents the prediction.

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Preprocessing%20Final%20Year.png)

The model gives a small uncertainty that grows in time, with a ~13,000 value difference by the end of the prediction. This large uncertainty is the same to 'I don't know'.


## Modeling
To further see the model's behavior, it was fit to the entire dataset and used to produce the following year.

The overall model does a mediocre job of fitting the actual values of the graph. To better fit the graph, a parameter of the model was tuned that reduced the root mean squared error (RMSE) the most. The new model does fit the graph slightly better, but additional work needs to be done. For now, we will leave it as is.

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Modeling%20100%20day%20prediction%20tuned.png)


## Model Prediction on Historical Data
Now that we have the tuned model, how well does it perform in determining the final year of the dataset? The model was trained on all but the last 7 days of the dataset; which were then used to test the remaining values. 

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Modeling%20Actual%20vs.%20Predicted.png)

While the predicted values see a small increase each day, the predicted values continue to highly underperform on each day.

Showcased below is the 7 days following the end of the training-set.

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Final%207%20day%20forecast.png)


## Model Prediction on Future Data
Now, this is the stuff we care about. How will the model forecast the future to see if we can turn a profit with Bitcoin investment or stay away from it? The entire dataset was reused to train the model and used to predict the next 7 days. 

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Modeling%207%20day%20future.png)


> Based on the prediction, if you invest into Bitcoin by the end of October 18, 2021, you would see the value increase for the next 7 days.

Even on the lower end of uncertainty, you would still see an increase in price following the seven days from the initial investment. 

## Future Work
The model requires a lot of work to take in multiple factors. Other work can include:
1. Comparison of multiple different model.
2. Different strategy outputs such as:
   - How much should you buy based on a budget?
   - If the price is going down, should you sell everything?
   - How much should you sell?
   - At what percentage up or down does the price need to change to warrant the action?
3. Far out introduce webscrapping to see what the talk of Bitcoin is to make better judgement.
