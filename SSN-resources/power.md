# Power of a test

This fact sheet presents a discussion on what is the statistical power of a hypothesis test

## Contents

- [Brief introduction to hypothesis testing](#Power_hyp)
- [Significance vs. Power](#sig_vs_pow)
- [Determinants of the power](#det_pow)
- [Rules of thumb](#pow_rules_thum)
- [References](#pow_ref)

## <a class=anchor id=Power_hyp></a> Brief introduction to hypothesis testing

Let us assume that we want to test whether or not some statement or proposed theory is true (or at least plausible) given the observed data. Usually, we do this via binary hypothesis testing, where we have a null hypothesis ($H_{0}$) and a competing alternative hypothesis ($H_{a}$), and our decision derived from the test could be correct or incorrect. 

If we reject $H_{0}$ when in fact $H_{0}$ is false, or if we do not reject $H_{0}$ when $H_{0}$ is true, then we say that our decision is correct. Otherwise, we say that our decision is incorrect. Note, however, that our decision could be incorrect under two scenarios, namely type I and type II errors.

* Type I error: Reject $H_{0}$ given that $H_{0}$ is true
* Type II error: Not reject $H_{0}$ given that $H_{0}$ is false. 

As researchers, we would like to minimize the chances of incurring in type I or type II errors. 

## <a class=anchor id=sig_vs_pow></a> Significance vs. Power

The significance, denoted by $\alpha$, is the probability of incurring in a type I error. In other words, $\alpha$ is the following conditional probability:

$$\alpha=\mathbb{P}(\text{Type I error}) = \mathbb{P}(\text{Reject }H_{0}\,|\,H_{0}\text{ is true}).$$

On the other hand, let us define $\beta$ as the probability of incurring in a type II error, this is, 

$$ \beta=\mathbb{P}(\text{Type II error}) = \mathbb{P}(\text{Not reject }H_{0}\,|\,H_{0}\text{ is false}), $$

so $1-\beta$ is the power of the test, denoted by $\eta$, i.e.,

$$ \eta = 1-\beta = \mathbb{P}(\text{Reject }H_{0}\,|\,H_{0}\text{ is false}).$$

It is common for us to set the significance level as a fixed quantity (usually 0.05), but we need to take into account that there is a strong inverse relationship between $\alpha$ and $\beta$. Therefore, if we reduce $\alpha$ inevitably we will also increase $\beta$. In other words, if we set $\alpha$ as very small number (which may seem like a good thing), will end up with a much smaller power (which is not a very good thing). 

Our task, then, is to obtain a large power (i.e., minimize the type II error), while at the same time having a small type I error. 

## <a class=anchor id=det_pow></a> Determinants of the power

After discussing the relationship between $\alpha$ and $\eta$, we are now going to discuss some of the determinants of the power. Note, however, that the determinants of the power may vary between specific research questions and methodologies. That being said, the usual components that affect the power are the significance level $\alpha$, the effect size, and the sample size. As discussed earlier, the significance level is the probability of incurring in a type I error, and it is usually set as a fixed quantity by the researcher. Now, let us discuss the other components. 

* Effect size: This is roughly described as the expected mean difference relative to the "noise" or standard deviation within each sample. If the effect size is large enough, the power will also be large because, the probability of a type II error will be small.

* Sample size: This determines the amount of "noise" in our sample. More precisely, the larger the sample size, the smaller the "noise" in the data.Therefore, from the above bullet point, we have that a larger sample size will result in a larger effect size and therefore, in a larger power. 

Thus, note that if we want to increase our power while leaving our significance level fixed, we should increase our sample size. More formally, we should select our sample size such that we attain a minimum desired power (usually 80%). 

This can easily be done using the R package [$\texttt{pwr}$](https://cran.r-project.org/web/packages/pwr/), where we have power calculations for $t$-tests, $F$-test, $\chi^{2}$-tests, $z$-tests, among many others.

## <a class=anchor id=pow_rules_thum></a> Rules of thumb

Solving for the sample size that gives a minimum power can be non straightforward. Nonetheless, there are some rules of thumb in the literature.

For example, in regression settings, Stevens (1996), suggest that we should have around 15 observations per predictor.  Other rules of thumb for more specific cases can be found in Van Belle (2011).

## <a class=anchor id=pow_ref></a> References

* Stevens, J. (1996). Applied multivariate statistics for the social sciences. Lawrence Erlbaum Associates, Publishers.

* Van Belle, G. (2011). Statistical rules of thumb. John Wiley & Sons.

<span>&#127968;</span> <a href="https://anustatsupportonline.github.io/">Return to homepage</a> <span>&nbsp;</span> 
<span>&#128187;</span> <a href="https://anustatsupportonline.github.io/SSN-resources">Return to SSN Resources page</a>
