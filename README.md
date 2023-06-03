# Bulldozer_price_prediction

This dataset is taken from a kaggle competion. The aims of competition was to predict the auction sale price for a piece of heavy equipment to create a "blue book" for bulldozers. The project is based on time series analysis and future price prediction of the bulldozer.

The steps that I followed to comple the project are:
1. Problem Definition
2. Data: Getting our data
3. Goal Setting 
4. Features: Understanding what information each feature gives. 
5. Exploratory Data Analysis
6. Data Cleaning
7. Data Encoding
8. Feature Engineering
9. Modelling
10. Evaluation
11. Experimentation
12. Feature Importance

I have divided the entire project into three notebooks:
1. Data Preperation: This notebook is for Explortory Data Analysis, Data Cleaning, Data Encoding and Feature Engineering.
2. Test Data Preperation: This notebook is to replicate the data preprocessing on training data to the test data.
3. Random Forest Model: This notebook is to train the random forest regressor to predict the sale price of bulldozer.

## 1. Problem Definition
How well can our model predict the price of bulldozers given it's characterstics and past prices of how much the bulldozers have been sold for?

## 2. Data
The data is collected from a competition conducted by kaggle https://www.kaggle.com/c/bluebook-for-bulldozers/data.

The data for this competition is split into three parts:

* Train.csv is the training set, which contains data through the end of 2011.
* Valid.csv is the validation set, which contains data from January 1, 2012 - April 30, 2012 You make predictions on this set throughout the majority of the competition. Your score on this set is used to create the public leaderboard.
* Test.csv is the test set, which won't be released until the last week of the competition. It contains data from May 1, 2012 - November 2012. Your score on the test set determines your final rank for the competition.

## 3. Evaluation
The evaluation metric for this competition is the RMSLE (root mean squared log error) between the actual and predicted auction prices.

This is a regression problem because we are asked to calculate the price of the bulldozers. So our goal is to minimize the value of our evaluation metric that is RMSLE.
For further details about evaluation visit
https://www.kaggle.com/c/bluebook-for-bulldozers/overview/evaluation

The best score of the competition was 
`0.22909`
So we will try to reach close to the score.

## 4. Features
The key fields are in train.csv are:

* SalesID: the uniue identifier of the sale
* MachineID: the unique identifier of a machine.  A machine can be sold multiple times
* saleprice: what the machine sold for at auction (only provided in train.csv)
* saledate: the date of the sale

Kaggle provides a data dictionary detailing all the features of the dataset. 
Access the complete list here https://docs.google.com/spreadsheets/d/1o047_fOmnykbHtqMLET72kdv8pVE096H/edit?usp=sharing&ouid=101978226593077445138&rtpof=true&sd=true

## 5. Exploratory Data Analysis

Explore the data to get a better understanding of the features. This step will help us create a blueprint to prepare the data, by cleaning and performing feature engineering, for modeling.

## 6. Data Cleaning

The data contains features with null values and many regression models are incapable of handling null values. Thus, it is essential to handle them either by removing them entirely or imputing values. Apart from null values there are features which are highly correlated i.e. one value can be predicted using other. These redundant value increase bias and the computation time.

## 7. Feature Encoding

Data contains feature that are completely categorical which can not be processed by Machine Learning model. To overcome this drawback these features need to be encoded into numerical values. I used various techniques to encode the data depending upon the type of feature and it's relation with the target value.

## 8. Feature Engineering

Since, the data set has features like date we need to convert them into a formate best suitable for machine learning algorithm. Further, there is a requirement of uniformity in data type for modeling.

## 9. Modeling 

For modeling our data set using machine learning model we need to split our data into test and validation set.

According to the Kaggle data page, the validation set and test set are split according to dates.

This makes sense since it's a time series problem.

E.g. using past events to try and predict future events.

Knowing this, randomly splitting our data into train and test sets using something like train_test_split() wouldn't work.

Instead, I split our data into training, validation and test sets using the date each sample occured.

In our case:

Training = all samples up until 2011
Valid = all samples form January 1, 2012 - April 30, 2012
Test = all samples from May 1, 2012 - November 2012

## 10. Evaluation
I create a method to calculate the performance of our model based on the scoring method of this competition
https://www.kaggle.com/c/bluebook-for-bulldozers/overview/evaluation

According to Kaggle for the Bluebook for Bulldozers competition, the evaluation function they use is root mean squared log error (RMSLE).

RMSLE = generally you don't care as much if you're off by $10 as much as you'd care if you were off by 10%, you care more about ratios rather than differences. MAE (mean absolute error) is more about exact differences.

It's important to understand the evaluation metric you're going for.

Since Scikit-Learn doesn't have a function built-in for RMSLE, we'll create our own.

We can do this by taking the square root of Scikit-Learn's mean_squared_log_error (MSLE). MSLE is the same as taking the log of mean squared error (MSE).

We'll also calculate the MAE and R^2 for fun.

## 11. Experimenting

To improve the performace of our model we need to experiment with the hyperparameters of our Machine Learning model. To do so, I have utilised Randomized search CV and Grid search CV to filter the range of values for the hyperparameters. Finally, I tuned the hyperparameters by hand to achive the best possible performance of the model.

## 12. Predicting

Post finding the best set of hyperparameter values and training our model with the data I will make prediction on the test data set. And finally compare it with the true values available on Kaggle.

## 13. Feature Importance

To check which feature are most important and least important towards our prediction for future use I created a feature importance chart. For calculating the importance value I used the default method of Random Forest as well as used the permutation importance method. 

# Conclusion

The final RMSLE score received on the test data was `0.30`. This score is closed I have achived to the targer score by improving the data quality and just using one ML model. Without processing the data like in this project I was receiving rmsle score of `0.47`. The new score is a big improvement on the final result of test data.
