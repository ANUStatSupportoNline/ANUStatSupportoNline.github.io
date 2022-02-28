# Logistic regression

Throughout this fact sheet, we are going to present useful resources on logistic regression.

## Contents

- [What is logistic regression?](#what_is_Logit)
- [Logit link function](#logit_link)
- [Learning the model parameters](#logit_estimation)
- [The residuals](#logit_residuals)
- [Model diagnostics](#logit_diagnostics)
- [Binomial regression](#binom_reg)
- [Implementation](#logit_implementation)
    - [Implementation in R](#logit_in_r)
    - [Implementation in Stata](#logit_in_stata)
- [References](#logit_ref)

## <a class=anchor id=what_is_Logit></a> What is logistic regression?

<div style="text-align: center;">
  <img src="/assets/images/logit_reg_plot.png" alt="Logistic_reg"
             width = "450" 
             height = "450">
</div>

As discussed in previous fact sheets, the linear regression model assumes that the response is real-valued and the error term is a normally distributed random variable. 

However, in many cases we would like to model a non-real-valued, but binary, response variable based on a set of explanatory variables. For example, our response variable might be: malignant or benign tumor; fraudulent or not fraudulent; or accepted vs rejected, among others. In such cases, we can easily encode our qualitative responses using an indicator function. That means that conditional on the set of covariates, the responses would be Bernoulli distributed random variables. Therefore, it makes sense to model the probability that the response equals one given all the covariates, i.e.,

<img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y = 1 |X).">

But, naturally, one question arises: How can we relate the covariates, <img src="https://render.githubusercontent.com/render/math?math=X">, with <img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y=1|X)">? Using a link function! More specifically, a logit link function, which is going to be presented in the [next subsection](#logit_link).

For a deeper understanding of logistic regression we can refer to the book [*Applied Logistic Regression*](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118548387) by Hosmer et al. (2013), which presents a complete overview in logistic regression. Additionally, Chapter 14 from the book  [*Applied Linear Regression Models*](http://users.stat.ufl.edu/~winner/sta4211/ALSM_5Ed_Kutner.pdf) by Kutner et al. (2005), and Chapter 2 from the book [*Extending the Linear Model with R*](https://www.taylorfrancis.com/books/mono/10.1201/9781315382722/extending-linear-model-julian-faraway) by Faraway (2016) are also great resources on how to model binary response variables. 

## <a class=anchor id=logit_link></a> Logit link function

In the generalized linear models literature, the link function let us relate the linear predictor (the same as in a regression model) to the expected value of the response, and from basic probability, we have that the expected value of a binary response is equal to <img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y=1|X)">. In other words, we want to relate <img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y=1|X)"> and <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x}'\boldsymbol{\beta}">. 

For Bernoulli distributed responses, the canonical link function (and the most popular link function) is the logit link. That means that the logistic function (the inverse of the logit function) will map from <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x}'\boldsymbol{\beta}"> to <img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y=1|X)"> as

<img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y=1|X)=g^{-1}(\mathbf{x}'\boldsymbol{\beta})=\frac{e^{\mathbf{x}'\boldsymbol{\beta}}}{1\dotplus e^{\mathbf{x}'\boldsymbol{\beta}}},">

where <img src="https://render.githubusercontent.com/render/math?math=g()"> is the logit function. 

As mentioned earlier, the most popular link function is the logit link. However, other existing links in the literature are the Probit link, the extreme value link, the Cauchy link, and the complementary log-log link. For a broader discussion on canonical link functions (and their relation to GLMs and exponential families) see section 2.6 from the book [*Statistical Inference*](https://www.cambridge.org/core/journals/mathematical-gazette/article/abs/statistical-inference-2nd-edn-by-paul-h-garthwaite-ian-t-jolliffe-and-byron-jones-pp328-40-hbk-2002-isbn-0-19-857226-3-oxford-university-press/FB9EBD3320909B8F7F968615CD8463B2) by Garthwaite et al. (2009). For a discussion on the use of other link functions see section 14.2 from the book [*Applied Linear Regression Models*](http://users.stat.ufl.edu/~winner/sta4211/ALSM_5Ed_Kutner.pdf).

## <a class=anchor id=logit_estimation></a> Learning the model parameters

As in linear regression, our goal is to learn the parameter vector  <img src="https://render.githubusercontent.com/render/math?math=\boldsymbol{\beta}">. This can be done in a variety of ways, but the most popular learning algorithm is maximum likelihood. As expected, the idea is to choose the set of parameters that maximizes the likelihood function.

Nonetheless, there are other popular learning algorithms, including penalized likelihood. See for example, the work by Friedman et al. (2010) [Regularization Paths for Generalized Linear Models via Coordinate Descent](https://doi.org/10.18637/jss.v033.i01).

## <a class=anchor id=logit_residuals></a> The residuals

In logistic regression, as in other generalized linear models, we have two types of residuals. (1) The Pearson residuals, which are closer to the residuals discussed in linear regression; and (2) the deviance residuals, which are computed in a less intuitive way. For a broader discussion on these two type of residuals see Chapter 5 from the book [*Applied Logistic Regression*](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118548387).

## <a class=anchor id=logit_diagnostics></a> Model diagnostics

As in linear regression, for logistic regression the model diagnostics serve as a way to assess whether our fitted model captures the structure of the data. Some graphical diagnostic tools may include: (1) plot of the residuals (Pearson or deviance) against the fitted values; (2) plot of the observed values against the fitted values; or (3) the Cook's distance plot, among many others. Chapter 5 from the book [*Applied Logistic Regression*](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118548387), describes in detail how to assess the model fit on logistic regression, including summary measures of goodness of fit, model diagnostics and assessment of fit via external validation. Additionally sections 14.7 and 14.8 from the book  [*Applied Linear Regression Models*](http://users.stat.ufl.edu/~winner/sta4211/ALSM_5Ed_Kutner.pdf), and sections 10.4 and 10.5 from the book [*Statistical Inference*](https://www.cambridge.org/core/journals/mathematical-gazette/article/abs/statistical-inference-2nd-edn-by-paul-h-garthwaite-ian-t-jolliffe-and-byron-jones-pp328-40-hbk-2002-isbn-0-19-857226-3-oxford-university-press/FB9EBD3320909B8F7F968615CD8463B2), present also how to conduct model diagnostics and assess the goodness of fit in logistic regression models.

## <a class=anchor id=binom_reg></a> Binomial regression

A wider generalization of the logistic regression model for binary data is the binomial regression model with a logit link. Recall that if we have <img src="https://render.githubusercontent.com/render/math?math=n"> independent Bernoulli distributed random variables <img src="https://render.githubusercontent.com/render/math?math=Y_{1},\,Y_{2},\,\dots,\,Y_{n}"> with parameter <img src="https://render.githubusercontent.com/render/math?math=p">, then

<img src="https://render.githubusercontent.com/render/math?math=Y=\sum_{i=1}^{n}Y_{i}">

will have a <img src="https://render.githubusercontent.com/render/math?math=\text{Bin}(n,\,p)"> distribution. Moreover, note that if <img src="https://render.githubusercontent.com/render/math?math=n=1">, then <img src="https://render.githubusercontent.com/render/math?math=\text{Bin}(n,\,p)="><img src="https://render.githubusercontent.com/render/math?math=\text{Ber}(p)">. Thus, the binomial regression model is a generalization of the logistic regression model for binary data. However, in the binomial model the response variable is the sum of <img src="https://render.githubusercontent.com/render/math?math=n"> independent and identically distributed Bernoulli random variables, where the parameter <img src="https://render.githubusercontent.com/render/math?math=n"> is assumed to be known by the researcher. Again, as in logistic regression for binary data, we need to relate the mean of the binomial distribution to the the linear predictor. It turns out that the most natural way to do this its by using a logit link. As usual, we can also learn the model parameters <img src="https://render.githubusercontent.com/render/math?math=\boldsymbol{\beta}"> in the same way as before. By maximizing the log-binomial likelihood. 

## <a class=anchor id=logit_implementation></a> Implementation

Now, we are going to point out useful resources on how to implement logistic regression both in R and Stata.

### <a class=anchor id=logit_in_r></a> Implementation in R

Chapter 2 from the book [*Extending the Linear Model with R*](https://www.taylorfrancis.com/books/mono/10.1201/9781315382722/extending-linear-model-julian-faraway) presents in detail how to fit a logistic regression in R as well as how to perform model diagnostics.

### <a class=anchor id=logit_in_stata></a> Implementation in Stata

In order to implement logistic regression models in Stata, we can follow the guide [*Introduction to logistic regression with stata*](https://stats.idre.ucla.edu/stata/webbooks/logistic/chapter1/logistic-regression-with-statachapter-1-introduction-to-logistic-regression-with-stata/), developed by the IDRE from UCLA. 

## <a class=anchor id=logit_ref></a> References

+ Faraway, J. (2016). *Extending the Linear Model with R*. CRC Press.

+ Friedman, J. H., Hastie, T., Tibshirani, R. (2010). Regularization paths for generalized linear models via coordinate descent. *Journal of Statistical Software*. 33(1), 1–22.

+ Garthwaite, P., Joliffe, I., Jones, B. (2009). *Statistical Inference*. Oxford Science Publications.

+ Hosmer Jr, D.W., Lemeshow S., Sturdivant R.X. (2013). *Applied logistic regression*. John Wiley & Sons.

* Kutner, M.H., Nachtsheim, C.J., Neter, J., Li, W. (2004). *Applied Linear Regression Models*. McGraw-Hill Education.

* UCLA: Statistical Consulting Group. Logistic regression with stata chapter 1: introduction to logistic regression with stata. Retrieved from: https://stats.idre.ucla.edu/stata/webbooks/logistic/chapter1/logistic-regression-with-statachapter-1-introduction-to-logistic-regression-with-stata/.
