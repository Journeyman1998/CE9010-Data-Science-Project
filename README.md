# CE9010 Project - Predicting Housing Prices

## Installation
Standard libraries - numpy, pandas, scikit-learn, matplotlib, seaborn - are needed. In addition, use the package manager [pip](https://pip.pypa.io/en/stable/) to install the following dependencies.

```bash
pip install geopandas
pip install pyshp
pip install descartes
pip install geopy
```

## Introduction
The objective of the project is to analyse how house pricing model can be influenced by various factors such as area, locations, distance from central and others. As those features could easily be found on the online platform, with a simple pricing model that considered these determinant factors, buyers could easily get the rough estimation of the property price from the pricing model. Furthermore, our findings could be shared through various social media mediums and could provide a useful rough pricing tool for potential buyers when searching for house that is both within their means and facilities they desired. 

## Data Acquisition
<p>Data was collected from the Propertyguru website, starting on 1 March 2020 by developing our own web scrapping tool. Tight security of the website was an immediate challenge that we had to overcome. Multiple issues such as image captcha, access to the website through our bot being denied were our main problems. In the end, we made use of selenium webdriver to make the bot as 'human-like' as possible and also had to collect the data over a few days with reduced frequency to ensure that we are not detected. Our code is shared on GitHub for anyone who may be interested.</p>

## Feature Engineering - Coordinates
<p>Our data contains the feature: Address, which is a string value. It is hard for a model to learn from text data. Therefore, we converted the addresses into the latitude/longitude coordinates. By making use of the library Geocoder and its class ArcGIS, we made slight modifications to it in order to achieve our needs. Our code is shared on GitHub as well. </p>

## Data Cleaning
The data cleaning was conducted in the following process: 
1. Eliminate missing values and values that contain unknown data (e.g unknown tenure). 
2. Remove uncommon houses like shophouse and convervation house from the dataset (as there are insufficient data to train the model for such type of houses)
3. Remove string symbols like 'S$', 'psf', 'sqft' 
4. Extract numeric value from the 'Land_Area' variable 

## Feature Engineering - Other Features
From the coordinates, we can engineer two features: the number of nearby primary schools^ and the number of nearby MRT stations.

In hope of improving our machine learning, we engineered some apartment-related features, such as bathroom area, bedroom area and convenience score.


^the data for secondary schools and junior colleges is not available

## Data Exploration
We removed some outliers (we found that these are invalid data, hence removing them) before performing data exploration.
Some interesting pointers:
1. Condo and HDB have similar area, but way different valuations.
2. Houses near central region have higher valuations.
3. More condos are distributed around the central region than HDBs.


## Data Preprocessing
We one-hot encoded the categorical data, and stratified-split the dataset into train and test set. Then, we did a z-scoring on the train and subsequently on the test data.

## Data Analysis
The performance of the model is measured by the lower of RMSE (root-mean-squared-error).

We performed machine learning on these models:
1. Linear/Polynomial Regression
2. Polynomial Ridge Regression
3. DecisionTreeRegressor
4. RandomForestRegressor
5. GradientBoostingRegressor
6. KNeighborsRegressor

Later, we also did stacking on all the base models (except Linear/Polynomial Regression). We set the meta model as Linear Regression.

In summary, the best model is
- With interpretability: DecisionTreeRegressor
- With accuracy (base): GradientBoostingRegressor
- With accuracy (overall): Stacking

## Conclusion
The test RMSE for Stacking is 114.523, which is still quite high for the purpose of predicting housing prices. This is due to the many factors that will affect the value of an apartment. The few key features we have obtained are not sufficient to train a model with extremely low test error. However, it may provide a rough estimate of the housing price for inexperienced buyers. 

## Future Work
Limitations of our project:
1. Insufficient data features.

2. Use of RandomisedSearch, instead of GridSearch, causes unoptimised base models.

3. Higher bias of some base models rendered Stacking ineffective.


Suggestions for improvement:
1. Get more data features by consulting domain experts.

2. In-depth selection of hyperparameters.

3. Use of models with lower bias, such as Support Vector Regressor or Neural Network.

4. Get more training data.
