# Forecast-swap-rate-using-ML-techniques
#### Input: 
 - Features (X): a set of time series representing 31 macro-economic indicators: unprocessed and have different available time horizons.
 - Target (Y): 6m differential, S(t+6m) - S(t), of the 10year-2year US swap rate, S(t) = R_10(t) - R_2(t) 
#### Data:
 - Y: file 'swap_data.xlsx'
 - X: from the 8th column of the sheet 'data_value' of the file 'blb ECO inidicatori significativi.xlsx' 
#### Objective: 
The objective is to build a out-of-sample and one-step-ahead forecasting tool for the last 3 years worth of data
consider the last 3 years of monthly forecasts (a total of 36 forecasts)
#### project model selection
To choose the appropriate technique to choose the most meaningful indicators to explain the target among 31 indicators. I consider between **Stepwise Regression** (choosing a subset of predictors) and **LASSO Regularization** (regularize the coefficient estimates). My aim is to choose the technique which gives me less mean squared error on the test set. 
- **Stepwise**: I choose the hybrid approach, i.e. the combination between forward selection and backward elimination. It starts with a model with no predictor. The at each step the variable that gives the greatest additional improvement to the fit is added to the model. After adding each new variable, the method may also remove any variables that no longer provide an improvement in the model fit.
  ![image](https://github.com/user-attachments/assets/3f55273f-2f32-433d-9715-d9392a003e49)

The threshold I choose to include or exclude features is p-value. After adding a feature, it fit the OLS and calculate the p-value, if its p-value is less than 0.05, then add in, if it’s greater than 0.1, than exclude.
- **LASSO**: A technique that regularizes the coefficient estimates, shrinks the coefficients towards zero. The lasso regression coefficient estimates (𝛽^𝐿 ) ̂ are the values that minimize:

$$sum_{i=1}^{n} \left( y_i - beta_0 - sum_{j=1}^{p} beta_j x_{ij} right)^2 + lambda sum_{j=1}^{p} |beta_j| = RSS + lambda sum_{j=1}^{p} |beta_j|$$

