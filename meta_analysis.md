## Meta analysis

This fact sheet presents a discussion on meta analysis and its importance in applied statistics.

## Contents

- [Meta analysis](#meta)
- [Implementation](#meta_implementation)
    - [Implementation in R](#meta_in_r)
    - [Implementation in Stata](#meta_in_stata)
- [References](#meta_ref)

## <a class=anchor id=meta></a> Meta analysis

The gold standard for conducting a meta analysis is the protocol established by the [Cochrane Collaboration] (https://training.cochrane.org/handbook/current). Consider [pre-registering](https://www.crd.york.ac.uk/prospero/) your systematic review too. The protocol for reporting a meta analysis is called [PRISMA](http://prisma-statement.org/).

## <a class=anchor id=meta_implementation></a> Implementation

In this section we are going to present useful resources on how to implement meta analysis in R and Stata.

### <a class=anchor id=meta_in_r></a> Implementation in R

In R the picture is a bit muddy as there are several competing packages. Many researchers use the metafor package which is written up in a [tutorial paper](https://cran.r-project.org/web/packages/metafor/vignettes/metafor.pdf) and a [flowchart](https://cran.r-project.org/web/packages/metafor/vignettes/diagram.pdf). The Towards Data Science blog has a [post](https://towardsdatascience.com/introduction-to-meta-analysis-in-r-468e9b33925c) describing metafor too.

Other researchers use the meta package which is written up in a R-bloggers [post](https://www.r-bloggers.com/2021/08/meta-analysis-in-r/). 

There's even a [package](https://cran.r-project.org/web/packages/PRISMAstatement/vignettes/PRISMA.html) to generate the PRISMA flowchart! 

### <a class=anchor id=meta_in_stata></a> Implementation in Stata

For advice on how to tackle a meta analysis in Stata, try this [OARC tutorial](https://stats.oarc.ucla.edu/stata/seminars/introduction-to-meta-analysis-in-stata/).

## <a class=anchor id=meta_ref></a> References

* Hedges, L.V. and Olkin, I. (2014). *Statistical Methods for Meta-Analysis*. Academic Press.

* Borenstein, M., Hedges, L.V. Higgins, J.P.T. and Rothstein, H.R. (2009). *Introduction to Meta-Analysis*. Wiley.


