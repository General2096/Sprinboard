# Sprinboard

## Bitcoin Cryptocurrency Forecast

# Data
Bitcoin's historical price can be found through varying degrees on multiple locations. I chose to use yahoo finance as it obtained the a large history of the coin dating back to September of 2014 from the following link. The date range has to be manually set before it can be retrieved. 
Link: https://finance.yahoo.com/quote/BTC-USD/history/

# Exploratory Data Analysis
Most of the datset was already organized and cleaned, 5 days had missing information and were dropped. 

# Preprocessing and Training

# Modeling
Facebook's Prophet was used for forecasting. The model was fit to the entire dataset and used to preduct the next 100 days. 


# Model tuning


# Model Prediction on Historical Data
The training-set is from the beginning up until November 18, 2020, and used to predict the final year of the data. 
![image](https://user-images.githubusercontent.com/74972980/141357303-6d27c37e-040e-42ce-9a43-93fdcc9ff9ef.png)

Showcased below is the 14 days following the end of the training-set
![image](https://user-images.githubusercontent.com/74972980/141357573-7d0284ac-4735-46c6-84e3-dc23faa6e879.png)


# Model Prediction on Future Data
The training set was the entire dataset used to predict the next 100 days from 
![image](https://user-images.githubusercontent.com/74972980/141359612-ab38a48c-1f7f-4aca-9fdc-e24c8edc09c1.png)

Showcased below is the prediction for the 14 days following the end of the dataset
![image](https://user-images.githubusercontent.com/74972980/141359248-1d617b03-3a90-4063-9733-c8bd5e433975.png)

# Cross Validation
Cross validation performance metrics are visualized for the MAPE(Mean Absolute Percent Error). It measures the size of the error in percentage terms (easy interpretation). It is calculated as the average of the unsigned percentage error.

We see for this forecast that errors around 20% are typical for predictions one month into the future, and that errors increase up to around 100% for predictions that are a 9 months out and decrease to 95% as it gets closer to 1 year.

![image](https://user-images.githubusercontent.com/74972980/141361754-a08d8b7d-fa1c-4606-a32e-38bafa06feaa.png)

# Additional Regressors
The following regressors were added to the model: High, Low, Volume, and Return. Similar to above, the same size training set was used to predict the final year of the dataset.
![image](https://user-images.githubusercontent.com/74972980/141359724-fcc2582d-7734-44da-86ec-7d24681ce0cd.png)

The model performed very well, almost matching the actual output
![image](https://user-images.githubusercontent.com/74972980/141360227-943039ea-f269-4f41-ae8f-21f8590f7545.png)

Set of the predicted and actual for the first and last five days
![image](https://user-images.githubusercontent.com/74972980/141362389-056617b2-817c-4504-ad73-cbd4b5054efe.png)


Similar to above, cross validation was performed again with much better results. 
![image](https://user-images.githubusercontent.com/74972980/141362575-865fa079-7c87-449e-9a0b-ce9e35c6b2a3.png)
We see for this forecast that errors around 1-2% are typical for predictions one month into the future, and that errors increase up to around 4% for predictions that are a 3 months out and decrease to 2% as it gets closer to 4 months.

# Future Work
1. Comparison of different model
