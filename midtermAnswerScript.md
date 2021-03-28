# Midterm Answers Script

```python

# A. Import the libraries you will need

from sklearn.datasets import fetch_california_housing
import numpy as np
import pandas as pd
from sklearn.preprocessing import StandardScaler as ss
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.model_selection import KFold
from sklearn.metrics import mean_squared_error

# B. Create your DoKFold

def DoKFold(model, X, y, k, standardize, random_state):
    if standardize:
        from sklearn.preprocessing import StandardScaler as SS
        ss = SS()

    kf = KFold(n_splits=k, shuffle=True, random_state=random_state)

    train_scores = []
    test_scores = []

    train_mse = []
    test_mse = []

    for idxTrain, idxTest in kf.split(X):
        Xtrain = X[idxTrain, :]
        Xtest = X[idxTest, :]
        ytrain = y[idxTrain]
        ytest = y[idxTest]

        if standardize:
            Xtrain = ss.fit_transform(Xtrain)
            Xtest = ss.transform(Xtest)

        model.fit(Xtrain, ytrain)

        ytest_pred = model.predict(Xtest)
        ytrain_pred = model.predict(Xtrain)

        train_scores.append(model.score(Xtrain, ytrain))
        test_scores.append(model.score(Xtest, ytest))

        train_mse.append(np.mean((ytrain - ytrain_pred) ** 2))
        test_mse.append(np.mean((ytest - ytest_pred) ** 2))

    return train_scores, test_scores, train_mse, test_mse

# C. Import the the California Housing data

data = fetch_california_housing()

# D.

# 1. set up X as your features from data.data
X = data.data
# 2. create a names object from data.feature_names
X_names = data.feature_names
# 3. set up y as your target from data.target
y = data.target
# 4. use pandas to create a data frame from your features and names object
df = pd.DataFrame(X, columns=X_names)

df

### 15. ###

# Which of the below features is most strongly correlated with the target?
# MedInc (median income)

# 1. create a data frame that has all of your features as well as your target
X_corr = df.copy()
# 2. calculate the correlations of all variables
X_corr.corr()

### 16. ###

# If the features are standardized, the correlations from the previous
# question do not change.

# 1. fit transform your features
Xs = ss.fit_transform(X)
# 2. create a data frame with the transformed data
Xs_df = pd.DataFrame(Xs, columns=columns)
# 3. add your target to the data frame
Xsy_df = Xs_df.copy()
Xsy_df['y'] = y
# 4. calculate correlations amongst all variables
Xsy_df.corr()

### 17 ###

# If we were to perform a linear regression using only the feature
# identified in question 15,
# what would be the coefficient of determination?
# Enter your answer to two decimal places: 0.47

np.round(np.corrcoef(df['MedInc'],y)[0][1] ** 2, 2)
lin_reg = LinearRegression()
lin_reg.fit(df['MedInc'].values.reshape(-1, 1), y)
np.round(lin_reg.score(df['MedInc'].values.reshape(-1, 1), y), 2)

### 18 ###

# What is the mean R2 value on the test folds?
#Enter your answer to 5 decimal places: 0.60198

# 1.  define k and model
k = 20
model = LinearRegression()
# 2.  Use DoKFold with LR()
train_scores, test_scores, train_mse, test_mse = DoKFold(model, X, y, k, True, 146)
# 3.  Output values
print(np.mean(train_scores), np.mean(test_scores))
print(np.mean(train_mse), np.mean(test_mse))

### 19 ###

# Next, try ridge regression.

# For the optimal value of alpha in this range, what is the mean R2 value on the test folds?
# Enter you answer to 5 decimal places: 0.60201

# 1.  define rid_a_range = to 101 values equally spaced between 20 and 30
rid_a_range = np.linspace(20, 30, 101)
# 2.  create an object to append calculated mean values from your ridge training data
rid_tr = []
# 3.  create an object to append calculated mean values from your ridge testing data
rid_te = []
# 4.  create an object to append calculated mean MSE values from your ridge training data
rid_tr_mse = []
# 5.  create an object to append calculated mean MSE values from your ridge testing data
rid_te_mse = []
# 6.  start a for loop
for a in rid_a_range:
    model = Ridge(alpha=a)
    train, test, train_mse, test_mse = DoKFold(model, X, y, k, True, 146)

    rid_tr.append(np.mean(train))
    rid_te.append(np.mean(test))
    rid_tr_mse.append(np.mean(train_mse))
    rid_te_mse.append(np.mean(train_mse))

# 7.  output requested values
idx = np.argmax(rid_te)
print(rid_a_range[idx], rid_tr[idx], rid_te[idx], rid_tr_mse[idx], rid_te_mse[idx])

### 20 ###

# Next, try Lasso regression.

# For the optimal value of alpha in this range, what is the mean R2 value on the test folds?
# Enter you answer to 5 decimal places: 0.00186

# 1.  define rid_a_range = to 101 values equally spaced between 20 and 30
las_a_range = np.linspace(0.001, 0.003, 101)
# 2.  create an object to append calculated mean values from your ridge training data
las_tr = []
# 3.  create an object to append calculated mean values from your ridge testing data
las_te = []
# 4.  create an object to append calculated mean MSE values from your ridge training data
las_tr_mse = []
# 5.  create an object to append calculated mean MSE values from your ridge testing data
las_te_mse = []
# 6.  start a for loop
for a in las_a_range:
    model = Lasso(alpha=a)
    train, test, train_mse, test_mse = DoKFold(model, X, y, k, True, 146)

    las_tr.append(np.mean(train))
    las_te.append(np.mean(test))
    las_tr_mse.append(np.mean(train_mse))
    las_te_mse.append(np.mean(train_mse))

# 7.  output requested values
idx = np.argmax(las_te)
print(las_a_range[idx], las_tr[idx], las_te[idx], las_tr_mse[idx], las_te_mse[idx])

### 21 ###

# Refit a linear, Ridge, and Lasso regression to the entire (standardized) dataset.

# Which of these models estimates the smallest coefficient for the variable that is least correlated
# (in terms of absolute value of the correlation coefficient) with the target?

#1. Identify the index number for the variable that is least correlated
print(X_names[5])
#2. Create your models lin =, rid = , las =
linear_model = LinearRegression()
ridge_model = Ridge(alpha = 25.8)
lasso_model = Lasso(alpha = 0.00186)
#3. fit your three models using your transformed features and target
linear_model.fit(Xs, y)
ridge_model.fit(Xs, y)
lasso_model.fit(Xs, y)
#4. extract the coefficients from each model using model_name.coef_[value_to_identify_variable]
linear_model.coef_[5], ridge_model.coef_[5], lasso_model.coef_[5]

### 22 ###

# Which of the above models estimates the smallest coefficient for the variable that is most correlated
# (in terms of the absolute value of the correlation coefficient) with the target?

#1. Identify the index number for the variable that is most correlated
print(X_names[0])
#2. extract the coefficients from each model using model_name.coef_[value_to_identify_variable]
linear_model.coef_[0], ridge_model.coef_[0], lasso_model.coef_[0]

### 23 ###

# If we had looked at MSE instead of R2 when doing our Ridge regression (question 19),
# would we have determined the same optimal value for alpha, or something different?

# different

idx = np.argmin(rid_te_mse)
print(rid_a_range[idx], rid_tr[idx], rid_te[idx], rid_tr_mse[idx], rid_te_mse[idx])

### 24 ###

# If we had looked at MSE instead of R2 when doing our Lasso regression (question 20),
# what would we have determined the optimal value for alpha to be?
#
# Enter your answer to 5 decimal places, for example: 0.00100

idx = np.argmin(las_te_mse)
print(las_a_range[idx], las_tr[idx], las_te[idx], las_tr_mse[idx], las_te_mse[idx])

```
