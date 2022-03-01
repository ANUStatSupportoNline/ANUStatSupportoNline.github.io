# Negative binomial regression

This fact sheet presents a discussion on Negative Binomial regression and its importance in applied statistics.

## Contents

- [What is Negative binomial regression?](#what_is_NB_reg)
- [Relationship with Poisson regression](#Pois_and_NB)
- [Learning the model parameters](#NB_estimation)
- [Implementation](#NB_implementation)
    - [Implementation in R](#NB_in_r)
    - [Implementation in Stata](#NB_in_stata)
- [References](#NB_ref)

## <a class=anchor id=what_is_NB_reg></a> What is Negative binomial regression?

As discussed in the Poisson regression fact sheet, one of the limitations of the traditional Poisson regression model is that it assumes that the mean is equal to the variance. As in the Poisson regression case, in the negative binomial regression model, the response variable is assumed to be count data, but it relaxes the restrictive assumption that the variance is equal to the mean. 

Useful resources on negative binomial regression are the books [*Regression Analysis of Count Data*](http://faculty.econ.ucdavis.edu/faculty/cameron/racd2/) by Cameron and Trivedi (2013) and [*Modeling Count Data*](https://www.cambridge.org/core/books/modeling-count-data/BFEB3985905CA70523D9F98DA8E64D08) by Hilbe (2014).

## <a class=anchor id=Pois_and_NB></a> Relationship with Poisson regression

The negative binomial model is a generalization of the Poisson model. To see this, let us consider the random variable $Y\sim\text{Pois}(\lambda)$. If we let the parameter $\lambda$ be a gamma distributed random variable as

$$ \lambda\sim\mathcal{G}(\text{shape} = r,\; \text{scale}=p/(1-p)),$$

then $Y\sim\mathcal{NB}(r,\,p)$. Now, for simplicity, let us define $\alpha=\frac{p}{1-p}$, then 

$$ \mathbb{E}[Y] = r\alpha = \mu,\;\;\;\;\text{var}(Y) = r\alpha + r\alpha^{2} = \mu + \mu^{2}/r.$$

Therefore, we can see that in the negative binomial model, the mean does not need to be the same as the variance. One important thing to note is that unlike the Poisson distribution that has one parameter ($\lambda$), the negative binomial distribution has two parameters ($r,\; \alpha$). It is common to set $r$ as a fixed quantity determined by the researcher. 

As with other generalized linear models, we need to relate the mean of the negative binomial distribution ($\mu$) to the linear predictor ($\mathbf{x}'\boldsymbol{\beta}$). The most convenient way to do this, is by using the following link function

$$\log\left(\frac{\mu}{\mu + k}\right) = \mathbf{x}'\boldsymbol{\beta}, $$

where $\boldsymbol{\beta}$ is our vector parameter of interest.

## <a class=anchor id=NB_estimation></a> Learning the model parameters

As expected, our goal is to learn the parameter vector $\boldsymbol{\beta}$. This can be done in a variety of ways, but the most popular learning algorithm is maximum likelihood. The idea is to choose the set of parameters that maximizes the likelihood function.

## <a class=anchor id=NB_implementation></a> Implementation

Now, we are going to point out useful resources on how to implement negative binomial regression both in R and Stata.

### <a class=anchor id=NB_in_r></a> Implementation in R

Chapter 3 from the book [*Extending the Linear Model with R*](https://www.taylorfrancis.com/books/mono/10.1201/9781315382722/extending-linear-model-julian-faraway) presents in detail how to fit a negative binomial regression and other count data regression models in R as well as how to perform model diagnostics.

### <a class=anchor id=NB_in_stata></a> Implementation in Stata

In order to implement logistic regression models in Stata, we can follow the guide [*Negative Binomial Regression - STATA data analysis examples*](https://stats.oarc.ucla.edu/stata/dae/negative-binomial-regression/), developed by the IDRE from UCLA. 

## <a class=anchor id=NB_ref></a> References

+ Cameron, C. and Trivedi P.K. (2013). *Regression Analysis of Count Data*. Cambridge University Press.

+ Faraway, J. (2016). *Extending the Linear Model with R*. CRC Press.

+ Hilbe, J.M. (2014). *Modeling Count Data*. Cambridge University Press.

* UCLA: Statistical Consulting Group. Negative Binomial Regression - STATA data analysis examples. Retrieved from: https://stats.oarc.ucla.edu/stata/dae/negative-binomial-regression/.
