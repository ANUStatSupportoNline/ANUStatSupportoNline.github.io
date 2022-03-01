# Poisson regression

in this fact sheet, we are going to discuss what is Poisson regression and its importance in applied statistics.

## Contents

- [What is Poisson regression?](#what_is_Pois_reg)
- [Log link function](#log_link_pois)
- [Learning the model parameters](#pois_estimation)
- [Dispersion parameter](#pois_Dispersion)
- [Implementation](#pois_implementation)
    - [Implementation in R](#pois_in_r)
    - [Implementation in Stata](#pois_in_stata)
- [References](#pois_ref)

## <a class=anchor id=what_is_Pois_reg></a> What is Poisson regression?

Similar to logistic regression, Poisson regression is a generalized linear model. However, in Poisson regression, we are interested in modelling count data and contingency tables. More precisely, it assumes that the response variable is a Poisson distributed random variable, where the mean of the Poisson distribution is related to the linear predictor trough a link function. The most popular link function in Poisson regression is the log link, which in fact, is the canonical link. 

A seminal resource on Poisson regression is chapter 3 from the book [*Extending the Linear Model with R*](https://www.taylorfrancis.com/books/mono/10.1201/9781315382722/extending-linear-model-julian-faraway) by Faraway (2016).

## <a class=anchor id=log_link_pois></a> Log link function

Let us assume that $Y_{i}$ is a Poisson distributed random variable with mean $\mu_{i}$, for $i=1,\dots,\,n$. Moreover, by the properties of the Poisson distribution, we have that $\mathbb{E}[Y_{i}] = \text{var}(Y_{i}) = \mu_{i}$. This means that the Poisson model assumes that the mean of each observation is equal to its variance, which may be a quite restrictive assumption. In other fact sheets, we will consider Negative Binomial regression, which relaxes this assumption.

Going back to the Poisson case, we now want to relate $\mu_{i}$ to the linear predictor $\mathbf{x}_{i}'\boldsymbol{\beta}$. The most natural way is to use the canonical link. More formally, we will relate $\mathbf{x}_{i}'\boldsymbol{\beta}$ and $\mu_{i}$ as

$$\log{\mu_{i}} =\mathbf{x}_{i}'\boldsymbol{\beta}. $$

Note that as in logistic regression models, this models also has a linear predictor and a link function, and our goal is to learn the parameter vector $\boldsymbol{\beta}$. 

## <a class=anchor id=pois_estimation></a> Learning the model parameters

This section closely resembles our fact sheet on logistic regression. As in logistic regression, our goal is to learn the parameter vector $\boldsymbol{\beta}$. This can be done in a variety of ways, but the most popular learning algorithm is maximum likelihood. As expected, the idea is to choose the set of parameters that maximizes the likelihood function.

Nonetheless, there are other popular learning algorithms, including penalized likelihood. See for example, the work by Friedman et al. (2010) [Regularization Paths for Generalized Linear Models via Coordinate Descent](https://doi.org/10.18637/jss.v033.i01).

## <a class=anchor id=pois_Dispersion></a> Dispersion parameter

As discussed earlier, the Poisson distribution assumes that $\mathbb{E}[Y_{i}] = \text{var}(Y_{i}) = \mu_{i}$, which may be quite restrictive for some applications. Nonetheless, we can introduce a dispersion parameter in the model. This parameter can captures over- or under-dispersion. Let us define $\phi$ as the dispersion parameter, such that, $\text{var}(Y) = \phi\mu$. Note that in the traditional Poisson regression we set $\phi=1$, while $\phi>1$ is used to account for overdispersion and $\phi<1$ is used for underdispersion. The parameter $\phi$ is unknown, but it can be estimated as 

$$\hat{\phi}=\frac{\sum_{i}(y_{i} - \hat{\mu}_{i})^{2}/\hat{\mu}_{i}}{n-p}, $$

where $\hat{\mu}_{i}$ is the maximum likelihood solution for $\mu_{i}$, and $p$ is the dimension of the parameter vector $\boldsymbol{\beta}$.

## <a class=anchor id=pois_implementation></a> Implementation

Now, we are going to point out useful resources on how to implement Poisson regression both in R and Stata.

### <a class=anchor id=pois_in_r></a> Implementation in R

Chapter 3 from the book [*Extending the Linear Model with R*](https://www.taylorfrancis.com/books/mono/10.1201/9781315382722/extending-linear-model-julian-faraway) presents in detail how to fit a Poisson regression in R as well as how to perform model diagnostics.

### <a class=anchor id=pois_in_stata></a> Implementation in Stata

In order to implement logistic regression models in Stata, we can follow the guide [*Poisson Regression - STATA data analysis examples*](https://stats.oarc.ucla.edu/stata/dae/poisson-regression/), developed by the IDRE from UCLA. 

## <a class=anchor id=logit_ref></a> References

+ Faraway, J. (2016). *Extending the Linear Model with R*. CRC Press.

+ Friedman, J. H., Hastie, T., Tibshirani, R. (2010). Regularization paths for generalized linear models via coordinate descent. *Journal of Statistical Software*. 33(1), 1–22.

* UCLA: Statistical Consulting Group. Poisson Regression - STATA data analysis examples. Retrieved from: https://stats.oarc.ucla.edu/stata/dae/poisson-regression/.