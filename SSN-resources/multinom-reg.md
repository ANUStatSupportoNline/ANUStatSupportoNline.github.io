# Multinomial regression

This fact sheet presents an introduction to multinomial logistic regression.

## Contents

- [Brief introduction to the Multinomial distribution](#what_is_Multinom)
- [Nominal vs. Ordinal data](#Ordi_vs_Nomi)
- [Multinomial logistic regression for nominal data](#Multi_nom_reg)
- [Ordinal response logistic regression](#Ordi_reg)
- [Implementation](#Multinom_implementation)
    - [Implementation in R](#Multinom_in_r)
    - [Implementation in Stata](#Multinom_in_stata)
- [References](#Multinom_ref)

## <a class=anchor id=what_is_Multinom></a> Brief introduction to the Multinomial distribution

Before presenting the Multinomial regression models for nominal data, we are going to present firstly, a brief introduction to the Multinomial distribution. 

Let us assume that there are in total <img src="https://render.githubusercontent.com/render/math?math=C"> different categories/classes, and we want to model the probability that category <img src="https://render.githubusercontent.com/render/math?math=c"> happens, where <img src="https://render.githubusercontent.com/render/math?math=c\in\{1,\dots,\,C\}">. Note that if <img src="https://render.githubusercontent.com/render/math?math=C=2">, we will have a traditional logistic regression for binary data, so the Multinomial regression model is said to be a generalization of the logistic regression model for binary data.

## <a class=anchor id=Ordi_vs_Nomi></a> Nominal vs. Ordinal data

As discussed earlier, the Multinomial distribution is used when we want to model the probability that a certain category <img src="https://render.githubusercontent.com/render/math?math=c"> happens, where <img src="https://render.githubusercontent.com/render/math?math=c\in\{1,\dots,\,C\}"> and <img src="https://render.githubusercontent.com/render/math?math=C>2">. However, we first need to distinguish between two types of data. Nominal data and ordinal data. In nominal data, there is not a natural way to order the <img src="https://render.githubusercontent.com/render/math?math=C"> categories, for e.g., <img src="https://render.githubusercontent.com/render/math?math=c\in\left\{\text{Blue, Yellow, Red}\right\}">, or <img src="https://render.githubusercontent.com/render/math?math=c\in\left\{\text{Dog, Cat, Bird}\right\}">. On the other hand, in ordinal data there is a natural way to order the categories, and such ordering will affect the analysis, for e.g., <img src="https://render.githubusercontent.com/render/math?math=c\in\left\{\text{Strongly agree, Agree, Neutral, Disagree, Strongly disagree}\right\}">, or  <img src="https://render.githubusercontent.com/render/math?math=c\in\left\{\text{1st place, 2nd place, 3rd place}\right\}">.

Formally speaking, Multinomial regression models are designed to analyze nominal data, where the order of the categories does not matter. We could use a multinomial model to fit ordinal data, but we would loose a lot of valuable information. However, later in the fact sheet we will also discuss how to fit ordinal data, without loosing information. 

## <a class=anchor id=Multi_nom_reg></a> Multinomial logistic regression for nominal data

We are now going to present Multinomial logistic regression. More formally, in multinomial regression the response variable <img src="https://render.githubusercontent.com/render/math?math=Y_{i}"> represents to which category observation <img src="https://render.githubusercontent.com/render/math?math=i"> belongs to. For example <img src="https://render.githubusercontent.com/render/math?math=Y_{i}"> = `cat` or <img src="https://render.githubusercontent.com/render/math?math=Y_{i}"> = `blue`. 

The goal is to model the probability that category <img src="https://render.githubusercontent.com/render/math?math=c"> happens, namely, <img src="https://render.githubusercontent.com/render/math?math=\mathbb{P}(Y = c) = \pi_{c}">, given a set of covariates <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x}\in\mathbb{R}^{p}">. So far, it looks very similar to logistic regression, and in fact, they are very similar. The only difference is that in Multinomial logistic regression <img src="https://render.githubusercontent.com/render/math?math=C>2">. Following the literature on Multinomial regression, we are going to set one of the <img src="https://render.githubusercontent.com/render/math?math=c"> categories as a baseline category. For example, let us consider <img src="https://render.githubusercontent.com/render/math?math=c=1"> as the baseline category. The idea is to compare the probability of each one of the other <img src="https://render.githubusercontent.com/render/math?math=C-1"> categories, against the probability of the baseline category. More precisely, we want to model

<img src="https://render.githubusercontent.com/render/math?math=\frac{\pi_{c}}{\pi_{1}} = \exp{\left\{\mathbf{x}'\boldsymbol{\beta}_{c} \right\}},">

for <img src="https://render.githubusercontent.com/render/math?math=c=2,\dots,C">, because <img src="https://render.githubusercontent.com/render/math?math=c=1"> is our baseline. Our goal is to learn the <img src="https://render.githubusercontent.com/render/math?math=C-1"> parameter vectors <img src="https://render.githubusercontent.com/render/math?math=\boldsymbol{\beta}_{c}">, for each one of the <img src="https://render.githubusercontent.com/render/math?math=C-1"> categories. This can be done via maximum likelihood estimation. 

## <a class=anchor id=Ordi_reg></a> Ordinal response logistic regression

As in the nominal response case, in the ordinal response case the response variable <img src="https://render.githubusercontent.com/render/math?math=Y_{i}"> represents to which category observation <img src="https://render.githubusercontent.com/render/math?math=i"> belongs to. The difference is now that the order of the categories matter. For example <img src="https://render.githubusercontent.com/render/math?math=Y_{i}"> = `Agree` or <img src="https://render.githubusercontent.com/render/math?math=Y_{i}"> = `1st place`. 

Additionally, in ordinal response regression it is assumed that the <img src="https://render.githubusercontent.com/render/math?math=C"> categories are ordered such that 

<img src="https://render.githubusercontent.com/render/math?math=\text{category 1} < \text{category 2} < \dots < \text{category C}.">

Given this ordering, it is convenient to work with cumulative probabilities. In other words, we want to model the odds that <img src="https://render.githubusercontent.com/render/math?math=Y<c">. this is 

<img src="https://render.githubusercontent.com/render/math?math=\frac{\mathbb{P}(Y\leq c)}{1-\mathbb{P}(Y\leq c)} = \frac{\mathbb{P}(Y \leq c)}{\mathbb{P}(Y\geq c\dotplus1)} = \frac{\sum_{j=1}^{c}\pi_{j}}{\sum_{j=c\dotplus1}^{C}\pi_{j}}\exp\left\{\mathbf{x}'\boldsymbol{\beta}_{c}\right\},">

for <img src="https://render.githubusercontent.com/render/math?math=c=1,\dots,\,C-1">. This is because the probability of <img src="https://render.githubusercontent.com/render/math?math=Y<C"> is always one. 

Again, we can learn the parameter vectors <img src="https://render.githubusercontent.com/render/math?math=\boldsymbol{\beta}_{c}"> using maximum likelihood estimation. 

## <a class=anchor id=Multinom_implementation></a> Implementation

Now, we are going to point out useful resources on how to implement nominal response regression and ordinal response regression using R and Stata.

### <a class=anchor id=Multinom_in_r></a> Implementation in R

Chapter 5 from the book [*Extending the Linear Model with R*](https://www.taylorfrancis.com/books/mono/10.1201/9781315382722/extending-linear-model-julian-faraway) presents in detail how to fit both nominal response regression and ordinal response regression models in R. 

### <a class=anchor id=Multinom_in_stata></a> Implementation in Stata

In order to implement multinomial regression and ordered logistic regression models in Stata, we can follow the guides <a href="https://stats.oarc.ucla.edu/stata/dae/multinomiallogistic-regression/">Multinomial logistic regression | STATA data analysis examples</a> and <a href="https://stats.oarc.ucla.edu/stata/dae/ordered-logistic-regression/">Ordered logistic regression | STATA data analysis examples</a>, respectively. Both guides were developed by the IDRE from UCLA. 

## <a class=anchor id=Multinom_ref></a> References

+ Faraway, J. (2016). *Extending the Linear Model with R*. CRC Press.

* UCLA: Statistical Consulting Group. Multinomial logistic regression - STATA data analysis examples. Retrieved from: https://stats.oarc.ucla.edu/stata/dae/multinomiallogistic-regression/.

* UCLA: Statistical Consulting Group. Ordered logistic regression - STATA data analysis examples. Retrieved from: https://stats.oarc.ucla.edu/stata/dae/ordered-logistic-regression/.


<span>&#127968;</span> <a href="https://anustatsupportonline.github.io/">Return to homepage</a> <span>&nbsp;</span> 
<span>&#128187;</span> <a href="https://anustatsupportonline.github.io/SSN-resources">Return to SSN Resources page</a>
