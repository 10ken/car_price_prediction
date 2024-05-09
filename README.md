# car_price_prediction

# 1.0 Data Description

This dataset was is from Kaggle with the intention of predicting used car sales. There are  2095 car sale entries across 605 different car brands such as Ford, Toyota, Maruti, and Hyundai that were made between the years 2000 to 2020 with the car information and their source of sale, ie. individual, dealer, or trustmark dealer.

### Features

**Unnamed: 0:** The unique identifier.

**name:** The car brand or make of the car.

**year:** The year of manufacture and release of the car.

**selling_price:** The price the car was sold at.

**km_driven:** The number of kilometers the car has driven at the time the car was listed for sale.

**fuel:** The type of fuel the car uses.

**seller_type:** The type of seller.

**transmission:** The type of transmission the car uses.

**owner:** The number of owners the car has had at the time the used car was listed for sale.

**max_power (in bph):** The maximum power output of an engine, typically measured in brake horsepower (bhp).

**Milage Unit:** The measure of fuel efficiency for vehicles, indicating the distance traveled in kilometers per unit volume of fuel consumed or compressed natural gas (CNG), indicating the distance traveled in kilometers per unit mass of fuel consumed.

**Milage:** The fuel efficiency of the vehicle, expressed as the number of kilometers it can travel per unit of fuel consumed.

**Enginer (CC):** The engine displacement, measured in cubic centimeters (cc), indicating the total volume of the engine's combustion chambers.


## 1.1 Notable Remarks About The Data

- The data collection method is known.
- Details about the seller are known.
- This data has already undergone some cleaning processes evident from missing unique identifiers.
- The year this data was collected is known
- The currency units for selling prices are unknown.


## 1.2 Assumptions

- The current year is 2021, hence there is no used car sales past the year 2020.

- The collected data are the current sale prices of used cars.

- The collected data is correct and accurate.

- The column `Unnamed: 0` has 2095 unique values for 2095 rows, indicating this is a unique identifier column. This column ranges from `0` to `6256` and frequently skips the next few numbers in the sequence. These skipped instances are presumably missing or bad data that had been removed through a data processing step prior to the data being uploaded to kaggle.

## 1.3  Research Questions

To better understand the data and projections of future car sales with the given data, we want to answer four questions.

**1.** What 3 year range of manufacture years are the most popular?

**2.** How does the number of driven kilometres affect the price?

**3.** What are some of the most attractive features when buying a used car?

**4.** What can we expect from the used car sales market for cars that are manufactured 
over the next 5 years between 2021 to 2025?


# 2.0 Exploratory Data Analysis

The original data is loaded and called `df`.

## 2.1 Shape and Structure

There are 2095 rows and 14 columns. 

There are 6 categorical and 8 numerical features.

## 2.2 Missing Values

There are no missing values in any of the columns.

## 2.3 Duplicates

There are no duplicates, however we have a unique identifier that does not repeat. There could be duplicate information without the unique identifier, possibly due to a data collection or logging error.

After checking for duplicates without the unique identifier, there are no duplicate instances.

## 2.4 Summary Statistics

The standard deviation for 'km_driven' and 'max_power' is relatively high, indicating a wide range of distances traveled and varying levels of engine power among the used cars in the dataset.

## 2.5 Outliers

Check relevant numerical columns for outliers with box plots.


Outliers for km_driven was manually checked. A function was developed to look for outliers going forward.

The upper and lower outlier thresholds were calculated. Review the notebook for the exact threshold values.

- km_driven had 44 outliers.
- max_power (in bhp) had 121 outliers.
- Engine (CC) has no outliers.

## 2.6 Correlation Analysis

A multicollinearity issue will be raised when a correlation between variables is greater than `|0.80|`.

Review notebook for the correlation plot.

`Engine (CC)` and `max_power (in bhp)` has a correlation value of `+0.85`, indicating a strong positive linear relationship between the two variables. This means that as one variable increases, the other variable tends to increase as well, and vice versa. From a statistical standpoint, such strong correlation suggests the potential for multicollinearity, posing a risk of double-counting effects on the response variable. To mitigate this issue and prevent unintended impacts on the response variable, it's advisable to remove one of these variables from the analysis.

## 2.7 Trends Overview

*Refer to notebook for plots*
**Analysis of Quantitative Features Trends**

- The distribution of `km_driven` is skewed left, indicating that a few vehicles have been driven significantly more kilometers than the median (50th percentile) of the used cars, thereby influencing a higher mean.


- There exists a positive correlation between `Engine (CC)` and `max_power (in bph)` with selling price. As both `Engine (CC)` and `max_power (in bph)` increase, so does the selling price. This observation aligns with our correlation analysis. 
    - However, the relationship between `Engine (CC)` and selling price appears more pronounced compared to `max_power (in bhp)` and selling price. Moreover, considering that `Engine (CC)` lacks outliers while `max_power (in bhp)` has 120 outliers, it is advisable to exclude `max_power (in bhp)` for a cleaner analysis.


- Upon visual inspection, it is evident that the data points for `km_driven` and `selling_price` exhibit clustering in certain regions. Further investigation into these clusters is warranted.


*Refer to notebook for plot*
`km_driven` is skewed left. There is a small number of used cars with an extremely high number of kilometers on the car.

*Refer to notebook for plot*
`Engine (CC)` and `selling_price` has a positive line of best fit.

*Refer to notebook for plot*
Two clusters between `km_driven` and `selling_price` have been clearly defined by the `KMeans` clustering model. These clusters can be confidently used as features to strengthen our model.


**Analysis of Qualitative Features Trends**

- The top 3 selling brands are Maruti, Hyundai, and Ford, respectively.
- The top 3 selling car manufacture years is 2013, 2012, and 2017, respectively.
- The majority of sellers are first owners by individuals with manual cars.

*Refer to plot*
Maruti, Hyundai, and Ford are the top selling brands.

*Refer to table*
The top 3 selling manufacture years is 2013, 2012, 2017.

*Refer to table*
The table highlights that the majority of sales are attributed to first owners of manual cars, representing over half of the total sales volume.


# 3.0 Cleaning Data Preparation for ML Modelling

## 3.1 Clean Year

- The reference point will be the year 2000, serving as our starting time at 0 and year 2020 will be at time 20.

- This designation is significant as the column relates to time, a crucial aspect of our analysis.

## 3.2 Clean Unnecessary Columns

- dropped Unnamed: 0 since there is no meaning to a unique identifier

- dropped max_power (in bhp) since
    1. it has a very strong correlation with Engine (CC)
    2. has outliers whereas Engine (CC) does not have outliers

-`Mileage Unit` is 99% the same value. This does not provide value information for the model's learning. Therefore this will also be removed.


## 3.3 Clean Outliers

- The outliers for `km_driven` has been updated to become the upper thresholds.

- Note the outliers from max_power does not need to be updated since that column has been removed.

## 3.4 Standardization

-`km_driven` has been standardized.

- The other variables was not standardized since it either held a time series value or it was an item characteristic.

## 3.5 Clean Categorical Variables

**Convert transmission values to boolean, [0. 1]**

Label meanings for 'transmission':

0: Automatic

1: Manual

**Owner has numerical significance**

owner

First Owner             1325

Second Owner             586

Third Owner              146

Fourth & Above Owner      37

Test Drive Car             1

**The categorical variable `owner` was changed to a numeric variable because it has numerical meaning.**

owner

1    1325

2     586

3     146

4      37

0       1

The categorical variable `owner` was changed to a numeric variable because it has numerical meaning.

**One Hot Encode the remaining categorical variables**

After cleaning the categorical variables, 11 features have been increased to 25 features.

# 4.0 Feature Engineering

*Refer to plot*
There are 10 well defined clusters between `km_driven` and `Engine (CC)`.

*Refer to plot*
There are 2 well defined clusters between `year` and `Mileage`.


# 5.0 Train Test Split

After splitting the data into training and testing sets, it's essential to reconsolidate and execute all prior cleaning and feature engineering procedures exclusively on the training dataset.

80% training and 20% testing data split.

In this step, the data cleaning, processing, and feature engineering was consolidated into helper functions for easy reusability.

Training dataset has 1676 rows and 27 columns.

Testing dataset has 419 rows and 27 columns.

# 6.0 Regression with Cross Validation

4 Models with cross validation was used.

1) Multivariate Linear Regression, using MSE

	- Test RMSE: 110,000
	- Train RMSE: 120,243
	- Average Cross Validation RMSE 121,710
	- This model is  not a good fit for this data.

2) XGBoost Regression, using RMSE
	
	- Test RMSE: 67,923
	- Train RMSE: 2,9043
	- Average Cross Validation RMSE 78,036

	- This model under fit the training data but was the best performing of all models.

3) Random Forest Model, using RMSE

	- Test RMSE: 70,753
	- Train RMSE: 31,994
	- Average Cross Validation RMSE 81,402
	
	- Second best performing model. Also under fitted.


4) Support Vector Machine Regression

	- Test RMSE: 217,432
	- Train RMSE: 238,324
	- Average Cross Validation RMSE 238,320

	- Worse than linear regression.


XGBoost Regression yielded the best result of 68,265 root mean squared error current units.The average cross validation RMSE for this model was 78,377. This means this model is overfitting the training data although it has the best performance on the test data.

# 7.0 Hyperparameter Tuning

Performed a total of 60 rounds of tuning across 3 models and various parameters, including L1 and L2 regularization.

With tuning, the performance has moved up to RMSE of 68,807 and an average cross validation of 75,954. Better on both sides but still underfitted.


# 8. Evaluation

With tuning, the performance has moved up to RMSE of 68,807 and an average cross validation of 75,954. Better on both sides but still underfitted.


# 9.0 Business impacts and implications

## 9.1 Answer Research Questions

**1.** What 3 year range of manufacture years are the most popular?

Used cars that were manufactured in 2012 to 2014 were the most popular.

**2.** How does the number of driven kilometres affect the price?

While no universal trend emerges between kilometres driven and selling price, an interesting observation surfaces when examining cars with higher mileage.

Specifically, for vehicles surpassing 125,000 kilometres, there appears to be a slight inclination toward lower selling prices.

**3.** What are some of the most important features when buying a used car?

The 3 most important features are `km_driven`, `year`, and `Mileage`.

**4.** What can we expect from the used car sales market for used car prices that are manufactured over the next 5 years between 2021 to 2025?

We are able to make predictions for 2021-2025.
We can see our predicted value and the estimated value.

Depending on the instance, the predicted value can be higher or lower than the estimated value with 1%.

# 10 Limitations And Next Steps

1) A larger dataset is essential for achieving a more comprehensive understanding of patterns and relationships.

2) Enhance the dataset by incorporating additional details about the cars, such as their models and features.

3) The insights derived from this dataset are constrained by its limited scope and scenarios.
