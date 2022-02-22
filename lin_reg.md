# Linear Regression

Throughout this fact sheet, we are going to discuss what is linear regression and its importance in applied statistics.

## Contents

- [What is linear regression?](#what_is_LR)
- [Simple vs. Multiple linear regression](#SLR_vs_MLR)
- [Model vs. Estimation approach](#LR_model_vs_estimation)
- [The residuals](#LR_residuals)
- [Ordinary Least Squares](#LR_OLS)
- [Model diagnostics](#LR_diagnostics)
- [Implementation](#LR_implementation)
    - [Implementation in R](#LR_in_r)
    - [Implementation in Stata](#LR_in_stata)
- [References](#LR_ref)

## <a class=anchor id=what_is_LR></a> What is linear regression?

Linear regression is one of the simplest and most intuitive approaches for statistical analysis and supervised learning. It is used to find or explain the relationship between a set of inputs (also known as explanatory variables, covariates or features), and a real-valued output (also known as the response variable). Note that in linear regression, the response must be a continuous variable, but the explanatory variables can be continuous, discrete or categorical. 

With linear regression we can determine how strong (or weak) is the relationship between the inputs and the output, and whether such relationship is linear. Additionally, we can use linear regression to predict what would be the value of the output given some inputs. In other words, we can use linear regression to predict the response variable. As we have seen, liner regression has many applications and it is fairly simple to understand and to implement in modern statistical packages. Therefore, it is not surprising that linear regression is widely used in almost all domains.

A nice and complete guide on linear regression and its implementation can be found in the books [*Applied Linear Regression Models*](https://ebookcentral.proquest.com/lib/anu/detail.action?docID=6198596) by Kutner et al. (2004), and [*Linear Models with R*](https://julianfaraway.github.io/faraway/LMR/) by Faraway (2014). Additionally, Chapter 11 from the book [*Mathematical Statistics with Applications*](https://au.cengage.com/c/isbn/9780495110811/) by Wackerly et al. (2007); Chapter 3 from [*An Introduction to Statistical Learning*](https://www.statlearning.com/) by James et al. (2021); and section 3.2 from the book [*The Elements of Statistical Learning*](https://web.stanford.edu/~hastie/ElemStatLearn/) by Hastie et al. (2009), are also great resources on linear regression. 

## <a class=anchor id=SLR_vs_MLR></a> Simple vs. Multiple linear regression

We denote a linear regression problem as a ***simple linear regression*** when the covariate space is made up of a single feature, in other words, we regress our response variable against one single explanatory variable. On the other hand, we denote a linear regression problem as a ***multiple linear regression*** if we regress our response variable against two or more explanatory variables. 

For instance, Chapters 1-5 from the book [*Applied Linear Regression Models*](https://ebookcentral.proquest.com/lib/anu/detail.action?docID=6198596) cover simple linear regression, whereas Chapter 6-11 cover multiple linear regression.

## <a class=anchor id=LR_model_vs_estimation></a> Model vs. Estimation approach

It is common to hear, especially among non-statisticians, statements like: "we are going to fit an OLS regression" or "linear regression finds the best fit by minimizing the squared residuals". At first sight, these statements may seem correct. However, they are not, as they are mixing the model with the estimation approach. 

Linear regression is a **model**, and this model is a function (also called a linear predictor) that maps from a set of covariates to a real-valued response. Such function is completely determined by a set of unknown learnable parameters. More formally, the model is 

<img src="https://render.githubusercontent.com/render/math?math=\Large y=f(\mathbf{x})=\mathbf{x}'\boldsymbol{\beta}\tag{+}\varepsilon,">

where <img src="https://render.githubusercontent.com/render/math?math=y"> is the response variable, the vector <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x}"> is our set of covariates, the vector <img src="https://render.githubusercontent.com/render/math?math=\boldsymbol{\beta}"> is our set of learnable parameters, and <img src="https://render.githubusercontent.com/render/math?math=\varepsilon"> is an error term assumed to be normally distributed with mean zero and unknown variance <img src="https://render.githubusercontent.com/render/math?math=\sigma^2">.

On the other hand, the **estimation approach** is the algorithm used to learn the unknown parameters, namely $\boldsymbol{\beta}$ and $\sigma^2$. Note that the model and the estimation approach are two different things. Popular estimation approaches to learn the unknown parameters in a linear regression model are: Ordinary least squares (OLS), Maximum likelihood estimation (MLE), Penalized least squares including ridge regression and the Lasso, among other learning algorithms.   

## <a class=anchor id=LR_residuals></a> The residuals

A crucial term in linear regression is *residuals*. The model residuals are the difference between the actual observed responses and the estimated linear predictor (or the fitted values). They measure how well our model fits the observed data, where larger residuals mean a worse fit. In fact, the residuals are a crucial component in the derivation of the OLS estimator for $\boldsymbol{\beta}$ and $\sigma^{2}$.

## <a class=anchor id=LR_OLS></a> Ordinary Least Squares

Ordinary least squares is the most popular learning algorithm used to estimate the unknown parameters from a linear regression problem. The idea is to choose the set of parameters that minimizes the sum of squared residuals. Under some assumptions, namely, when the errors are homoscedastic and serially uncorrelated, OLS is unbiased and have minimum variance; this is known as the Gauss-Markov theorem. Moreover, when the errors are normally distributed random variables, then the OLS estimator will be the same as the Maximum likelihood estimator. Generalizations of OLS are Weighted least squares (WLS) and Generalized least squares (GLS). Sections 1.6 and 6.3 from the book [*Applied Linear Regression Models*](https://ebookcentral.proquest.com/lib/anu/detail.action?docID=6198596), and Chapter 2 from [*Linear Models with R*](https://julianfaraway.github.io/faraway/LMR/) present a deeper discussion on OLS estimation, the Gauss-Markov theorem and the model residuals.

## <a class=anchor id=LR_diagnostics></a> Model diagnostics

The analysis from linear regression depends on various assumptions. Model diagnostics can be used to assess whether such model assumptions are met. We can also check if the fitted regression model captures the structure of the data or if there are any unusual observations that are interfering with the analysis. Furthermore, model diagnostics not only reveal deficiencies in a regression model, but may suggest how the model can be improved. 

For a broader discussion on model diagnostics see the materials from the [*Regression Diagnostics Workshop*](https://tinyurl.com/SORA-TABA-diagnostics) and the book [*Regression Diagnostics*](https://socialsciences.mcmaster.ca/jfox/Books/RegressionDiagnostics/index.html) both by John Fox, or Chapter 4 from [*Linear Models with R*](https://julianfaraway.github.io/faraway/LMR/), as both are great resources on model diagnostics for linear regression.

## <a class=anchor id=LR_implementation></a> Implementation

Throughout this section, we are going to present useful resources on how to implement linear regression in R and Stata.

### <a class=anchor id=LR_in_r></a> Implementation in R

The books [*An R Companion to Applied Regression*](https://socialsciences.mcmaster.ca/jfox/Books/Companion/index.html) by Fox and Weisberg (2019), and  [*Linear Models with R*](https://julianfaraway.github.io/faraway/LMR/) present in detail how to implement linear regression models in R, as well as how to interpret the R output. Additionally, we can also make use of the multiple R packages available to facilitate our analysis. For instance, we can easily obtain diagnostic plots for our model using the function

```{r}
gg_diagnose(fitted.lm)
```
from the package [```lindia```](https://cran.r-project.org/package=lindia), where ```fitted.lm``` is an ```lm``` object that contains a fitted regression

### <a class=anchor id=LR_in_stata></a> Implementation in Stata

In order to implement simple and multiple linear regression, and to perform model diagnostics in Stata, we can follow the guide [*Regression with Stata Chapter 1*](https://stats.idre.ucla.edu/stata/webbooks/reg/chapter1/regressionwith-statachapter-1-simple-and-multiple-regression/), developed by the IDRE from UCLA. 

## <a class=anchor id=LR_ref></a> References

* Faraway, J. (2014). *Linear Models with R*. CRC Press.

* Fox, J. (2020). *Regression Diagnostics*. Sage Publications.

* Fox, J. (2021). *Regression Diagnostics Workshop*. McMaster University.

* Fox, J., Weisberg, S. (2019). *An R Companion to Applied Regression*. Sage Publications.

* Hastie, T., Tibshirani. R., Friedman., J. (2009). *The Elements of Statistical Learning*. Springer Science & Business Media.

* James, G., Witten, D., Hastie, T., Tibshirani, R. (2021). *An Introduction to Statistical Learning (with Applications in R)*. Springer Science & Business Media.

* Kutner, M.H., Nachtsheim, C.J., Neter, J., Li, W. (2004). *Applied Linear Regression Models*. McGraw-Hill Education.

+ Lee. Y.Y., Ventura. S. (2017). ***lindia***: Automated Linear Regression Diagnostic. R package version 0.9. URL https://cran.r-project.org/web/packages/lindia/index.html.

* UCLA: Statistical Consulting Group. Regression with Stata Chapter 1. Retrieved from: https://stats.idre.ucla.edu/stata/webbooks/reg/chapter1/regressionwith-statachapter-1-simple-and-multiple-regression/.

* Wackerly, D.D., Mendenhall, W.III., Scheaffer, R.L., (2007). *Mathematical Statistics with Applications*. Thomson Learning, Inc.




