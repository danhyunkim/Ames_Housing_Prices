# Executive Summary

Zillow is an online real estate database that was founded in 2006 that provides its users the ability to buy, sell, rent or get estimates of residential buildings. They are trying to boost their user base across the country. We set out to build an efficient model to effectively estimate the price of a given home and we focused on Ames, Iowa. The model is aimed to predict home prices as accurately as possible to increase user confidence in Zillow's product, and in turn, the user base.

## Problem Statements

How can we increase user confidence in Zillow's in Ames, Iowa?

What is the best model to utilize to accurately predict selling price?

## Data Dictionary

Below is a data dictionary of the features that we analyzed.

|Feature|Description|
|---|---|
|MS SubClass|The building class|
|MS Zoning|Identifies the general zoning class of the building|
|Lot Frontage|Linear feet of street connected to the property|
|Lot Area|Lot size in square feet|
|Street|Type of road access to the property|
|Alley|Type of alley access to the property|
|Lot Shape|General shape of the property|
|Land Contour|Flatness of the property|
|Utilities|Type of utilities available|
|Lot Config|Lot Configuration|
|Land Slope|Slope of the property|
|Neighborhood|Physical locations within Ames city limits|
|Condition 1|Proximity to main road or railroad|
|Condition 2|Proximity to main road or railroad (if a second is present)|
|Bldg Type|Type of dwelling|
|House Style|Style of dwelling|
|Overall Qual|Overall material and finish quality of the dwelling|
|Overall Cond|Overall condition rating of the dwelling|
|Year Built|Year the building was built|
|Year Remod/Add|Year remodeled or additions to the building (same as year built if no remodeling or additions)|
|Roof Style|Type of roof|
|Roof Matl|Roof material|
|Exterior 1st|Exterior covering on house|
|Exterior 2nd|Exterior covering on house (if more than one material)|
|Mas Vnr Type|Masonry veneer type|
|Mas Vnr Area|Masonry veneer area in square feet|
|Exter Qual|Quality of exterior material on building|
|Exter Cond|Present condition of the exterior material|
|Foundation|Type of foundation of the building|
|Bsmt Qual|Height of the basement in inches|
|Bsmt Cond|General condition of the basement|
|Bsmt Exposure|Basements exposure to a walkout or garden level basement walls|
|BsmtFin Type 1|Quality of finished basement area|
|BsmtFin SF 1|Type 1 area finished in square feet|
|BsmtFin Type 2|Quality of second finished basement area (if present)|
|BsmtFin SF 2|Type 2 area finished in square feet|
|Bsmt Unf SF|Unfinished area of basement in square feet|
|Total Bsmt SF|Total square feet of basement area|
|Heating|Type of heating|
|Heating QC|Heating quality and condition|
|Central Air|Central Air Conditioning (yes or no)|
|Electrical|Electrical system|
|1st Flr SF|Square footage of 1st floor|
|2nd Flr SF|Square footage of 2nd floor|
|Low Qual Fin SF|Low quality finish of all floors in square footage|
|Gr Liv Area|Above grade (ground) living area in square feet|
|Bsmt Full Bath|Basement full bathrooms|
|Bsmt Half Bath|Basement half bathrooms|
|Full Bath|Full bathrooms above ground|
|Half Bath|Half bathrooms above ground|
|Bedroom AbvGr|Number of bedrooms above basement level|
|Kitchen AbvGr|Number of kitchens|
|Kitchen Qual|Quality of kitchens|
|TotRms AbvGrd|Total rooms above ground not including bathrooms|
|Functional|Home functionality rating|
|Fireplaces|Number of fireplaces|
|Fireplace Qu|Quality of the fireplace(s)|
|Garage Type|Garage location|
|Garage Yr Blt|Year garage was built|
|Garage Finish|Interior finish of garage|
|Garage Cars|Size of garage in car capacity|
|Garage Area|Size of garage in square feet|
|Garage Qual|Garage quality|
|Garage Cond|Garage condition|
|Paved Drive|Paved driveway|
|Wood Deck SF|Wood deck area in square feet|
|Open Porch SF|Open porch area in square feet|
|Enclosed Porch|Enclosed porch area in square feet|
|3Ssn Porch|Three season porch area in square feet|
|Screen Porch|Screen porch area in square feet|
|Pool Area|Pool area in square feet|
|Pool QC|Pool quality|
|Fence|Fency quality|
|Misc Feature|Miscellaneous features not covered in other categories|
|Misc Val|Monetary value of miscellaneous features|
|Mo Sold|Month sold|
|Yr Sold|Year sold|
|Sale Type|Type of sale|
|SalePrice|Selling price|

## Methodology

Below is a brief overview of the steps we took to build our regression model.

### Data Cleaning

With null values and outliers existing in our data, we had to make sure that these values were accounted for in some way or another for our models to effectively capture the data. With intuition we were able to determine how to treat the null values. For example, if there was empty data in a column that indicated whether or not the house had a pool, we thought it would be safe to assume that the empty value just meant the house had no pool. A similar line of thought went for the rest of the null values. In the case for outliers, we decided to keep the outliers in the dataset to keep as much data as possible. We only fixed outliers that were clearly incorrect.

### Feature Engineering

Dummy variables were created for all non-numerical columns. If the columns were ordinal, we replaced the string values with actual integer rankings. For example, since 'Excellent' is better than 'Good' which is better than 'Fair', we ranked 'Excellent' as 5, 'Good' as 4, and so on until all ordinal values were accounted for.

We also created polynomial features of all numerical and dummy variables to see how the interaction terms between each feature worked in tandem to have an impact on the selling price. 

### Modeling

We utilized the Linear Regression model throughout this analysis. To establish our baseline score we built a traditional Linear Regression using the feautures that had the highest correlation with selling price. This model did not contain the polynomial features and dummy variables that we created.

We then built LassoCV and RidgeCV models utilizing all of the numerical columns, polynomial features and dummy variables to see which model would have the highest R2 score. 

## Findings

We found that the features that have the most impactful influence on the selling price of a home are:

* Overall Quality 
* Above Grade (Ground) Living Area
* Garage Size (by cars and in sqft.)
* Basement Size (in sqft.)
* 1st Floor Size (in sqft.)
* Number of Full Bathrooms

The LassoCV model turned out to be the strongest over the RidgeCV and simple Linear Regression. 

## Improvements

Some improvements we can make to improve our model are:

* Take the log of the predictor variable and the feature variables in order to smooth out the distributions of each variable. This will provide a more balanced dataset on which we can run our model on resulting in a stronger model.
* Iterate on the polynomial features/dummy variables that were utilized in the regression model.
* Experiment with the hyperparameters within the model.
* Gather more data. Having more data is always helpful so if we gathered more observations on houses in Ames, we would have a larger training set to work with.

## What does this mean for Zillow?

Using our findings and the model that we have built, Zillow can apply this knowledge to different markets in the country. The model we created can work as a baseline model in which the analytics team can continue to strengthen with new feature categories, new engineered features, log features, etc.






