# Cab-Fare-Prediction
Project Name – Cab Fare Prediction

Problem Statement -
You are a cab rental start-up company. You have successfully run the pilot project and
now want to launch your cab service across the country. You have collected the
historical data from your pilot project and now have a requirement to apply analytics for
fare prediction. You need to design a system that predicts the fare amount for a cab ride
in the city.

Data Set :
1) train_cab.zip
2) test.zip

Missing Values : Yes
 
Chapter 1 

Introduction
With Cab rental services growing exponentially in the past decade, the ease of the public over using the cab services provide a greater value for using these rental services.

1.1 Problem Statement 

You are a cab rental start-up company. You have successfully run the pilot project and now want to launch your cab service across the country. You have collected the historical data from your pilot project and now have a requirement to apply analytics for fare prediction. You need to design a system that predicts the fare amount for a cab ride in the city.


1.2 Data 

Understanding the data is important for solving the business problem and applying scientific models to predict the data 

Variables 	Description 
fare_amount 	Fare amount 
pickup_datetime 	Cab pickup date with time 
pickup_longitude 	Pickup location longitude 
pickup_latitude 	Pickup location latitude 
dropoff_longitude 	Drop location longitude 
dropoff_latitude 	Drop location latitude 
passenger_count 	Number of passengers sitting in the cab 

Missing Values: Yes


	
Below code is used to copy the train_data  and verify the data provided for the problem statement. 


From the above analysis we find that we have,
•	7 Variables
•	16067 Observations

Among these 7 Variables 6 are independent variables and 1 is dependent variable which is fare_amount

Notes: Fare_amount is a continuous variable.

 
Chapter 2 
Data Pre-Processing
Before building a model to predict the fare amount from historical data that we have , it is important for us to do the Exploratory Data Analysis so that we can transform the raw data into an understandable format. Raw data cannot be fed directly into the model as it would cause errors in the prediction. Hence it is important we pre process the data before sending it through a model.

Below are the steps we have to perform first in Data Preprocessing
Here are the steps that are being followed for the given data.
1. Data cleaning and exploration
2. Missing value analysis
3. Outlier Analysis
4. Feature selection
5. Feature scaling


3.1 Data exploration and Cleaning 
Below observations can be made from the given data,
•	The Variable pickup_datetime contains date and time of the passenger in the cab. Hence this can be further broken down to extract more variables from this as stated below.
i)	Year
ii)	Month
iii)	Day
iv)	Hour
v)	Minute
vi)	Seconds
With this approach 6 variables are created which are Year, Month, Date, Hour, Minute and Seconds.

Also we will be removing the pickup_datetime variable as we no longer need this


•	We have the four variables, pickup_longitude, pickup_latitude , dropoff_longitude, dropoff_latitude . Using these 4 variables we can combine into a one variable called distance , by calculating the difference between pickup location and drop off location.

The Haversine ('half-versed-sine') formula was published by R.W. Sinnott in 1984, although it has been known for much longer. At that time computational precision was lower than today (15 digits precision). With current precision, the spherical law of cosines formula appears to give equally good results down to very small distances.
Since this project is related to cab pick up point of a passenger within  a city hence the distance will be smaller and we are going to use this function using geosphere package available in R

•	From the data we have obtained so far we are going to further pre process the data.
From the previous section we can see that the fare_amount and distance.

Once we change the data type we now move on to find the missing values and impute those values.
Missing Values
First we calculate the no of NA values in the data_set. We find that only 85 is the missing values out of 16067 observations.  Since the no of NA values is 85 only, it is very negligible compared to the 16067 observations, hence we are not going to impute the missing values and we will be ignoring them.

Outlier Analysis

In order to find the Outliers in a data, we first plot the boxplot for the dataset to find the outliers. 


From the above diagram we see that there are few outliers present in the data set for some of the variables i.e. fare_amount and distance. For the remaining variables of time like Year, Month,Date, Hour, Minute and Seconds there are not outliers present.

Hence we go for removing these outliers and replacing them with the value of NA’s.


From the  co relation plot we find that the fare_amount and distance variables are co related which is true because as the distance increases for the cab ride, the fare for the ride also increases. Since we need both the distance and fare_amount variables we will retain the distance variable to predict the fare_amount for the test data.



•	Feature Scaling
•	We first find how the data is distributed across different variables that we have like fare_amount, passenger_count, distance


From the histogram plotted we can verify the data is not normally distributed hence we go for normalisation. 

 

Chapter 3
Modelling

Since our target variable to predict fare of the cab (fare_amount) is continous variable we will be evaluating the model using regression algorithms to predict the data which are as following,

a.	Linear Regression
b.	Decision Tree
c.	Random Forest

First we split the data into train and test using sampling method and apply the regression models for the test data to predict the values and compare with the actual values.

Below is the comparison model we have arrived at after evaluating all the model and its parameters

Model Name	MAPE	Accuracy
Linear Regression	18.42129	81.578706
Decision Tree	20.96588	79.034118
Random Forest	18.59785	81.402151


For the Error Metrics we have calcualted MAPE only because RMSE is widely used in time series data.

From the above table we can see that the Random_Forest Model and Linear Regression is having almost similar Accuracy rate hence  we will be finalizing one of them, and I have chosen the Random Forest Model for predicting the cab fare for new test data.
