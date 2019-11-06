# Stats-Cheatsheet

### 1) One variable regression model

![stats1](/imgs/stats1.png)

* the best model (choice of coefficients) has the smallest error terms

* residual sum of squares (RSS), also known as the sum of squared residuals (SSR) or the sum of squared estimate of errors (SSE)

![stats2](/imgs/stats2.png)

* Root Mean Square Error (RMSE) normalized by N (units of dependent variable)

![stats7](/imgs/stats7.png)

<br>

* total sum of squares (TSS or SST)

![stats3](/imgs/stats3.png)(of the baseline model)

*Question:* Why is the mean being computed on training data for SST and not on test data?

*Answer:* (amar_jonath): The SST computes the sum of squared errors of our baseline model. This baseline model predicts the mean of the target variable in the TRAINING set and not the test set, which is unknown.

The rationale behind that is that you don't have the information of the variable you are trying to predict in your test set while making your prediction, so it cannot be part of your baseline model at all - even if it's just the mean. This is the base behind offline learning.

There is also an alternative framework known as "online learning" where one can indeed use the test data (or the average thereof) for prediction. Online learning is a rich and deep field under active research and, unfortunately, is beyond the scope of this class.

* R<sup>2</sup>

![stats4](/imgs/stats4.png)

R<sup>2</sup> captures value added from using a model (or a measure of how much of the variance in y is explained by the model)

  + R<sup>2</sup> = 0 means no improvement over baseline
  + R<sup>2</sup> = 1 means a perfect predictive model

R<sup>2</sup> is unitless and universally interpretable

  + can be be hard to compare between models
  + good models for easy problems will have R<sup>2</sup> near 1
  + good models for hard problems can still have R<sup>2</sup> near 0

R<sup>2</sup> is also the square of the correlation between the actual and predicted outcomes

### 2) Multiple linear regression model

![stats5](/imgs/stats5.png)

* the objective is selecting the best models coefficients (the coefficients that minimize SSE)

* adding more variables (features) can improve the model (this effect has a <i>cap</i> as more variables are added)

* not all variables should be used since each new variable requires more data and potentially can lead to <i>overfitting</i>. There is a trade off for the model: overfitting leads the model to perform well (high R<sup>2</sup>) on data used to create the model but worse on unseen data (new data we're interested in predicting the dependent variable value)

* adjusted R<sup>2</sup> is used to account for the number of independent variables used relative to the number of data points. (Multiple) R<sup>2</sup> will always increase if you add more independent variables. But adjusted R<sup>2</sup> will decrease if you add an independent variable that doesn't help the model.<br>
<sub>When we remove insignificant variables, the "Multiple R-squared" will always be worse, but only slightly worse. This is due to the nature of a linear regression model. It is always possible for the regression model to make a coefficient zero, which would be the same as removing the variable from the model. The fact that the coefficient is not zero in the intial model means it must be helping the R-squared value, even if it is only a very small improvement. So when we force the variable to be removed, it will decrease the R-squared a little bit. However, this small decrease is worth it to have a simpler model.</sub>

On the contrary, when we remove insignificant variables, the "Adjusted R-squred" will frequently be better. This value accounts for the complexity of the model, and thus tends to increase as insignificant variables are removed, and decrease as insignificant variables are added.

* the in-sample (training set) R<sup>2</sup> will improve as the model includes more independent variables, but not necessarily the out of sample (test set) R<sup>2</sup>

* R<sup>2</sup> is negative when the model fits the data worse than the horizontal line (the baseline model).


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
  
  it occurs when the various independent variables are correlated, and this might confuse the coefficients (the betas) in the model
  
  multicollinearity is checked against excessively high values and signs (if intuition suggest a different sign you have to check)
  
  
### 3) Logistic regression

![stats10](/imgs/stats10.png)

* linear regression would predict a continuous outcome. With *logistic regression* we extend the idea of linear regression to situations where the outcome variable (dependent) is categorical

* we use the *logistic response function* which is a non linear regression equation to produce number between 0 and 1

  + we can instead talk about *Odds* (like in gambling)

    Odds > 1 if y = 1 is more likely
  
    Odds < 1 if y = 0 is more likely
    
    ![stats8](/imgs/stats8.png)

  + we define the *Logit* as follow [the bigger the Logit is, the bigger P(y = 1)]

![stats9](/imgs/stats9.png)


  + if we have a coefficient *c* for a variable, then that means
  
    + the *log odds (or Logit)* are increased by *c* for a unit increase in the variable

    + the *odds* are multiplied by *e^c* for a unit increase in the variable

* the outcome of a logistic regression model is a probability, so to make a binary prediction we're using a *threshold value t*:

  + P(y = 1) >= t predicts a binary prediction 0
  
  + P(y = 1) < t predicts a binary prediction 1
  
  the t value is generally based on the *better* errors. With no preferences between errors we select t=0.5 or the more likely outcome
  
* classification (confusion) matrix is used to compare actual vs predicted outcomes

  + a model with a higher threshold will have a lower sensitivity and a higher specificity.
  
  + a model with a lower threshold will have a higher sensitivity and a lower specificity.

  <sub>Sensitivity = Recall or True positive rate</sub><br>
  <sub>Specificity = True negative rate)</sub>

![stats11](/imgs/stats11.png)

* Receiver Operator Characteristic curve or ROC curve can help picking which value of the threshold is best

  it captures all thresholds simultaneously:
  
  + high treshold (high specificity / low sensitivity)
  + low treshold (low specificity / high sensitivity)

  generally we choose the best threshold for best trade off based on:
    + the cost of failing to detect positives
    + cost of raising false alarms

![stats12](/imgs/stats12.png)

* Area under the curve (AUC) show an absolute measure of quality of prediction (it's the perecentage of time that our model will do a correct classification)

![stats13](/imgs/stats13.png)

* full confusion matrix and metrics

![stats14](/imgs/stats14.png)

### 4) Classification and regression trees (CART)

* when there's the need of an interpretable model with which you can easily understand the importance of factors/coefficients and make a new prediction at ease, CART are preferred Vs logistic regression

* CART let you:
  + build a tree by splitting on variables
  + predict the outcome of a new observation by following the splits
  + have an interpretabel model that does not assume to be linear

![stats15](/imgs/stats15.png)


<hr>
<b>References:</b><br>
<sub>https://en.wikipedia.org/wiki/Residual_sum_of_squares</sub><br>
<sub>https://ocw.mit.edu/courses/sloan-school-of-management/15-071-the-analytics-edge-spring-2017/lecture-and-recitation-notes/</sub><br>
<sub>https://en.wikipedia.org/wiki/Total_sum_of_squares</sub><br>
<sub>https://en.wikipedia.org/wiki/Root-mean-square_deviation</sub><br>
