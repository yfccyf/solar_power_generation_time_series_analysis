# Solar Power Generation Prediction for Grid Management: Project Overview
* Created a model that predicts the next-day power generation to help power plant with grid management
* Aggregated power generation data from 22 unique inverters
* Downsampled the high-frequency data to appropriate frequency for modeling and prediciton purpose
* Performed differencing to stabilize the non-stationary time series data
* Built a VAR model in order to develop multivariate time series analysis

## Code and Resources Used
**Python Version:** 3.8

**Packages:"" statsmodel, pmdarima, pandas, numpy, matplotlib, seaborn

## Data Overview
2 datasets are used: Power generation data, and weather data (After cleaning and feature selection)
* Power Generation Data: 34 days of power generation data recorded in 15-minute interval

![](images/df2_head.png)

* Weather Data: 34 days of ambient weather data recorded in 15-minute interval

![](images/df2_2_head_2.png)
## Data Preprocessing
Extracted date and time columns for both datasets. Other than the timestamp, from the datasets, we have the following features:

Power Generation Data:
* DC Power
* AC Power
* Daily Yield
* Total Yield

Weather Data
* Ambient Temperature
* Module Temperature
* Irradiation

Since our goal is to predict the power generation for the entire power plant, the data from 22 inverters are aggregated. The data size dropped from over 60,000 to 3,000 rows

## EDA
### Distribution
Whole timespan: large amount of zero values in DC_POWER and AC_POWER, which is due to long idle hours (night)

![](images/dist.png)

Active hours: dual mode

![](images/dist2.png)

### Correlation
DC_POWER and AC_POWER are perfectly correlated, thus, we only chose DC_POWER as target

![](images/corr.png)

### Relationships among variables
#### Between DC and Daily Yield
We can tell that the power conversion rate is around 20%


![](images/conversion.png)

#### Between Ambient and Module Temperature

During the day, module temp is much higher than ambient temp, but both happen simultaneous and highly correlated. Therefore, I only chose Ambient temp as exogenous predictor

![](images/temp.png)

#### Between Ambient Temperature and Irradiation
There is certain delay between irradiation and ambient temp

![](images/irradiation.png)

### Time Series
Mean generation values on an avergae day

![](images/g1.png)

Mean generation values over the whole period

![](images/g2.png)

### Target and predictor combined Time Series
Both variables are highly correlated

![](images/combined.png)

## Model Building
