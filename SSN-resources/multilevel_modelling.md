## Multilevel Modelling

This fact sheet presents a discussion on multilevel modelling and its importance in applied statistics.

## Contents

- [Hierarchical Data](#hier_data)
- [Pooled and un-pooled estimators](#unpool_vs_pool)
- [A partial pooled approach](#par_pool)
- [Maximum Likelihood estimation](#MLE_multilevel)
- [Implementation](#multilevel_implementation)
    - [Implementation in R](#multilevel_in_r)
    - [Implementation in Stata](#multilevel_in_stata)
- [References](#multilevel_ref)

## <a class=anchor id=hier_data></a> Hierarchical Data

So far, we have talked about a random sample from a population. For example, we may be interested in analysing if the socio-economical status of a student affects its academic performance. To that end, we may randomly select a group of students from a given school and perform a simple linear regression analysis, where the response variable is the academic performance, and the explanatory variable is a measure of the socio-economic status of each student. 

Note, however, that we may also have data from multiple students nested within schools, and from multiple schools nested within geographic districts, and so on. This type of data are often called hierarchical or multilevel data. The main feature of such type of data is that observations within a group tend to be more similar to each other than observations across groups. In our previous example, it is reasonable to expect that students within the same school are more similar than students from different schools, or we can also expect that schools within the same district are more similar than schools from different districts. However, there are still some similarities between all the students regardless of their school or district. Thus, we want to capture group-specific features for each observation, while capturing commonalities among all the observations. 

## <a class=anchor id=unpool_vs_pool></a> Pooled and un-pooled approaches

We are now going to discuss two $\text{n\"{a}ive}$ approaches to model our multilevel data. But first, let us intriduce some notations. Let us consider a two-level hierarchical data set, where we have in total $J$ schools and within each school we have $n_{j}$ students. Let $y_{i,j}$ and $x_{i,j}$ be a measure of the academic performance and the socio-economical level, respectively, of student $i$ in school $j$, for $i=1,\dots,n_{j}$ and $j=1,\dots,J$. 

The first approach is to consider the model

$$\boldsymbol{y}_{j} = \alpha_{j} + \beta_{j}\boldsymbol{x}_{j} + \boldsymbol{\varepsilon}_{j},$$

where $\boldsymbol{y}_{j} = \left(y_{1,j},\dots,y_{n_{j},j}\right)'$, $\boldsymbol{x}_{j} = \left(x_{1,j},\dots,x_{n_{j},j}\right)'$, and $\boldsymbol{\varepsilon}_{j} = \left(\varepsilon_{1,j},\dots,\varepsilon_{n_{j},j}\right)'\sim\mathcal{N}(\mathbf{0},\, \sigma_j^{2}\mathbf{I})\,$, for $j=1,\dots,J$. Here we are modelling each one of the $J$ schools separately, and our goal is to estimate each one of the $J$ parameter vectors $(\alpha_{j},\,\beta_{j},\,\sigma^{2}_j)'$. This approach is known in the literature as an un-pooled aproach.

In the second approach we want to model

$$\boldsymbol{y} = \alpha + \beta\boldsymbol{x} + \boldsymbol{\varepsilon},$$

where $\boldsymbol{y} = \left(\boldsymbol{y}_{1}',\dots,\boldsymbol{y}_{J}'\right)'$, $\boldsymbol{x} = \left(\boldsymbol{x}_{1}',\dots,\boldsymbol{x}_{J}'\right)'$, and $\boldsymbol{\varepsilon} = \left(\boldsymbol{\varepsilon}_{1}',\dots,\boldsymbol{\varepsilon}_{J}'\right)'\sim\mathcal{N}(\mathbf{0},\,\sigma^2\mathbf{I})$. Here we are pooling the data from all the schools into one "big" data-set, and our goal is to estimate the parameter vector $(\alpha,\, \beta)'$. This approach is known as a pooled approach. 

However, neither of these two approaches are completely satisfactory. In the pooled approach we are assuming a unique data generating process for all the schools, which is a strong assumption. On the other hand, in the un-pooled approach we are assuming that there is no information that we
can learn from other schools, which is not true, because even if the schools are different. there are some similarities between them, and capturing those similarities will lead to a more robust analysis.

Thus, it is clear that we need something in-between. A partial pooled approach will do exactly this!

## <a class=anchor id=par_pool></a> A partial pooled approach

Let's consider the following hierarchical regression model

$$ y_{i,j} = \boldsymbol{\beta}'_{j}x_{i,j} + \varepsilon_{i,j},$$

As in a traditional regression setting, we have that $\{\varepsilon_{1,1},\dots,\,\varepsilon_{1,n_1}\}, \dots,\, \{\varepsilon_{J,1},\dots,\,\varepsilon_{J,n_J}\}\sim \text{  i.i.d  }\, \mathcal{N}(0,\, \sigma^2)$, where the vector $\boldsymbol{\beta}_j$ are school specific parameters. Therefore, the joint distribution for the observed data (the likelihood) for school $j$ would be

$$ \boldsymbol{y}_j|\boldsymbol{\beta}_j \sim \mathcal{N}(\mathbf{X}_j\boldsymbol{\beta}_j,\, \sigma^2\mathbf{I}). $$

So far, it looks very similar to an un-pooled approach. We now need to model the similarities between the schools. To that end, let us assume a sampling distribution (a likelihood) for the coefficients $\{\boldsymbol{\beta}_{1},\dots,\,\boldsymbol{\beta}_{J}\}$ as 

$$ \{\boldsymbol{\beta}_{1},\dots,\,\boldsymbol{\beta}_{J}\} \sim \text{ i.i.d. }\, \mathcal{N}(\boldsymbol{\beta},\, \boldsymbol{\Psi}),$$

where $\boldsymbol{\beta}$ is a regression vector that is common across the $J$ schools, and $\boldsymbol{\Psi}$ is a covariance matrix that describe the variability of $\boldsymbol{\beta}_{j}$ around $\boldsymbol{\beta}$. Thus, we are capturing group-specific features for each observation, while capturing commonalities among all the groups. 

## <a class=anchor id=MLE_multilevel></a> Maximum Likelihood estimation

Now, we are now going to discuss how to learn all the parameters from the above multilevel model. Long story short, we can use maximum likelihood estimation!

It can be shown that the complete log-likelihood function for the above multilevel model is 

$$ l(\boldsymbol{\theta}) = \sum_{j} \log\{\texttt{dmvnorm}(\boldsymbol{y}_j,\, \mathbf{X}_j\boldsymbol{\beta},\, \mathbf{X}_j\boldsymbol{\Psi}\mathbf{X}_j + \sigma^2\mathbf{I} )  \},$$

where $\theta$ is the set of all the parameters in the model, and, as expected, the maximum likelihood estimator for $\boldsymbol{\theta}$ is given by $\text{arg min}_{\boldsymbol{\{\theta}\}}\,-l(\boldsymbol{\theta})$. 

## <a class=anchor id=multilevel_implementation></a> Implementation

In this section we are going to present useful resources on how to implement multilevel modelling in R and Stata.

### <a class=anchor id=multilevel_in_r></a> Implementation in R

There's a tutorial on the lmer() function from an ecology point of view in Andrew Robinson's [icebreakeR](https://cran.r-project.org/doc/contrib/Robinson-icebreaker.pdf). Bodo Winter writes a popular [tutorial](http://www.bodowinter.com/tutorial/bw_LME_tutorial.pdf) on lmer() from a social science point of view.

Strangely the OARC (was IDRE) at UCLA only provide a data analysis example for [multilevel logistic regression](https://stats.oarc.ucla.edu/r/dae/mixed-effects-logistic-regression/).

### <a class=anchor id=multilevel_in_stata></a> Implementation in Stata

Strangely the OARC (was IDRE) at UCLA only provide a data analysis example for [multilevel logistic regression](https://stats.oarc.ucla.edu/stata/dae/mixed-effects-logistic-regression/).

## <a class=anchor id=multilevel_ref></a> References

* Faraway, J.J. (2006). *Extending the Linear Model with R*, 1st edition. CRC Press.

* Gelman, A. and Hill, J. (2007). *Data Analysis using Regression and Multilevel/Hierarchical Models*. Cambridge University Press.

* Pinheiro, J.C. and Bates, D.M. (2000). *Mixed-Effects Models in S and S-Plus*. Springer.

