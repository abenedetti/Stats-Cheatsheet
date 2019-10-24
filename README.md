# Stats-Cheatsheet

### 1) One variable regression model

![stats1](/stats1.png)

* the best model (choice of coefficients) has the smallest error terms

* residual sum of squares (RSS), also known as the sum of squared residuals (SSR) or the sum of squared estimate of errors (SSE)

![stats2](/stats2.png)

<br>

* total sum of squares (TSS or SST)

![stats3](/stats3.png)(of the baseline model)

<br>

* R<sup>2</sup>

![stats4](/stats4.png)

R<sup>2</sup> captures value added from using a model

  + R<sup>2</sup> = 0 means no improvement over baseline
  + R<sup>2</sup> = 1 means a perfect predictive model

R<sup>2</sup> is unitless and universally interpretable

  + can be be hard to compare between models
  + good models for easy problems will have R<sup>2</sup> near 1
  + good models for hard problems can still have R<sup>2</sup> near 0


### 2) Multiple linear regression model

![stats5](/stats5.png)

* The objective is selecting the best models coefficients (the coefficients that minimize SSE)

* Adding more variables (features) can improve the model (this effect has a <i>cap</i> as more variables are added)

* Not all variables should be used since each new variable requires more data and potentially can lead to <i>overfitting</i>. There is a trade off for the model: overfitting leads the model to perform well (high R<sup>2</sup>) on data used to create the model but worse on unseen data (new data we're interested in predicting the dependent variable value) 



<hr>
<b>References:</b><br>
<sub>https://en.wikipedia.org/wiki/Residual_sum_of_squares</sub><br>
<sub>https://ocw.mit.edu/courses/sloan-school-of-management/15-071-the-analytics-edge-spring-2017/lecture-and-recitation-notes/</sub><br>
<sub>https://en.wikipedia.org/wiki/Total_sum_of_squares</sub><br>
