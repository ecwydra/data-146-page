#  Project 3

## Question 1

Training: 0.019
Testing: -0.002

Number of splits: 20

Interpretation: I assigned 10 splits initially, but then played around with different numbers of splits. I noticed that around 20 splits the r squared value got the closest to 1. The numbers from 20 splits are listed above. Given the training scores, testing scores, and external r squared value (testing score), I'm assessing the model created as poorly fit. If the r squared value were higher then I would say the model was better fit. 

## Question 2

Training: 0.019
Testing: 0.003

Number of splits: 10

Interpretation: I approached this problem the same way I approached question 1. I had initially assigned a value of 5 for the number of splits. After playing around with the number a little, I found that the best number of splits was again 10. It makes sense that the number of splits wouldn't change from an OLS model without standardized data to and OLS model based off of standardized data, because the number of data points was the same just with different values. This model is also poorly fit given the values listed above. The value I place the most weight on when determining if the model is fit well is the external validity (testing score), which is far from 1.

## Question 3

Training score for this value: 0.019
Testing score for this value: 0.019

Number of splits: 10

Interpretation: For this question I standardized the data, and reached a similar conclusion to the two previous problems. The testing and training scores are close, which is a good sign, but the r2 value for the testing data is still really low. This leads me to conclude that this model is still not fit correctly.

## Question 4

Interpretation: I found that after training and testing the models on the actual prices in the boston housing data set the models still performed poorly. My two main criticisms are the same: the training score and testing score aren't consistently close enough together and the r2 of the testing data is still too low to consider the model to be well fit.

Nonstandardized OLS

Training: 0.004
Testing: -0.062

Standardized OLS

Training: 0.004
Testing: -0.017

Ridge Regression

Training score for this value: 0.004
Testing score for this value: -0.015

## Question 5

Nonstandardized OLS - 0.246

Standardized OLS - 0.230

Ridge Regression - 0.273

Interpretation: The model with the highest r2 score is the ridge regression model, then the nonstandardized OLS, then the standardized OLS. On one hand, I could say that this means that the ridge regression model is the best fit model out of all three and therefore the one to use, but I think what's more realistic is that just using the r2 value to compare models isn't the best way to go. The problem with comparing r2 values from one model to the next is that in one of these models the variables were transformed. This could be throwing off the r2 value and then comparing it to other values wouldn't be accurate. Another thing to consider is the entire plot of testing scores vs training scores. The r2 value of a snapshot in the data isn't the best thing to interpret. It would be more accurate to plot the r2 data, thereby determining which of the models truly fits the best given all data points, and not just one.

## Question 6

My assessment is that the model with the best results, in this case the ridge regression, is neither only overfit nor underfit; it's likely both. The reason the r2 value alone doesn't reflect that is because having a single r2 value is having only a snapshot of how the data appears to be behaving. In reality, the best way to see how each model is behaving is to plot the training data along the validation data (r2). In the event that the training data and r2 validation data are similar, the model would fit. If there's high training and high testing error the model would be overfit, and if there's low training error with high testing error then the model would be underfit. The data mentioned in previous questions suggests that the model is underfit in areas, and overfit in other areas. My suggestions to zillow would be the following:

* add more data (more to train and test on is always a good idea)
* clean up the data a little (the columns with zip codes should be melted into one column)
* try building the model with more specialized data. In the models I created most of the features were included, which likely made it more difficult to interpret the results.
* add more hyperparameters! In class we talked about tuning a model using hyperparameters, and I think more of that could be done here to result in a better fit model.

