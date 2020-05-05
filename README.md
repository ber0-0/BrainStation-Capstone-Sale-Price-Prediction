# Project：House Price Prediction

This capstone project aims to share real estate market insights and build a predictive model for house price/sale price.

- data (folder): Contains all used datasets.
- Ames_2016-2019 (jupyter notebook): Initial preprocessing on the raw dataset: separated the dataset into sale data and assessment data.
- Final_Presentation (tableau): Exploratory data analysis on the real estate market.
- Transaction (jupyter notebook): Data cleansing, EDA and modeling (including CNN). Please run this file under deeplearning environment.
- Models (Pickled_Files folder):
    - linreg.pkl: pickled file for linear regression
    - knn.pkl: pickled file for KNearestNeighbor
    - dtc.pkl: pickled file for Decision Tree
    - svr.pkl: picked file for Support Vector Regressor
    - xgb_grid.pkl: picked file for XGBoost 
    
## PROJECT PROBLEM STATEMENT
The real estate market is one of the major representations of economic performance. House price is one of its major indicators. This capstone project analyzes the current real estate market trends and builds a model that can effectively predict house prices. The goals of this project are to share some insights into the real estate market and to predict house prices using machine learning.  

## BACKGROUND
Although BC Real Estate Association has provided many market insights to the general public and the licensing agents, these insights do not provide sufficient granularity for an individual to evaluate the market value of a property. House price prediction is a good subject area to apply data science techniques as many models could be used to address this problem. We know that many factors play a role in determining the market value of a property; some examples of these factors are location, lot size, material, and age of the building. Therefore, we can use this information to predict the market value of a property.

## DATASET
This dataset is downloaded from the Ames City website as a [csv file](https://www.cityofames.org/government/departments-divisions-a-h/city-assessor/reports). This dataset contains all the sale data across various property types between 2016 to 2019. It also has information such as property address, property size, and more. For this capstone project, only residential sale data is being used.

## PREPROCESSING/EXPLORATORY DATA ANALYSIS
### PREPROCESSING/DATA CLEANING
The original dataset has 22232 rows and 91 features. The dataset is preprocessed and cleansed as below:
-	Relevancy 
    -	Excluded sale data on properties in other cities;
    -	Filtered sale data on residential properties;
    -	Irrelevant features, such as property address and record year/month, are removed.
-	Duplicated values
    -	Removed features with same or similar values 
-	Missing values
    -	Dropped data points that have no feature information;
    -	Filtered data with sale data.
-	Anomaly
    -	One property has 77 rooms above the ground with a lot size of 8092 sqft. This is most likely a typo, therefore the value of 7 is assigned instead;
    -	One property has 33 bedrooms with a lot size of 6390 sqft. This is also most likely a typo, therefore the value of 3 is assigned instead.
-	Since the building age has an impact on house prices, this feature is created using the difference between year property sold and year property built. 
    -	Properties with negative building age are suspected to be pre-sale properties, therefore these data are dropped from the dataset.

### EXPLORATORY DATA ANALYSIS
Ames is a city in Story County, Iowa and is the home of Iowa State University (ISU).   It has an area of 62.86 km2. According to the 2010 US Census, the major employment in town is Education. Campustown is located south of the ISU campus.  
  
Since location is a major feature in how the house price fluctuates, a boxplot of property prices and neighborhood is created. The average property prices are the highest in North Ridge and North Ridge Height, where are close to the ISU campus. Considered the major employment in town in Education, these two neighborhoods are no doubt the most popular in the local real estate market.
 
The pool area, the number of bedrooms and garage year built are weakly correlated to the sale price. The land assessment and other assessment values are collinear to the total assessment value because the total assessment equals to the sum of these two values. The number of cars parked is collinear to the garage area. This is quite obvious since the bigger the garage, the more cars can be parked in there. As a result, the total assessment value and the garage area features are kept; other features are dropped to prevent multicollinearity.

## MODELS
Since house price (sale price) is a continuous variable, regression models are being used to address this problem. The selected models for this problem are linear regression (Lasso and Ridge), KNearestNeighbor, Decision Tree, Support Vector Regressor, Extreme Gradient Boost (XGBoost) and Convolutional Neural Network (Keras). Before training the model, the dataset has been scaled and used PCA to reduce dimensionality if applicable. Each model has been fine-tuned and cross-validated using GridSearch and pipeline. 
If we look at the R2 value of each model, Extreme Gradient Boosting (xgb) gives out the best result on the test data with 0.83, whereas Decision Tree (dtc) gives out the worst result on the test data with 0.40. 

      
If we look at the distribution of the error between actual and predicted house prices, XGBoost again gives out the best result as XGBoost models have more errors centered around 0. Surprisingly, although the decision tree gives out the worst R2 value, it still has more errors centered around 0 comparing to the rest of the models.  

## CONCLUSION/FINDINGS
Based on the analysis and modeling of the data, location seems to have an important impact on house prices. Moreover, the ground level area (GLA) is also strongly correlated with the house price. Although the XGBoost model gives out a good prediction on the house price, it performs better at predicting high values.

 
## SUMMARY

In order to improve the power of this model, more feature information shall be collected, and more data points are needed to train this model. 
The ultimate goal for this project is to develop a model that can predict the precise sale price of a property based on its features. If the model is capable of predicting a precise sale price of a property, then the realtors or the selling parties can use this model to evaluate the listed price range. Also, an individual can use this model to estimate property-related levies or taxes. Finally, we can launch an application or a webpage to assist individuals to evaluate his/her affordability based on different features, such as location, property type and more.

