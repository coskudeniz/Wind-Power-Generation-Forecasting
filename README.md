# Wind-Power-Generation-Forecasting
Forecasting wind power generation using regression models

## Aim
The aim of this task is to be able to predict wind power generation based on different features. This is a regression problem. A basic learning algorithm for regression, linear regression with L1 regularization (Lasso) is fit to the given dataset. Root mean squared error is minimized but other metrics like R2 score can be optimized as well.

## Data
The dataset that you can find under the data folder is an actual dataset of power generation taken from a wind power plant. The dataset consists of hourly weather and energy production values. The training data consists of 36355 data points and the test data consists of 2928 data points. However, there are data points with missing values in the training set and all the columns for those data points are missing so they cannot be used for training. Those missing values are dropped and after dropping them, there are 33427 data points in the training set. 

There are duplicated values for the dates 2013-10-27 03:00:00 and 2015-11-08 03:00:00 in the training set. The reason for these duplicated values is because of changes in the hours for the purpose of daylight saving. These are corrected and some exploratory analysis is done to see which features are correlated with each other and with the target. The details can be found in the notebook provided. After the duplicated values are dropped, there are 33425 data points in the training set. 

The dataset consists of the features 'AppTemperature', 'Temperature', 'CloudCover', 'DewPoint', 'Humidity', 'Pressure', 'WindBearing', 'WindSpeed' and 'Prod'. 'Prod' is the target and the values in the 'Prod' column are the hourly generated power. The time frame is from 2013-04-01 03:00:00 to 2017-09-30 23:00:00 for the training dataset and from 2017-10-01 00:00:00 to 2018-01-31 23:00:00 for the test dataset.

## Linear Regression
Linear models are good when there are a lot of features compared to the data points and for sparse datasets like text data (This is not the case here). They can be used with large amounts of data since they can be trained quickly. By training a linear model quickly, the problems can be analyzed like underfitting or overfitting and the best way to proceed can be figured out. However, some preprocessing should be done to get the features ready for linear regression. One hot encoded features are created for the months, hours and days information in the dataset. Also, the interactions between these features are studied as well and fed into a linear regression model. The reason for doing this is that, instead of learning one coefficient for all months, days and hours, the linear model can learn different coefficients for each separate month, hour and day as well as the interactions between them. This approach can help linear models but will not make much of a difference for more complex models like ensembles of trees or deep learning models.

L1 regularization results in sparse features due to the addition of the absolute values of the weights into the squared error loss function. By trying to minimize this new loss function, some weights are set to 0. The strength of regularization can be adjusted by the alpha parameter. Higher values will result in more regularization. As can be seen in the Jupyter notebook that is included, most of the coefficients are set to 0 for most of the features. The wind speed is the feature with the highest correlation with the target variable (produced energy) and Lasso model assigned the highest coefficient to this feature. Grid Search is used for selecting the best regularization parameter using cross-validation. Since this is a time-series dataset, cross-validation is done based on time using the TimeSeriesSplit cross-validation object of Scikit-Learn module. 

Also, a linear regression model without any regularization is fit. The results can be observed in the Jupyter notebook. The resuts are worse compared to the Lasso model.

The other regularization techniques used were L2 regularization (Ridge) and elasticnet which combines L1 and L2 regularization. 
