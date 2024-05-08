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

**1.** How has the demand changed over the years between 2000 to 2020?

**2.** How does the number of driven kilometers affect the price?

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
