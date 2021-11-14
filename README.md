![image](https://user-images.githubusercontent.com/74972980/141377147-6a64b9da-a9bb-4896-9056-fe66ed0f394f.png)

# Bitcoin Cryptocurrency Forecast
You constantly hear both on news, financial outlets, social media about investment in cryptocurrency, more specifically, BItcoin. Bitcoin is a decentralized digital currency that you can buy, sell and exchange directly, without an intermediary like a bank. Bitcoin today is the largest known cryptocurrency in the world holding the largest value. Similar to other cryptocurrencies, the value is extremely volatile, affected by a myriad of factors such as governance, regulation, social media, political influencers, social influences, etc. 

A few examples of influences on Bitcoin price:
1. In March 2021, Tesla announced that it would accept Bitcoin.
2. In September 2021, El Salvador announed it would adopt Bitcoin as a legal tender. 
3. In September 2021, China banned the exchange and trade of all cryptocurrency.

With this constant noise and change in Bitcoin today, can a the price of Bitcoin be predicted with some accuracy, if so, can a financial strategy be formed to assess the investment incentive and duration on the coin and individual for a period of 7 days. 

> In other words, can the price of Bitcoin be predicted 7 days into the future from the end of the dataset with some confidence on whether to buy or sell Bitcoin?

## Data Wrangling
Bitcoin's historical price can be found through varying degrees on multiple locations. I chose to use [Yahoo](https://finance.yahoo.com/quote/BTC-USD/history/) finance as it obtained a massive history of the coin dating back to September of 2014. The date range has to be manually set to its earliest availability before it can be retrieved if you are not following the notebook. 

The data is comes in clean and organized for you. Making it easier for those new to interact with.


![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Data%20Wrangling%20-%20Original.png)


## Exploratory Data Analysis
New addition had to be made to the current dataset. First was adding a 'Return' column that was the percentage of change on the 'Adjusted Close' price to the day before. Secondly, a column interpreting the date to the day of the week. With this information we see which days the largest amount of bitcoin trade by volume are conducted. 

The final seven days of the dataset with the inclusion of the added 'Return' and 'Day of Week' columns

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Actual%20Last%207%20days.png)

By grouping the all of the dates through their respective days, we can see; unsurprisingly, the largest day for Bitcoin trade by volume is on Sunday. 

A package called mplfinance was used to create the graph below where the last 120 days were assessed based on price and volume. 

`!pip install mpl_finance` or 

`!pip install --upgrade mplfinance` if you already have the package installed.


![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/EDA%20mplfinance.png)

From the last 120 days, we see the price continues to fluctuate. A decrease in price occurred during the month of September 2021 and has since been on the rise again.


## Preprocessing and Training
> [Prophet](https://facebook.github.io/prophet/) is an open source library published by Facebook that is based on decomposable models. It provides the ability to make time series predictions with good accuracy using simple intuitive parameters and has support for including impact of custom seasonality and holidays! 

Prophet must first be installed. In my case with Python:

`pip install pystan==2.19.1.1` and 

`pip install prophet`.

To see the model in action, without performing any type of tuning, how would the model see the current data? Initial processing and training was conducted on the entire dataset minus the last year which were used for to test the model performance. The black dots represent a specific date, the shaded blue represent the upper and lower uncertainty, and the blue line represents the prediction.

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Preprocessing%20Final%20Year.png)

The model gives a small uncertainty that grows in time, with a ~13,000 value difference by the end of the prediction. This large uncertainty is the same to 'I don't know'. This size prediction will be revisited but strictly for visualization. 


## Modeling
To further see the model's behavior, it was fit to the entire dataset and used to produce the next 100 days.

The overall does a mediocre job of fitting the actual values of the graph. The better fit the graph, a parameter of the model was turned that reduced the root mean squared error (RMSE) the most. The new model does fit the graph slightly better, but additional work needs to be done. For now, we will leave it as is.

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Modeling%20100%20day%20prediction%20tuned.png)


## Model Prediction on Historical Data
Now that we have the tuned model, how well does it perform in determining the final year of the dataset? The model was trained on all but the last 7 days of the dataset; which were then used to test those values. 

![image](https://github.com/General2096/Springboard/blob/main/Capstone%20Project/Images/Modeling%20Actual%20vs.%20Predicted.png)


Showcased below is the 7 days following the end of the training-set.

![image](https://user-images.githubusercontent.com/74972980/141696563-34287bf0-d2f4-48c2-99b8-658f54ad5db8.png)


## Model Prediction on Future Data
Now, this is the stuff we care about. How will the model forecase the future to see if we can turn a profit with Bitcoin investment or stay away from it? The entire dataset was reused to train the model and used to predict the next 100 days. While the goal of this project was just to predict 7 days into the future; 100 day prediction was used to see the potential values of the model might hold. The values that we will look at, will only those 7 days.

Insert image of the graph predition

Insert image of the 7 day table

From the table showcased above, the model predics a continous rise in the value of Bitcoin.

> Based on the prediction, you would invest into Bitcoin and see the value increase for the next 7 days.


## Cross Validation
Now, is it possible the model got lucky with the prediction? Could it have just been luck the values align with what we want them to be and not see potential errors? If those errors are apparent, can they be mitigated. A way to mitigate this is to perform cross validation. With this method, we take multiple sets of the data and measure the forecast error using historical data. 

Cross validation performance metrics are visualized for the MAPE(Mean Absolute Percent Error). It measures the size of the error in percentage terms (easy interpretation). It is calculated as the average of the unsigned percentage error.

Insert image of the plot cross valiadtion metric

We see for this forecast that errors around 20% are typical for predictions one month into the future, and that errors increase up to around 100% for predictions that are a 9 months out and decrease to 95% as it gets closer to 1 year.


## Additional Regressors
We have additional information additionally that was removed in the beginning. Can this be used to increase the prediction power of the model.

The following regressors were added to the model: High, Low, Volume, and Return. Similar to above, the same size training set was used to predict the final year of the dataset.

Insert image of the model prediction of last year

The model performed very well, almost matching the actual output

Insert image of actual vs predicted chart

Set of the predicted and actual for the first and last five days
![image](https://user-images.githubusercontent.com/74972980/141362389-056617b2-817c-4504-ad73-cbd4b5054efe.png)


Similar to above, cross validation was performed again with much better results. 
Insert image of final cross validation chart
We see for this forecast that errors around 1-2% are typical for predictions one month into the future, and that errors increase up to around 4% for predictions that are a 3 months out and decrease to 2% as it gets closer to 4 months.

## Future Work
The model requires a lot of work to take in multiple factors. Other work can include:
1. Comparison of multiple different model.
2. Different strategy outputs such as:
   - How much should you buy based on a budget?
   - If the price is going down, should you sell everything?
   - How much should you sell?
   - At what percentage up or down does the price need to change to warrant the action?
3. Far out introduce webscrapping to see what the talk of Bitcoin is to make better judgement.
