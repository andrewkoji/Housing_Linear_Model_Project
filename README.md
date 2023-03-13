## Phase 2 Project

Final Project Submission
Please fill out:

- Student name: Andrew Levinton
- Student pace: self paced
- Scheduled project review date/time:
- Instructor name: Ahbhineet Kukarni
- Blog post URL:

## Business Problem:
# Stakeholder: Real Estate Agency - Zillow

![Zillow_logo19.png](./images/zillow.png)

# Problem: 
Business problem - Provide advice to homeowners about how home renovations might increase the estimated value of their homes, and by what amount.

### How problem will be approached

This problem will be approached using information from a built in linear regression model. The model will be built using both numerical and categorical data to provide what features may help to increase the price of peoples homes. Numerical data will be explored and categorical data will be added after in an attempt to improve the model.

### Description of the Data:
King County House Sales dataset
columns can be referred to in readme.

### Target variable
* `price` - Sale price (prediction target)

Possible continuous numerical predictors, based on correlation:

Based on correlation coefficient:
- `sqft_living`- Square footage of living space in the home
- `sqft_above`- Square footage of house apart from basement
- `bathrooms`- Number of bathrooms
- `sqft_patio`- Square footage of outdoor porch or deck space
- `bedrooms` - Number of bedrooms
-`sqft_garage`- Square footage of garage space
- `school_rating` - Engineered based on data scraped from the GreatSchools API

Other numerical variables:
- `sqft_lot` - Square footage of the lot
- `sqft_basement` - Square footage of the basement
- `lat` - Latitude coordinate
- `long` - Longitude coordinate

### Simple Linear Regression on select features

These categories are interesting because they are both continuous and integer values that 

Possible string categorical variables:
- `greenbelt`- Whether the house is adjacent to a green belt
- `view`- Quality of view from house
- `waterfront` - Whether the house is on a waterfront
  * Includes Duwamish, Elliott Bay, Puget Sound, Lake Union, Ship Canal, Lake Washington, Lake Sammamish, other lake, and river/slough waterfronts
- `nuisance` - Whether the house has traffic noise or other recorded nuisances
* `date` - Date house was sold

Possible numerical categorical variables:
* `condition` - How good the overall condition of the house is. Related to maintenance of house.
  * See the [King County Assessor Website](https://info.kingcounty.gov/assessor/esales/Glossary.aspx?type=r) for further explanation of each condition code

* `grade` - Overall grade of the house. Related to the construction and design of the house.
  * See the [King County Assessor Website](https://info.kingcounty.gov/assessor/esales/Glossary.aspx?type=r) for further explanation of each 


* `bedrooms` - Number of bedrooms
* `bathrooms` - Number of bathrooms
* `floors` - Number of floors (levels) in house

Assumption check:
- `Is it linear?`
- `Is it normal?`
    - histogram
    - QQ-plot
- `Is it homoscedastic?`

### Plan for building stats model:
- Narrow down variables to selections(also known as FEATURES)
- One hot encode any categorical variables for plotting purposes
- be prepared to remove certain "dummies" from the dataset to optimize one hot encoding. 

### Process for "narrowing":
- Look at:
    - `Scatter plots`
    - `histograms`
    - `correlation coefficients`
    - `statsmodel p-values to test if the feature is statistically significant`
- Try transforming the data via linear, logarithmic or polynomial transformation to see how shape of data changes. 

## Observing correlation matrix for possible features that can be used with the price
![image-2.png](./images/Correlations.png)

![image-2.png](./images/corrheatmap.png)

## Interesting Correlations

At first glance, it appears that the following variables are the "most interesting" variables to look at:
- `sqft_living`
- `sqft_above`
- `bathrooms`
- `sqft_patio`
- `lat`
- `bedrooms`
- `school rating`
- `sqft_basement`
- `floors`

The correlations may not be the best metric for picking features because there could be a case of statistical insignificance or skewed data (data is not normally distributed). For further investigation, we will also look at the variance inflation factor (VIF).

### Variance inflation factor (VIF)

Multicollinearity occurs when there are two or more independent variables in a multiple regression model, which have a high correlation among themselves. When some features are highly correlated, we might have difficulty in distinguishing between their individual effects on the dependent variable. Multicollinearity can be detected using various techniques, one such technique being the Variance Inflation Factor(VIF).

In VIF method, we pick each feature and regress it against all of the other features. For each regression, the factor is calculated as :

VIF = 1 / (1 - R^2)

Where, R-squared is the coefficient of determination in linear regression. Its value lies between 0 and 1.

The list of variance inflation factors are calculated for each numerical value below:


#### VIF Data: 

Variable            VIF
- `bedrooms`:      24.768622
- `bathrooms`:     26.263735
- `sqft_living`:   119.808110
- `sqft_lot`:      1.140594
- `floors`:        17.177547
- `condition`:     31.150197
- `grade`:         133.035571
- `sqft_above`:    92.874304
- `sqft_basement`: 7.075288
- `sqft_garage`:   4.675596
- `sqft_patio`:    2.240790
- `yr_built`:      9263.218882
- `yr_renovated`:  1.211647
- `lat`:           136585.268881
- `long`:          146658.438892
- `school_rating`: 22.635104
- `month`:         697.233857
- `day_of_year`:   612.219197

#### VIF levels:

- Good: VIF <= 5

- Moderate/Questionable: VIF >=5 and VIF <= 10

- Throw out: VIF >= 10

#### Good VIFS: 
- `sqft_lot`: 1.140594
- `sqft_garage`: 4.675596
- `sqft_patio`: 2.240790
- `yr_renovated`: 1.211647

#### Questionable VIFS: 
- `sqft_basement`: 7.075288

#### Throw out VIFS: 
- `bedrooms`: 24.768622
- `bathrooms`: 26.263735
- `sqft_living`: 119.808110
- `floors`: 17.177547
- `sqft_above`: 92.874304
- `yr_built`: 9263.218882
- `lat`: 136585.268881
- `long`: 146658.438892
- `month`: 697.233857
- `day_of_year`: 612.219197
- `school_rating`: 22.635104

It appears at first glance that the data only yields a small set of independent variables that are not highly collinear with eachother. This will be looked at again after the removal of outliers, and the transformation of data.

![image.png](./images/scatterplots.png)

# Model #1 - numerical predictors only, some categorical
![image-2.png](./images/OLS_Model_1.png)


Predictors:
- `bedrooms`
- `bathrooms`
- `sqft_living`
- `sqft_lot`
- `floors`
- `condition` - redefined to numerical values
- `grade`- redefined to numerical values
- `sqft_above`
- `sqft_basement`
- `sqft_garage`
- `sqft_patio`
- `lat`
- `long`
- `school_rating`

Target variable:
- `price`


## Observations
p_value > 0.05


- `month`
- `long`


** look at again after adjusting for outliers


 - All variables with a p_value > 0.05 are deemed statistically insignificant and will eventually be dropped from the final model.

 - Month was not anticipated as an effective predictor because it is not typical for the season to affect the sale price of a house.
 
 - longitude will continue to be looked at but appears insignificant to the model now
 
 
Additional Observations:
 - The adjusted r-squared value is .514, indicating that his model can explain approximately 51.4% of the data.
 -  Skew: A kurtosis value between -2 and +2 is good to prove normalcy. The skew value is 10.060, indicating that this model is heavily skewed. This will be addressed through transformations to normalize the data. 

![image.png](./images/model1residhist.png)

## Possible Improvements to be made to model:
- dropping of variables that are not statistically significant (Pval > 0.05)
- addition of categorial variables(one hot encoded)
- location would possibly be the most interesting variable, mapped against the waterfront or view variable
- transformation of data to satisfy normality assumption -ex: log transformation or square root transformation
- removal of outliers: Outliers in this case will be considered to be any data falling greater than 
  3 standard deviations outside the mean
### Goals
    - improve skewness
    - reduce heteroscedacity - ensure model is homoscedastic
    - increase rsquared to promote higher level explanation of data from model
    - remove multicollinearity

## Possible categorical variables of interest: 

* `waterfront` - Whether the house is on a waterfront
  * Includes Duwamish, Elliott Bay, Puget Sound, Lake Union,Lake Washington, Lake Sammamish, other lake 
  Data is engineered by zipcode in this study.
* `greenbelt` - Whether the house is adjacent to a green belt
* `nuisance` - Whether the house has traffic noise or other recorded nuisances
* `view` - Quality of view from house
  * Includes views of Mt. Rainier, Olympics, Cascades, Territorial, Seattle Skyline, Puget Sound, Lake Washington, Lake Sammamish, small lake / river / creek, and other
* `heat_source` - Heat source for the house
* `sewer_system` - Sewer system for the house
* `address` - The street address

The grade and condition are already changed to numerical variables, so this part of the analysis will focus on the string categorical variables. 

The address appears to be the most interesting variable in the batch because it can be mapped against the waterfronts or the quality of view from the houses. For this, we will extrapolate features of the address to reduce and categorize the location. 

Waterfont, greenbelt, nuisance, view, sewer(onehotencoded), and heat source(onehotencoded) are added to the model to see its effects.

## Model #2

### Changes to create model 2

- Additon of categorical variables: 
- `waterfront, view, greenbelt`: changed to booleans or scaled as 1-4 depending on number of options
- `sewer, heatsource`: one hot encoded to be added as numerical variable

![image-2.png](./images/OLS_Model_2.png)

## Observations of Model 2
Predictors:
- 'bedrooms'
- 'bathrooms'
- 'sqft_living'
- 'floors'
- 'grade'
- 'sqft_above',
- 'sqft_basement'
- 'sqft_garage'
- 'sqft_patio'
- 'yr_built',
- 'yr_renovated'
- 'lat'
- 'long'
- 'school_rating
- 'day_of_year'
- 'waterfront'
- 'nuisance',
- 'view'
- 'heat_source' - one hot encoded
- 'sewer' - one hot encoded

pvalue > 0.05
- long
- yr_renovated
- month
- sewer_PRIVATE RESTRICTED
- sewer_PUBLIC RESTRICTED
- heat_source_Electricity/Solar
- heat_source_Gas
- heat_source_Gas/Solar
- heat_source_Oil/Solar
- heat_source_Other
- nuisance
- greenbelt

Categorical variables of waterfront, nuisance, and view were encoded with numbers to see if improvements were made. 

Model is still highly skewed although did present itself with some improvements. Next steps will be to normalize the data by transforming features that are skewed within the data, as well as remove outliers

- Jarque-Bera score is sky high and must come down for the model to hold any validity. 
- Durbin Watson score is in the acceptable range of 1.50-2.50
- Rsquared has 'improved' but only at the expense of the the continued flaws mentioned before. 

## Next Steps
Next steps are to improve numerical variables by:
- `removing outliers to improve skew` 
- An outlier will be defined as three standard deviations away from the mean of the target variable.

- `transform variables so they are normally distributed within the model`
- The target variable will be transformed to normalize the distribution. 
- removing variables that have a pvalue > 0.05

## Model #3 - Ran after outliers are removed

![image.png](./images/OLS_Model_3.png)

![image.png](./images/model3residafteroutliersremoved.png)

#### Predictors

- `bedrooms`
- `bathrooms` 
- `sqft_living` 
- `sqft_lot 
- `floors`
- `condition` 
- `grade` 
- `sqft_above` 
- `sqft_basement` 
- `sqft_garage`
- `sqft_patio` 
- `yr_built` 
- `yr_renovated` 
- `lat` 
- `long` 
- `month`
- `day_of_year` 
- `sewer_PRIVATE RESTRICTED` 
- `sewer_PUBLIC`
- `sewer_PUBLIC RESTRICTED` 
- `heat_source_Electricity/Solar`
- `heat_source_Gas` 
- `heat_source_Gas/Solar` 
- `heat_source_Oil`
- `heat_source_Oil/Solar` 
- `heat_source_Other` 
- `waterfront` 
- `nuisance`
- `view` 
- `greenbelt`

## Observations of model 3
pvalue > 0.05
- `sqft_basement` 
- `sewer_PRIVATE RESTRICTED`
- `sewer_PUBLIC RESTRICTED`
- `heat_source_Electricity/Solar`
- `heat_source_Oil/Solar`
- `heat_source_Other`



- Adjusted rsquared indicates that the model explains 63.3% of the data.
- Skewness has improved dramatically to an acceptable range between -2 and 2. The removal of outliers has made this possible.
- Durbin-Watson score is still in the acceptable ranges of 1.5-2.5
- Jarque-Bera score is still very high but has been brought down by a significant factor. Still not perfect but trending in the right direction.
- Multicollinearity is possibly present in the model and likely so given the initial VIFs before the first model was built. VIFS should be revisited again to see if those variables are worth keeping. 

# Looking at transformations for the target variable aka price.

## Histogram and QQplot of the target variable
![image.png](./images/histQQprice.png)

### Issue above is the data shows linearization everywhere but both tails of the data. Catching the lower tail will be the goal for the test of transformation. For this, we will try a root transformation. 


## Histogram and QQplot of the transformed target variable
![image-2.png](./images/histqqsqrtprice.png)



![image-3.png](./images/TVtransformations.png)

### Checking model with transformed target variable - square root transformation
![image.png](./images/OLS_Model_sqrt.png)


![image-2.png](./images/model3residsqrtprice.png)

## y_log vs y_sqrt

The model with the square root transformation appears to be less skewed and possesses a higher rsquared value, lending the ability of the model to explain more of the data. For these reasons we will use y_sqrt as our dependent variable for now until y_log appears to outweight the benefit of y_sqrt.

Jarque-Beras score is significantly better as well with the y_sqrt variable so I'll go with it for now. 

## Checking distribution of predictor


### Looking at sqft_living
![image.png](./images/sqftliving.png)

### Log transformed sqft_living (sqft_living_log)
![image-2.png](./images/sqftliving_log.png)

## Model ran one more time - after dropping bedrooms, and all onehotencoded variables with pval > 0,05

![image-4.png](./images/OLS_Model_3_after_dropped_variables.png)

### Residual distribution
![image-5.png](./images/residonemore.png)


## Observations

- pval > 0.05

`bedrooms` - dropped from the current model

- all variables are statistically significant (pvalue < 0.05)
- Durbin-Watson Score continues to be "fine" but not improve a whole lot.
- Jarque-Bera Score continues to improve but still must come down
- skewness is now an afterthought as its at a very low -0.347
Overall no real improvement of the model happens here, we will try adding in new variables to improve as well as revisit VIFs to likely drop all that were originally at extremely high levels. 


Next steps to improve the model:
1. revisit VIFs to see if any variables(now that outliers are removed and data has been transformed) should now be dropped from the model. 
2. New predictors will be engineered to be added to the model. The next focus will be on the zipcodes in an attempt to narrow down the data with location-dependent price points. Possible data to be looked at are:
- waterfronts 
- views
- school districts: rating, and school taxes
- tax brackets

## Rerunning model after scaling

![image.png](./images/OLS_Model_Scaled.png)

### Residual Distribution Plot 
![image.png](./images/residualnobedrooms.png)

#### Checking VIFs
![image-3.png](./images/scaledVIFs.png)
- VIFs for many variables are still elevated and need to be dropped from model if that remains in the final model. 

## Final model

#### Model is ran after adding the waterfront data (one hot encoded) as well as dropping any additional variables that are of a pvalue > 0.05

![image.png](./images/final_model.png)
### Residual Distribution Plot 

![image-2.png](./images/finalresid.png)

### Final Check on VIFs for multicollinearity
![image-3.png](./images/final_vifs.png)

- All VIFs are under 3 but one, addressing the issue of multicollinearity. The statsmodel also does not label any concerns on multicollinearity.

### QQplots of all variables

As shown below, the QQplots of all the variables satisfies linearity which is one of the required assumptions for the model, with some issues at the upper and lower tail for some. 

![image.png](./images/final_QQplot.png)

### Interpretation

We have a linear model with the dependent variable (price) square root transformed, and the following independent variables and their corresponding coefficients:

- const: 963.234796
- bathrooms: 20.254186
- sqft_lot: 10.414107
- floors: -7.052045
- condition: 24.035449
- grade: 68.459181
- sqft_above: 74.797094
- sqft_basement: 23.043827
- sqft_garage: -4.584058
- sqft_patio: 8.214320
- yr_built: -23.544185
- yr_renovated: 7.226726
- lat: 88.816082
- long: 11.343899
- school_rating: 27.353843
- sewer_PUBLIC: 6.584108
- heat_source_Gas: 9.278196
- heat_source_Gas/Solar: 3.607930
- waterfront: 6.715330
- nuisance: -6.073275
- view: 22.472439
- greenbelt: 7.161059
- water_Elliot Bay: -25.286029
- water_Lake Sammamish: 75.729413
- water_Lake Washington: -64.398218
- water_Puget Sound: -16.004882

`- Adjusted rsquared indicates the model explains 62.6% of the data`

The linear regression model with a dependent variable that has been square root transformed and scaled, along with independent variables that have been scaled as z-scores, can be interpreted as follows:

The model is used to predict the price of a house, which has been square root transformed, based on the values of several independent variables. Each independent variable has been standardized to a z-score, so the coefficients represent the change in the dependent variable (price) for a one standard deviation increase in the independent variable.

Specifically, the interpretation of the coefficients is as follows:

The constant coefficient in a linear regression model represents the expected value of the dependent variable (in this case, the square root of the price) when all the independent variables are equal to zero. Therefore, as the constant coefficient is 963.234796, we would expect the square root of the price to be around 963 when all the independent variables are zero. However, it's important to note that in the context of the model, there may not be any real-world scenarios where all the independent variables are actually zero. The constant term is mainly used as a baseline reference point for the other predictors in the model.

- `As the number of bathrooms increases by one standard deviation, the square root price increases by 20.254186.`
- `As the size of the lot increases by one standard deviation, the square root price increases by 10.414107.`
- `As the number of floors increases by one standard deviation, the square root price decreases by 7.052045.`
- `As the condition of the house increases by one standard deviation, the square root price increases by 24.035449.`
- `As the grade of the house increases by one standard deviation, the square root price increases by 68.459181.`
- `As the size of the above ground living area increases by one standard deviation, the square root price increases by 74.797094.`
- `As the size of the basement living area increases by one standard deviation, the square root price increases by 23.043827.`
- `As the size of the garage increases by one standard deviation, the square root price decreases by 4.584058.`
- `As the size of the patio increases by one standard deviation, the square root price increases by 8.214320.`
- `As the age of the house (yr_built) increases by one standard deviation, the square root price decreases by 23.544185.`
- `As the year of renovation (yr_renovated) increases by one standard deviation, the square root price increases by 7.226726.`
- `As the latitude of the house increases by one standard deviation, the square root price increases by 88.816082.`
- `As the longitude of the house increases by one standard deviation, the square root price increases by 11.343899.`
- `As the school rating increases by one standard deviation, the square root price increases by 27.353843.`
- `As the house has a public sewer system (sewer_PUBLIC) instead of a private one, the square root price increases by 6.584108.`
- `As the heat source for the house switches from something other than gas to gas, the square root price increases by 9.278196.`
- `As the heat source for the house switches from something other than gas/solar to gas/solar, the square root price increases by 3.607930.`
- `As the house is on a waterfront property, the square root price increases by 6.715330.`
- `As the house experiences a nuisance (as defined by the model), the square root price decreases by 6.073275.`
- `As the view from the house improves by one standard deviation, the square root price increases by 22.472439.`
- `As the house is adjacent to a greenbelt, the square root price increases by 7.161059.`
- `As the house is located closer to Elliot Bay (in Seattle), the square root price decreases by 25.286029.`
- `As the house is located closer to Lake Sammamish, the square root price increases by 75.729413.`
- `As the house is located closer to Lake Washington, the square root price decreases by 64.398218.`
- `As the house is located closer to Puget Sound, the square root price decreases by 16.004882.`

## Conclusion
This entire process included the above described data engineering techniques, as well as an extensive look at transforming variables, feature selection and elimination through trial and error. Different transformations on the price for example were attempted to normalize the distribution, but the decision was made to use the square root transformation as it lended itself to dealing with the upper and lower tails of the distribution of the price more efficiently. 

The rest of the data cleaning process also included dropping or filling in of missing values, removal of outliers, one hot encoding categorical variables as well as dropping all variables that presented themselves with a high variance inflation factor. The use of QQplots and histograms were used to check the distribution of residuals. 


## Four assumptions
The decisions of the creation of this model were based on the four assumptions with the method of justification, which are:

1. Linearity assumption: Scatterplots of the variables should represent some level of linearity aka correlation to the target variable. The use of scatterplots and correlation matrices were the method of justification for this assumption. 

2. Normality Assumption: Use of QQplots and Residual histograms were the method for justifying normality. 
The normality assumption in linear regression models refers to the assumption that the residuals (i.e., the difference between the observed and predicted values) are normally distributed. This assumption is important because many statistical tests and procedures used in linear regression models rely on the assumption of normality, including hypothesis testing, confidence intervals, and prediction intervals.

One way to check for normality of the residuals is by using a Q-Q plot (quantile-quantile plot). A Q-Q plot is a graphical tool that compares the distribution of the residuals to a normal distribution. If the residuals are normally distributed, the points in the Q-Q plot should follow a straight line. Any deviation from the straight line indicates that the residuals are not normally distributed. Specifically, if the points in the Q-Q plot deviate from the straight line in the tails of the distribution, it suggests that the residuals have heavier tails than a normal distribution. On the other hand, if the points in the Q-Q plot deviate from the straight line in the center of the distribution, it suggests that the residuals have a skewed distribution.

Another way to check for normality of the residuals is by using a histogram. A histogram is a graph that shows the frequency distribution of the residuals. If the residuals are normally distributed, the histogram should have a bell-shaped curve, with the majority of the residuals near the mean and fewer residuals towards the tails of the distribution. Any deviation from the bell-shaped curve indicates that the residuals are not normally distributed.

3. Homoscedasticity: Durbin-Watson score close to 2 indicates that the errors are approximately normally distributed with constant variance.

A Durbin-Watson score close to 2 generally indicates that the model's errors are approximately homoscedastic (i.e., the variance of the errors is constant across all levels of the predictor variables).

This is because a score close to 2 suggests that the errors are approximately normally distributed with constant variance, which is a key assumption of many regression models. When the errors are homoscedastic, it means that the variability of the dependent variable is relatively constant across different levels of the independent variables, which allows for more accurate estimation of the coefficients and predictions of the model.

4. Multicollinearity: VIF scores for independent variables. 

Variance Inflation Factors (VIFs) are a measure used to assess the degree of multicollinearity in a multiple regression model. Multicollinearity occurs when two or more independent variables in a regression model are highly correlated with each other, which can make it difficult to interpret the individual effects of each variable on the dependent variable.


## Final assessment and thoughts of the model
- When plotted the model residuals show a normalized distribution, satisfying the normality assumption although with fairly long tails. This is something to be added into the future work. 
- The Durbin-Watson score is almost exactly 2, satisfying the assumption of homoscedasticity. 
- The linearity assumption was satisfied through a rigorous look at the plots and in general can be a difficult metric to validate. 
- The skew level of the data is well within the acceptable range of -2 to 2 which is a vast improvement from the original model which was originally above 10. 
- The kurtosis level is outside the acceptable range of -7 to 7 at a score of ~8.5, but however is still a major improvement from the original model. This is one that should be looked at later. 
- The Jarque Beras score is a massive 35770 which will require further investigation for future work. My instincts tell me there still may be some major outliers that may be affecting this score as the QQplots appear to be for the most part okay. 



## Conclusion

`A positive coefficient indicates that as the corresponding independent variable increases, the square root of the price of the house also increases, while a negative coefficient indicates that as the corresponding independent variable increases, the square root of the price of the house decreases.`

`In this model, we see that the most important variable in predicting the square root of house prices is the latitude of the house, with a coefficient of 100.368386. This suggests that houses located further north tend to have higher prices. The next most important variable is water proximity, with Water_Lake Sammamish variable having a very high coefficient of 75.729, suggesting that houses located near this lake tend to have much higher prices than other houses. On the other hand, the Water_Lake Washington variable has a negative coefficient, indicating that houses located near this lake tend to have lower prices than other houses.`

`Other important variables include the grade of the house, the square footage of the house above ground, and the condition of the house, all with coefficients greater than 20. The number of bathrooms, square footage of the basement, and the size of the view from the house are also important, with coefficients greater than 15.`

`On the other hand, variables such as the square footage of the garage and the presence of a nuisance nearby have negative coefficients, indicating that houses with larger garages or located near nuisances tend to have lower prices. The year the house was built and the longitude of the house also have negative coefficients, suggesting that older houses and houses located further west tend to have lower prices.`

`Overall, these results suggest that there are many factors that contribute to the price of a house, and that location, house size and quality, and the presence of nearby amenities all play important roles in determining the square root of house prices.`


## Recommendations

For the purposes of Zillows ability to choose inventory in the King County Real Estate Market, I recommend looking at properties that are near Lake Sammish or that are further north that also is accompanied with a waterfront. Since the grade, condition, and number of bathrooms appear positively correlated to the price it would make sense to try and buy older homes in the aforementioned areas as older homes tend to be cheaper in terms of price. Taking these homes and ensuring the grade and condition are of high quality through either pre-assessed purchases or renovations, along with possibly adding bathrooms can raise the price for resell value. Picking houses near school districts of high rating can have an impact as well. 

Houses towards the west as well as ones that present nuisances clearly result in lower prices, so my recommendation would be to avoid buying houses that fit these parameters as it may result in "holding the bag" scenarios which could lead to longer times held with inventory. 

The only invalid metric that should probably be ignored for now(but explored further) is the size of the garage negatively affecting the price. I would not consider this to be an accurate assessment, but I do not want to exclude it from the model. 


#### Questions model can answer:

- `Should the house be on a waterfront?`
- `How far north should the houses be?`
- `What age should the house have?`
- `What level of renovations need to be performed on the houses, and when?`
- `Will the house price be affected by common nuisances? (eg. noise, construction, bugs)`
- `How far west should the house be before one should lose interest of the purchase?`
- `What average quality of schools in the surrounding area?`

## Future Work

In the future work, it is worth revisiting the value of the homes on the remaining waterfronts and seeing if there is any statistical significance. More exploration is needed but was not ready to be presented at this time. 

The views that are highlighted in the column_names.md documentation can be explored and onehotencoded and could be a potential candidate feature. 

Jarque Beras score and outliers of the dataset should be further explored. The use of 3 standard deviations from the mean being the metric for outliers could be expanded slightly as it appears this was still affected in a major way. 

Any independent variables that presented with a Variance Inflation factor above 5 should be looked at again to see if multicollinearity is an issue with these particular variables. 



```python

```
