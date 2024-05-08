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

