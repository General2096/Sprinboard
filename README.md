![image](https://user-images.githubusercontent.com/74972980/141377147-6a64b9da-a9bb-4896-9056-fe66ed0f394f.png)

# Bitcoin Cryptocurrency Forecast
You constantly hear both on news/financial outlets and social media about investment in cryptocurrency, more specifically, BItcoin. Bitcoin is a decentralized digital currency that you can buy, sell and exchange directly, without an intermediary like a bank. Bitcoin today is the largest known cryptocurrency in the world holding the largest value. Similar to other cryptocurrencies, the value is extremely volatile, affected by a myriad of factors such as governance, regulation, social media, political influencers, social influences, etc. 

A few examples of influences on Bitcoin price:
1. In March 2021, Tesla announced that it would accept Bitcoin.
2. In September 2021, El Salvador announed it would adopt Bitcoin as a legal tender. 
3. In September 2021, China banned the exchange and trade of all cryptocurrency.

With this constant noise and change in Bitcoin today, can a the price of Bitcoin be predicted with some accuracy, if so, can a financial strategy be formed to assess the investment incentive and duration on the coin and individual for a period of 7 days. In other words, can the price of Bitcoin be predicted 7 days into the future from the end of the dataset with a final say of whether to buy or sell Bitcoin?

## Data Wrangling
Bitcoin's historical price can be found through varying degrees on multiple locations. I chose to use yahoo finance as it obtained a massive history of the coin dating back to September of 2014 from [Yahoo](https://finance.yahoo.com/quote/BTC-USD/history/). The date range has to be manually set to its earliest availability before it can be retrieved. 



## Exploratory Data Analysis
The dataset is very simple and was already organized; missing information was dropped.

Volume trade per day.

![image](https://user-images.githubusercontent.com/74972980/141391946-7de8d5f6-2278-4ba7-86ff-3a8e58e798f9.png)

From the last 120 days, we see the price continues to fluctuate. A decrease in price occurred during the month of September 2021 and has since been on the rise again.

![image](https://user-images.githubusercontent.com/74972980/141381625-7a89def1-6732-47df-af96-c714327fcea5.png)


## Preprocessing and Training
Early model view prediction of the final year of the dataset.
![image](https://user-images.githubusercontent.com/74972980/141381693-c286b76a-0d43-4ac5-a01d-204ae6d653e3.png)

## Modeling
Facebook's Prophet was used for forecasting. The model was fit to the entire dataset and used to preduct the next 100 days. 
![image](https://user-images.githubusercontent.com/74972980/141392825-366cc000-deed-4ba2-8d51-24e10d14d24b.png)

### Model tuning
Parameter of the model were turned that reduced the root mean squared error (RMSE) the most.

## Model Prediction on Historical Data
The training-set is from the beginning up until November 18, 2020, and used to predict the final year of the data. 
![image](https://user-images.githubusercontent.com/74972980/141357303-6d27c37e-040e-42ce-9a43-93fdcc9ff9ef.png)

Showcased below is the 14 days following the end of the training-set
![image](https://user-images.githubusercontent.com/74972980/141357573-7d0284ac-4735-46c6-84e3-dc23faa6e879.png)


## Model Prediction on Future Data
The training set was the entire dataset used to predict the next 100 days from 
![image](https://user-images.githubusercontent.com/74972980/141359612-ab38a48c-1f7f-4aca-9fdc-e24c8edc09c1.png)

Showcased below is the prediction for the 14 days following the end of the dataset
![image](https://user-images.githubusercontent.com/74972980/141376966-ff299bbd-908a-48b4-91ef-348d0bcfe7c3.png)


## Cross Validation
Cross validation performance metrics are visualized for the MAPE(Mean Absolute Percent Error). It measures the size of the error in percentage terms (easy interpretation). It is calculated as the average of the unsigned percentage error.

We see for this forecast that errors around 20% are typical for predictions one month into the future, and that errors increase up to around 100% for predictions that are a 9 months out and decrease to 95% as it gets closer to 1 year.

![image](https://user-images.githubusercontent.com/74972980/141361754-a08d8b7d-fa1c-4606-a32e-38bafa06feaa.png)

## Additional Regressors
The following regressors were added to the model: High, Low, Volume, and Return. Similar to above, the same size training set was used to predict the final year of the dataset.
![image](https://user-images.githubusercontent.com/74972980/141359724-fcc2582d-7734-44da-86ec-7d24681ce0cd.png)

The model performed very well, almost matching the actual output
![image](https://user-images.githubusercontent.com/74972980/141360227-943039ea-f269-4f41-ae8f-21f8590f7545.png)

Set of the predicted and actual for the first and last five days
![image](https://user-images.githubusercontent.com/74972980/141362389-056617b2-817c-4504-ad73-cbd4b5054efe.png)


Similar to above, cross validation was performed again with much better results. 
![image](https://user-images.githubusercontent.com/74972980/141362575-865fa079-7c87-449e-9a0b-ce9e35c6b2a3.png)
We see for this forecast that errors around 1-2% are typical for predictions one month into the future, and that errors increase up to around 4% for predictions that are a 3 months out and decrease to 2% as it gets closer to 4 months.

## Future Work
1. Comparison of different model
