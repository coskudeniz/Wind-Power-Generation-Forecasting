# Wind-Power-Generation-Forecasting
Forecasting wind power generation using regression models

## Aim
The aim of this task is to be able to predict wind power generation based on different features. This is a regression problem. A basic learning algorithm for regression, linear regression with L1 regularization (Lasso) is fit to the given dataset. Root mean squared error is minimized but other metrics like R2 score can be optimized as well.

## Data
The dataset that you can find under the data folder is an actual dataset of power generation taken from a wind power plant. The dataset consists of hourly weather and energy production values. The training data consists of 36355 data points and the test data consists of 2928 data points. However, there are data points with missing values in the training set and all the columns for those data points are missing so they cannot be used for training. Those missing values are dropped and after dropping them, there are 33427 data points in the training set. 

The dataset consists of the features 'AppTemperature', 'Temperature', 'CloudCover', 'DewPoint', 'Humidity', 'Pressure', 'WindBearing', 'WindSpeed' and 'Prod'. 'Prod' is the target and the values in the 'Prod' column are the hourly generated power. 

There are duplicated values for the dates 2013-10-27 03:00:00 and 2015-11-08 03:00:00 in the training set. The reason for these duplicated values is because of changes in the hours for the purpose of daylight saving. These are corrected and some exploratory analysis is done to see which features are correlated with each other and with the target. The details can be found in the notebook provided.
