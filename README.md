# Bike Rental Demand
## Section 1.1. Problem

As more Australian commuters are struggling with the hassle of sitting in a traffic jam while driving or
catching public transportation, rental bikes can be an ideal and affordable transportation option for those
who wants to commute short distances without the hassle. Moreover, with the increasing number of bike
hire companies in Sydney, the companies need to determine specific factors that could potentially affect
bike rental demand. The goal of this project is to make prediction on bike rental demand under various
circumstances based on relevant dataset and statistical models. 

- **Research Question:** “Which factors can potentially affect bike rental demand? Predict bike rental demand based on the factors” 
- **Null hypothesis H0** = There is no statistically significant relationship between the variables (hour and temperature) and the bike rental demand (count) 
- **Alternative hypothesis Ha** = There is statistically significant relationship between the variables (hour and temperature) and the bike rental demand (count)

## Section 1.2. Approach
Regression analysis is a reliable statistical model in identifying which factors have impact on a topic of
interest. Therefore, regression analysis will be performed as an approach to solve the research
question and make prediction on bike rental demand.

## Section 1.3. Data
The relevant dataset for this project was acquired from Kaggle which was uploaded by Capital Bikeshare.
The dataset is called ‘train.csv’ which contains hourly bike rental data from Washington D.C. between
early 2011 to end of 2012. Note that there are 12 variables and 10886 observations in the dataset. The
variables are explained as below:
- **datetime** - consists of hourly date in timestamp format.
- **season** - consists of integer values between 1 to 4 to indicate spring, summer, fall and winter
respectively.
- **holiday** - consists of boolean values 0 and 1 to indicate whether the date is holiday or not.
- **workingday** - consists of boolean values 0 and 1 to indicate whether the date is a working day
or not.
- **weather** - consists of integer values between 1 to 4 to indicate weather conditions where 1 =
clear or few clouds, 2 = mist and cloudy, 3 = light snow or rain and 4 = heavy rain or snow.
- **temp** - consists of temperature in Celsius
- **atemp** - consists of “feels like” temperature in Celsius
- **humidity** - consists of relative humidity level
- **windspeed** -consists of wind speed in mph
- **casual** - consists of number of non-registered user rentals
- **registered** - consists of number of registered user rentals
- **count** - consists of number of total rentals

## Section 1.4. Data Preparation
The dataset ‘train.csv’ was loaded and a data cleaning was performed before the explorative analysis by
using tools ‘python’, ‘numpy’ and ‘pandas’. Firstly, the integer values 1-4 in ‘season’ were converted to
string values ‘Spring’, ‘Summer’, ‘Fall’ and ‘Winter’ respectively in order to ensure these values are more
readable. In addition, the integer values 1-4 in ‘weather’ were converted to string values ‘clear or few
clouds’, ‘mist and cloudy’, ‘light snow or rain’ and ‘heavy rain or snow’ to indicate better representation of
weather conditions. Boolean values such as 0 and 1 in ‘holiday’ and ‘workingday’ variables were
converted to string values ‘No’ and ‘Yes’ to clearly understand whether the day is a holiday or working
day. After all of these data cleaning processes, the new dataset ‘train_cleaned.csv’ was exported and
saved with these modifications. Then all missing/null values were checked in ‘train_cleaned.csv’ by using
the command ‘isnull().sum()’ from pandas library and it was confirmed that there were 0 missing/null
values in each variables. Furthermore, 4 new variables called ‘year’, ‘month’, ‘dayofweek’ and ‘hour’ were
created based on the ‘datetime’ variable and added to the ‘train_cleaned.csv’ in order to make a more
detailed explorative analysis. There are no abnormalities observed in ‘train_cleaned.csv’ after the data
cleaning and the dataset has 16 variables and 10886 observations.

## Section 1.5. Explorative Analysis
Explorative analysis was performed by using visualisation tools ‘matplotlib’ and ‘seaborn’ in prior to
making any regression models and predictions. The visualisation are provided to summurise
number of bike rentals based on various variables (factors). The main objective of this summurisation is to
capture a general relationship between variables. Note that more results of visualisation and
summurisation can be found in ‘bike rental demand stage 1.ipynb’.

![1](https://user-images.githubusercontent.com/59059144/99245924-8ba4d280-2858-11eb-927b-67344e08b704.PNG)

**(figure 1. Boxplot of Rentals per season)**
This boxplot shows number of bike rentals based on different seasons. As you can see from the figure 1,
the number of rentals in spring is relatively low compared to summer and fall which indicates that season
can be one of the factors that affect number of bike rentals.

![2](https://user-images.githubusercontent.com/59059144/99246034-bd1d9e00-2858-11eb-9515-32facff21446.PNG)

**(figure 2. Pointplot of Rentals per day and hour)**
The point plot depicts number of bike rentals for weekdays and weekend in different hours between 12am
to 11pm. The peak hours of demand during weekdays are 8am when commuters need to go to
workplaces or schools and 5pm when commuters need to go home after working. On the other hand, the
peak hours of demand during weekend are between 12pm to 3pm. This shows that weekdays, weekend
and hour of the day can be one of the factors that affect number of bike rentals.

## Section 1.6. Evaluation Setup
**Paired t-test** 
Paired t-test will be performed between predictor variable and dependent variable to test reliability. The reliability will be assessed by p-value derive from the paired t-test.

**Paired Samples Correlations** 
Correlations will be evaluated in order to find the strength of linear relationship between predictor variable and dependent variable. Note that the correlation values will be between -1 to 1 where 1 is total positive correlation, 0 is no correlation, and -1 is negative correlation.

**R squared** 
R squared will be evaluated and used as indication of how well the model fits our data. Note that R squared is ranged 0 to 1 where the higher values indicate a better fit.

**K-fold Cross Validation** 
10-fold cross validation will be performed to validate our model in order to select the best model with the lowest cross-validation score that would perform best on the testing data. The train set will be randomly shuffled and ⅓ of the data from the train set will be used as test set. Then the remaining test set into 10. In each iteration, compare the performance of all of these datasets to find the lowest cross-validation score. It is also used to prevent overfitting.

**Root Mean Squared Logarithmic Error (RMSLE)**
RMSLE will be used to measure the accuracy of our model. RMSLE is calculated as:

![3](https://user-images.githubusercontent.com/59059144/99247611-4cc44c00-285b-11eb-870a-66ca12acda9f.PNG)

Where where n is the number of observations, pi is our predicted count, and ai is the actual count. Note that smaller RMSLE value means more accurate model.

## Section 2: Approach

**Paired t-test**

![4](https://user-images.githubusercontent.com/59059144/99247789-8c8b3380-285b-11eb-8245-05c9e5611935.PNG)

Paired t-test was the first approach that is performed in order to test reliability with the p-value so we can decide whether to reject or accept our null hypothesis. As you can see from the table above:

 - The p-value between temp and count is .000 which is less than 0.05
 - T p-value between hour and count is .000 which is less than 0.05

Hence we can reject the null hypothesis and confirm that there is statistically significant relationship between the variables (hour and temperature) and the bike rental demand (count).

**Correlation Analysis**

![5](https://user-images.githubusercontent.com/59059144/99247954-d5db8300-285b-11eb-8638-cfd0a754a600.PNG)

By evaluating correlations, we can understand which predictor variables are strongly correlated with the dependent variable ‘count’. From the table above, we can clearly see that ‘temp’ and ‘hour’ are highly correlated to ‘count’. However, ‘humidity’ is negatively correlated to ‘count’ as people tend not to travel on bike when the weather is humid.

**Model Building**
After analysing feature engineering, paired t-test and correlation analysis, we are going to build some models to predict the bike sharing demand by using two datasets ‘train.csv’ and ‘test.csv’. We will be using the scikit-learn library from Python. Note that our models will be evaluated by R squared, 10-fold cross validation and RMSLE as we mentioned in section 1.

 1.Linear Regression (baseline) Initially, we built a simple linear regression model as our baseline by using the ‘temp’ and ‘hour’ as predictor variables against the dependent variable ‘count’. This model achieved 0.41369 R squared which indicates a weak fit. Moreover, the 10-fold cross validation score and RMSLE on this model achieved 1.04814.

2.Linear Regression with more predictor variables (benchmark model) Since our baseline achieved really bad results, we are required to build benchmark model in order to make a more accurate prediction on the bike sharing demand. Firstly, we used more predictor variables ‘temp’, ‘hour’, ‘season’, ‘weather’, ‘atemp’, ‘humidity’,’year’, ‘dayofweek’, ‘holiday’ and ‘workingday’ against the dependent variable ‘count’ to build the model. Then we made prediction on X_train set. This model achieved 0.48527 R squared which still indicates weak fit. Also the model achieved 0.98131 for the 10-fold cross validation and 0.98036 for the RMSLE.

3.Random Forest (benchmark model) Another benchmark model was built by random forest to check if this model is more accurate than the previous benchmark model. The first step for constructing random forest is we select N samples from the train set by using random sampling. Then we select K features randomly from all of the features in order to make the decision tree by using these features. Iterating these two steps M times will give us M decision tree model which is the formation of random forest. Lastly, after each tree decision, we make predictions. This model achieved 0.99347 R squared which indicate good fit. Also the model achieved 0.28837 for the 10-fold cross validation and 0.10701 for the RMSLE.

## Section 3: Results
**1. Linear Regression (baseline)**

![6](https://user-images.githubusercontent.com/59059144/99278281-f7039a00-2882-11eb-8494-f7852739cb3b.PNG)

Our baseline shows the weakest fit compare to the linear regression model with more predictors and random forest model as its R squared value is 0.41369. Although we used the two most strongly correlated variables ‘temp’ and ‘hour’ to the dependent variable ‘count’, this base model provided a poor result with the 10-fold cross validation and RMSLE value 1.04814. This indicates that we would need more predictor variables to improve the linear regression model. Hence, further feature selection is required for improvements.

**2. Linear Regression with more predictor variables (benchmark model)**

![7](https://user-images.githubusercontent.com/59059144/99278418-20242a80-2883-11eb-9674-80414290f1b0.PNG)

The linear regression model with more predictors scored 0.48527 for the R squared value which still indicates a weak fit but better than our baseline. As you can see from the above table, the values for 10-fold cross validation and RMLES are improved compare to our baseline. This confirms that selecting more features based on the correlation analysis could improve the linear regression model. However, the result is still considered as poor due to the complexity of the dataset . Since there are too many observations and variables in the dataset, linear regression may not be suitable for predicting the bike share demand.

![8](https://user-images.githubusercontent.com/59059144/99278503-3d58f900-2883-11eb-98bd-c4aecb0441b1.PNG)

This first graph shows that the linear model has a weak fit due to poor R squared value. The second and third graphs show the distribution of train and test results and it is visually clear that our prediction based on linear regression is poor since they are not relatively identical.

**3.Random Forest (benchmark model)**

![9](https://user-images.githubusercontent.com/59059144/99278628-67aab680-2883-11eb-848b-c9455c3b25bc.PNG)

The random forest model gives the value 0.99347 for R squared which indicates good fit and it is much better than the previous models. As you can see from the table above, it is clear that the random forest model performs best compare to the previous models as its 10-fold cross validation is 0.28837 and RMSLE is 0.10701. In addition, GBM package can be used to improve efficiency of the model and capacity of decision tree.

![10](https://user-images.githubusercontent.com/59059144/99278803-9e80cc80-2883-11eb-8415-e8beace27fc3.PNG)

This first graph shows that the random forest model has a good fit due its R squared value. The second and third graphs show the distribution of train and test results and it is visually clear that our prediction based on random forest is relatively accurate since they are relatively identical.

## Section 4: Conclusion
Throughout the ‘bike rental demand’ study, I have learnt that the ‘temp’ and ‘hour’ variables are the two most important factors which affects the bike rental demand. However, I have also learnt that other factors such as ‘season’ and ‘weather’ are also significant in making predictions on the bike rental demand as I got the poor result from the linear regression model with only two variables (‘temp’ and ‘hour’). As a data analyst, this study was ideal to experience the real-world company’s problem that could be potentially applied to Australian’s bike rental companies. After comparing the baseline with the benchmark models, I was able to predict the bike rental counts with relatively high accuracy by using random forest. In future, different models such as time series and neural network can be performed to make more predictions.
