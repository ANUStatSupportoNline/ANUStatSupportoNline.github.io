# Power of a test

This fact sheet presents a discussion on what is the statistical power of a hypothesis test

## Contents

- [Brief introduction to hypothesis testing](#Power_hyp)
- [Significance vs. Power](#sig_vs_pow)
- [Determinants of the power](#det_pow)
- [Rules of thumb](#pow_rules_thum)
- [References](#pow_ref)

<div style="text-align: center;">
  <img src="/assets/images/power.png" alt="power"
             width = "450" 
             height = "450">
</div>


## <a class=anchor id=Power_hyp></a> Brief introduction to hypothesis testing

Let us assume that we want to test whether or not some statement or proposed theory is true (or at least plausible) given the observed data. Usually, we do this via binary hypothesis testing, where we have a null hypothesis (<img src="https://render.githubusercontent.com/render/math?math=H_{0}">) and a competing alternative hypothesis (<img src="https://render.githubusercontent.com/render/math?math=H_{a}">). Note that our decision derived from the test could be correct or incorrect. 

If we reject <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> when in fact <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> is false, or if we do not reject <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> when <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> is true, then we say that our decision is correct. Otherwise, we say that our decision is incorrect. Note, however, that our decision could be incorrect under two scenarios, namely type I and type II errors.

* Type I error: Reject <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> given that <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> is true
* Type II error: Not reject <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> given that <img src="https://render.githubusercontent.com/render/math?math=H_{0}"> is false. 

As researchers, we would like to minimize the chances of incurring in type I or type II errors. 

## <a class=anchor id=sig_vs_pow></a> Significance vs. Power

The significance, denoted by <img src="https://render.githubusercontent.com/render/math?math=\alpha">, is the probability of incurring in a type I error. In other words, <img src="https://render.githubusercontent.com/render/math?math=\alpha"> is the following conditional probability:

<img src="https://render.githubusercontent.com/render/math?math=\alpha=\mathbb{P}(\text{Type I error}) = \mathbb{P}(\text{Reject}\,\,H_{0}\,|\,H_{0}\,\,\text{is true}).">

On the other hand, let us define  <img src="https://render.githubusercontent.com/render/math?math=\beta"> as the probability of incurring in a type II error, this is, 

 <img src="https://render.githubusercontent.com/render/math?math=\beta=\mathbb{P}(\text{Type II error}) = \mathbb{P}(\text{Not reject}\,\,H_{0}\,|\,H_{0}\,\,\text{is false}),">

so <img src="https://render.githubusercontent.com/render/math?math=1-\beta"> is the power of the test, denoted by <img src="https://render.githubusercontent.com/render/math?math=\eta">, i.e.,

<img src="https://render.githubusercontent.com/render/math?math=\eta = 1-\beta = \mathbb{P}(\text{Reject}\,\,H_{0}\,|\,H_{0}\,\,\text{is false}).">

It is common for us to set the significance level (<img src="https://render.githubusercontent.com/render/math?math=\alpha">) as a fixed quantity (usually 0.05), but we need to take into account that there is a strong inverse relationship between <img src="https://render.githubusercontent.com/render/math?math=\alpha"> and <img src="https://render.githubusercontent.com/render/math?math=\beta">. Therefore, if we reduce <img src="https://render.githubusercontent.com/render/math?math=\alpha"> inevitably we will also increase <img src="https://render.githubusercontent.com/render/math?math=\beta">. In other words, if we set <img src="https://render.githubusercontent.com/render/math?math=\alpha"> as very small number (which may seem like a good thing), will end up with a much smaller power (which is not a very good thing). 

Our task, then, is to obtain a large power (i.e., minimize the type II error), while at the same time having a small type I error. 

## <a class=anchor id=det_pow></a> Determinants of the power

After discussing the relationship between <img src="https://render.githubusercontent.com/render/math?math=\alpha"> and <img src="https://render.githubusercontent.com/render/math?math=\eta">, we are now going to discuss some of the determinants of the power. Note, however, that the determinants of the power may vary between specific research questions and methodologies. That being said, the usual components that affect the power are the significance level <img src="https://render.githubusercontent.com/render/math?math=\alpha">, the effect size, and the sample size. As discussed earlier, the significance level is the probability of incurring in a type I error, and it is usually set as a fixed quantity by the researcher. Now, let us discuss the other components. 

* Effect size: This is roughly described as the expected mean difference relative to the "noise" or standard deviation within each sample. If the effect size is large enough, the power will also be large because, the probability of a type II error will be small.

* Sample size: This determines the amount of "noise" in our sample. More precisely, the larger the sample size, the smaller the "noise" in the data.Therefore, from the above bullet point, we have that a larger sample size will result in a larger effect size and therefore, in a larger power. 

Thus, note that if we want to increase our power while leaving our significance level fixed, we should increase our sample size. More formally, we should select our sample size such that we attain a minimum desired power (usually 80%). 

This can easily be done using the R package [`pwr`](https://cran.r-project.org/web/packages/pwr/), where we have power calculations for <img src="https://render.githubusercontent.com/render/math?math=t">-tests, <img src="https://render.githubusercontent.com/render/math?math=F">-test, <img src="https://render.githubusercontent.com/render/math?math=\chi^{2}">-tests, <img src="https://render.githubusercontent.com/render/math?math=z">-tests, among many others.

## <a class=anchor id=pow_rules_thum></a> Rules of thumb

Solving for the sample size that gives a minimum power can be non straightforward. Nonetheless, there are some rules of thumb in the literature.

For example, in regression settings, Stevens (1996), suggest that we should have around 15 observations per predictor.  Other rules of thumb for more specific cases can be found in Van Belle (2011).

## <a class=anchor id=pow_ref></a> References

+ Champely, S., et al. (2020). ***pwr***: Basic Functions for Power Analysis. R package version 1.3. URL https://cran.r-project.org/web/packages/pwr/.

* Stevens, J. (1996). Applied multivariate statistics for the social sciences. Lawrence Erlbaum Associates, Publishers.

* Van Belle, G. (2011). Statistical rules of thumb. John Wiley & Sons.



<span>&#127968;</span> <a href="https://anustatsupportonline.github.io/">Return to homepage</a> <span>&nbsp;</span> 
<span>&#128187;</span> <a href="https://anustatsupportonline.github.io/SSN-resources">Return to SSN Resources page</a>
