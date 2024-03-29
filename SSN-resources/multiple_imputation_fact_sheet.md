---
output:
  html_document: default
  pdf_document: default
---
## Multiple imputation

In this fact sheet, we are going to discuss what is multiple imputation and its importance in applied statistics.

## Contents

- [What is multiple imputation?](#what_is_MI)
- [Simple vs. Multiple imputation](#SI_vs_MI)
- [Analysis of multiply imputed data sets](#Analysis)
- [Implementation](#MI_implementation)
    - [Implementation in R](#MI_in_r)
    - [Implementation in Stata](#MI_in_stata)
- [References](#MI_ref)

## <a class=anchor id=what_is_MI></a> What is multiple imputation?

Multiple imputation (MI) has recently become an extremely popular approach when missing data. One big reason for this is that once missing values have been imputed and imputed datasets have been generated, these can be easily analysed using standard statistical analysis, followed by pooling the estimates using Rubin's rules. Additionally, MI is now incorporated in several widely used statistical software packages, so that imputation has now become an easily implemented solution for missing data. Multiple imputation can be very useful to handle missing values if done correctly, however it can be equally misleading if performed incorrectly.

The seminal books on multiple imputation are [*Multiple Imputation for nonresponse in surveys*](hard copy in ANU library) by Rubin (1987), and [*Statistical analysis with missing data*](electronic copy in ANU library) by Little and Rubin (2002). 

A general article on [Multiple imputation in epidemiological and clinical  research](https://www.bmj.com/content/338/bmj.b2393) has been published in the British Medical Journal.

If you're involved in randomised clinical trials, a paper on [When and how should multiple imputation be used](https://bmcmedresmethodol.biomedcentral.com/articles/10.1186/s12874-017-0442-1) appeared in BMC Medical Research Methodology.

There are a number of things to bear in mind when considering multiple imputation. These include the mechanism of missingness, structure of the imputation model, selecting predictors for the imputation model, imputing derived variables, the number of imputations and the method of imputation. Have a look at our [blog post](https://statscome2you.weblogs.anu.edu.au/2020/07/29/six-things-to-bear-in-mind-when-performing-multiple-imputation/) for more detail on each of these. 

## <a class=anchor id=SI_vs_MI></a> Simple vs. Multiple imputation

A variety of methods of single imputation were developed when computing power was lower than it is today e.g. replacing missing values with their mean or median. Last Observation Carried Forward has been popular in medical research but is not ideal: see the article on [LOCF](https://methods.sagepub.com/reference/encyc-of-research-design/n211.xml) in the Sage Encyclopedia of Research Design.

## <a class=anchor id=Analysis></a> Analysis of multiply imputed datasets

Analysis of multiply imputed datasets generally proceeds exactly as for complete datasets, and the results are pooled using Rubin's rules to provide you with a single set of results. However, stepwise model selection after multiple imputation is frowned on: see [Heymans et al.](https://link.springer.com/article/10.1186/1471-2288-7-33) for a bootstrap alternative or [Sabbe et al.](https://onlinelibrary.wiley.com/doi/abs/10.1002/sim.5760) for a LASSO alternative.

## <a class=anchor id=MI_implementation></a> Implementation

In this section, we are going to present useful resources on how to implement multiple imputation in R and Stata.

### <a class=anchor id=MI_in_r></a> Implementation in R

CRAN maintains a [task view on multiple imputation](https://cran.r-project.org/web/views/MissingData.html) which lists all the options. Our preference is for the packages [mice](https://amices.org/mice/) and [mi](https://cran.r-project.org/web/packages/mi/vignettes/mi_vignette.pdf).

### <a class=anchor id=MI_in_stata></a> Implementation in Stata

In order to implement multiple imputation in Stata, we can follow the guide called [Multiple imputation in Stata](https://stats.oarc.ucla.edu/stata/seminars/mi_in_stata_pt1_new/), developed by the IDRE from UCLA. 

## <a class=anchor id=MI_ref></a> References

* van Buuren, S. (2012). *Flexible Imputation of Missing Data*, 2nd edition. CRC Press.

* Little, R.J.A. and Rubin, D.B. (2002). *Statistical Analysis with Missing Data*, 2nd edition. Wiley. 

* Rubin, D.B. (1987). *Multiple Imputation for Nonresponse in Surveys*. Wiley.


