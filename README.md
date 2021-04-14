# Salary Prediction Portfolio
Salary Prediction Project
## Table of contents
* [Introduction](#introduction)
* [Technologies](#technologies)
* [Goal](#goal)
* [Dataset](#dataset)
* [Methodology](#methodology)
* [Models Used](#models-used)
* [Model Results and Selection](#model-results-and-selection)
## Introduction
A relatively new company would like to predict employees' annual salary based on specific attributes in order to make competitive job offers to new hires. 
## Technologies
Python
## Goal
The goal for this analysis is to be able to predict the salary for a job position based on certain attributes.
## Dataset
The data includes 1,000,000 observations and the following variables:
<br>
*jobId:* Unique identifier for each employee 
<br>
*salary:* fixed payment per year 
<br>
*companyId:* Identifier for each company 
<br>
*jobType:* Position held within the company (CEO, CFO, CTO, Vice President, Manager, Janitor, Senior, or Junior) 
<br>
*degree:* educational degree (Doctoral, Masters, Bachelors, High School, or None) 
<br>
*major:* concentration of study 
<br>
*industry:* general field of work 
<br>
*yearsExperience:* how many years of work experience 
<br>
*milesFromMetropolis:* how many miles away the job is from a major city
![Dataview](./img/dataview.png)
## Methodology
1. *Data Understanding and Data Cleaning:* Lengths and types of the variables were determined and data was checked for missing values and duplicates. Since the dataset contains 1 million records and only five missing values were found, removal was deemed appropriate. <br />
![Datacleaning](./img/datacleaning.png)
2. *Exploratory Analysis:* Created visualizations to explore the target variable and examine the potential existance of outliers or corrupt data. Further visualized the relationship between the target and the feature variables and relationships between features.
![Targetviz](./img/targetviz.png) ![Heatmap](./img/heatmap.png) <br />
The average salary is approximately $110,000 and salary is normally distributed. The heatmap shows that degree and major are highly correlated.
3. *Feature Selection and Feature Engineering:* Removed features that could potentially create noise and accessed the validity of removal through backward elimination. Used ordinal encoding on degree and job type and one-hot encoding on major and industry in order to be used in the model. Since regression will be used, I applied standardization to ensure that one feature doesn't influence the model more than the others. I used VIF to ensure multicollinearity doesn't exists amongst the features.
![Backwardelim](./img/backwardelim.png) ![Vif](./img/vif.png)
4. *Model Building and Evaluation:* Established a Baseline Model, using Linear Regression, and evaluated based on MSE and R-squared. Developed 3 other models in order to improve upon baseline model. <br />
![Baselinescatter](./img/baselinescatter.png) ![Baselinedist](./img/baselinedist.png)
5. *Scoring the Dataset:* Model with lowest MSE and highest R-squared was selected for salary prediction. The baseline model results were an R-sqaured of 74% and a MSE of 395.
## Models Used
Linear Regression: Baseline
<br>
Linear Regression with Polynomial Transformation: When I plotted the model previously, the data showed some curvature. If we applyed polynomial transformation to the features, a quadratic curve will potentionally fit the data better than a linear one.
<br>
Random Forest: Since the data consists of largely categorical features, I choose this model to see if it would perform better.
<br>
Gradient Boosting: For the same reason as Random Forest and this model will help minimize errors.
## Model Results and Selection
### Model 1: Linear Regression - Polynomial Transformation
![Polydist](./img/polydist.png)
<br>
The best hyperparameters selected by the model were: linearregression__fit_intercept: False, linearregression__normalize: True, polynomialfeatures__degree: 2
<br>
**Results: MSE: 359, R-squared: 76%**
<br>
### Model 2: Random Forest
![Randomforestdist](./img/randomforestdist.png)
<br>
The best hyperparameters selected by the model were: max_depth=15, min_samples_leaf=20, min_samples_split=10, n_estimators=186
**Results: MSE: 371, R-squared: 75%**
<br>
### Model 3: Gradient Boosting
![Gradientboostingdist](./img/gradientboostingdist.png)
<br>
The best hyperparameters selected by the model were: learning_rate=0.1, max_depth=5, max_features=1.0, min_samples_leaf=3, n_estimators=300
**Results: MSE: 358, R-squared: 76%**
<br>
**Final Model Selected: Gradient Boosting**

The distribution plot for the choosen model shows that the predicted values are very close to the actual values with a bit of an overestimation in salaries from $105,000 to $160,000.<br />
<br>
The plot below demostrates the level of importance of each feature on salary. The feature with the highest influence on Salary is job type.
![Featureimp](./img/featureimp.png)<br />
