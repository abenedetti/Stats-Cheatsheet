# Stats-Cheatsheet

### 1) One variable regression model

![stats1](/imgs/stats1.png)

* the best model (choice of coefficients) has the smallest error terms

* residual sum of squares (RSS), also known as the sum of squared residuals (SSR) or the sum of squared estimate of errors (SSE)

![stats2](/imgs/stats2.png)

<br>

* total sum of squares (TSS or SST)

![stats3](/imgs/stats3.png)(of the baseline model)

<br>

* R<sup>2</sup>

![stats4](/imgs/stats4.png)

R<sup>2</sup> captures value added from using a model

  + R<sup>2</sup> = 0 means no improvement over baseline
  + R<sup>2</sup> = 1 means a perfect predictive model

R<sup>2</sup> is unitless and universally interpretable

  + can be be hard to compare between models
  + good models for easy problems will have R<sup>2</sup> near 1
  + good models for hard problems can still have R<sup>2</sup> near 0


### 2) Multiple linear regression model

![stats5](/imgs/stats5.png)

* the objective is selecting the best models coefficients (the coefficients that minimize SSE)

* adding more variables (features) can improve the model (this effect has a <i>cap</i> as more variables are added)

* not all variables should be used since each new variable requires more data and potentially can lead to <i>overfitting</i>. There is a trade off for the model: overfitting leads the model to perform well (high R<sup>2</sup>) on data used to create the model but worse on unseen data (new data we're interested in predicting the dependent variable value) *This number adjusts the R-squared value

* adjusted R<sup>2</sup> is used to account for the number of independent variables used relative to the number of data points. (Multiple) R<sup>2</sup> will always increase if you add more independent variables. But adjusted R<sup>2</sup> will decrease if you add an independent variable that doesn't help the model.

![stats6](/imgs/stats6.png)

* in the `summary` of the `lm` function in `R` there is information to help understand if a variable should be included in the model:

  + <i>estimate</i>: a coefficient of 0 (or not significantly different from 0) means that the value of the independent variable does not change our prediction for the dependent variable. Therefore we should probably remove the variable from our model, since it's not helping to predict the dependent variable
  
  + <i>standard error</i>: gives a measure of how much the coefficient is likely to vary from the estimate value
  
  + <i>t value</i>: gives the estimate divided by the standard error. It will be negative if the estimateis negative and positive if the estimate is positive. The larger the absolute value of the t value, the more likely the coefficient is to be significant.

  + <i>p value</i>: gives a measure of how plausible it is that the coefficient is actually 0, given the data we used to build the model. The less plausible it is, or the smaller the probability number in this column, the less likely it is that our coefficient estimate is actually 0. We want independent variables with small values in this column. 

  The <i>p value</i> will be large if the absolute value of the <i>t value</i> is small, and vice versa. 

  The `summary` of the `lm` function recaps it all in the level of <i>significance levels</i> (last column) 

* <i>multicollinearity</i> is a measure of the linear relationship between variables:
  
  + +1 means a perfect positive relationship
  
  + 0 means no linear relationship
  
  + -1 means a perfect negative relationship
  
  

<hr>
<b>References:</b><br>
<sub>https://en.wikipedia.org/wiki/Residual_sum_of_squares</sub><br>
<sub>https://ocw.mit.edu/courses/sloan-school-of-management/15-071-the-analytics-edge-spring-2017/lecture-and-recitation-notes/</sub><br>
<sub>https://en.wikipedia.org/wiki/Total_sum_of_squares</sub><br>
