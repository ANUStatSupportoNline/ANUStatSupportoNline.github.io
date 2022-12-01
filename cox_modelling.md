## Cox Modelling

This fact sheet presents a discussion on Cox modelling (also known as survival analysis) and its importance in applied statistics.

## Contents

- [Cox models](#cox_models)
- [Maximum Likelihood estimation](#MLE_cox)
- [Implementation](#cox_implementation)
    - [Implementation in R](#cox_in_r)
    - [Implementation in Stata](#cox_in_stata)
- [References](#cox_ref)

## <a class=anchor id=cox_models></a> Cox models

There's a nice 8 page pdf [introduction](http://www.bandolier.org.uk/painres/download/whatis/COX_MODEL.pdf) to Cox models from Bandolier.

## <a class=anchor id=MLE_cox></a> Maximum Likelihood estimation

Under construction. 

## <a class=anchor id=cox_implementation></a> Implementation

In this section we are going to present useful resources on how to implement Cox modelling in R and Stata.

### <a class=anchor id=cox_in_r></a> Implementation in R

The most commonly used R function is coxph() in the survival library. [R bloggers](https://www.r-bloggers.com/2016/12/cox-proportional-hazards-model/) has a post about it, and so does [STHDA](https://sthda.com/english/wiki/cox-proportional-hazards-model). [IDRE](https://stats.oarc.ucla.edu/r/dae/mixed-effects-cox-regression/) at UCLA do too but it moves fairly quickly to a multilevel data example. There's a [seminar]https://stats.oarc.ucla.edu/r/seminars/introduction-to-survival-analysis-in-r/) that covers the basics.

### <a class=anchor id=cox_in_stata></a> Implementation in Stata

[IDRE](https://stats.oarc.ucla.edu/stata/seminars/stata-survival/) at UCLA offer a seminar on survival analysis with Stata. 

## <a class=anchor id=cox_ref></a> References

* Therneau, T.M. and Grambsch, P.M. (2013). *Modelling Survival Data: Extending the Cox Model*. Springer. 

