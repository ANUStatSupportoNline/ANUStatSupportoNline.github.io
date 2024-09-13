My local café updates its menu from time to time and it’s always nice to find a new dish, with the promise of fabulous new flavours behind the name of the dish. It’s the same with statistical software – and when I found the Stats iQ button allowing me to try Describe, Relate and even Regression, I was excited to try it out. Here’s what I found.

The Describe function produces bar charts of the responses to individual variables. This is a very standard analysis and a great place to start the exploration of your survey responses.

The Relate function produces a two-way table of two categorical variables along with a chi-square test of the independence of the row and column variables.

This is also a very standard analysis, appropriate for answering a range of valuable research questions.

However, the Regression function is where things have the potential to go off the rails. I managed to produce output from a logistic regression when the response variable had three categories. This should not happen, at least not under the usual use of the term “logistic regression”. Qualtrics had chosen a focus category for me, and also did not alert me to the fact that one variable had very little data in one category, which could have led to unstable estimates.

But there’s more! Qualtrics also offers a sample size calculator [https://www.qualtrics.com/blog/calculating-sample-size/]. Input your confidence level, population size and margin of error and out pops a sample size! 

First thing. The population size is not strictly needed in order to calculate a sample size that meets the required criteria. It matters more if the population size is small, or small relative to the likely sample size. Then a finite population correction does come into play, but there’s no mention of that in the site.

Second thing. “The confidence interval is the plus-or-minus figure that represents the accuracy of the reported.” Well, most first year stats textbooks define the margin of error as the plus-or-minus figure, and the confidence interval as the resulting pair of numbers. So that’s a bit confusing. “Confidence interval is also called the margin of error.” Well, not exactly … but let’s proceed.

Third thing. “Standard deviation. This refers to how much individual responses will vary between each other and the mean. If there's a low standard deviation, scores will be clustered near the mean with minimal variation. A higher standard deviation means that when plotted on a graph, responses will be more spread out. Standard deviation is expressed as a decimal, and 0.5 is considered a "good" standard deviation to set to ensure a sample size that represents the population.”

Agree with everything up to “spread out”. The kind of graph is not specified but a histogram is perhaps implied. Not necessarily though. Standard deviation is indeed expressed as a decimal but it is a number that can be anywhere between 0 and infinity! The authors have got themselves tangled up between continuous data (like the dollar amount mentioned in their example) and categorical data (like the binary yes/no data also in their example). For binary data, p = 0.5 is not good, it is in a sense the ‘worst case” in terms of variability in a proportion from sample to sample. The relevant formula is p(1 – p), not just p on its own.

And then for the brave, the formula behind their online calculator is revealed.

<div style="text-align: center;">
  <img src="/assets/images/Qualtrics sample size formula.png" alt="Lin_reg">
</div>
 
Z is defined in the usual way, and would be 1.96 for a 95% confidence interval.

Margin of error is selected from between 1% and 10% in the calculator, which encompasses the usual 3% margin of error for political polls, for instance.

StdDev appears to be set at 0.5. The weird thing is that no mention is made here of the need for a finite population correction, even though it is explicitly allowed for in the online calculator. Why?

So many assumptions. This calculator works for exactly one sample size calculation scenario, estimation of a population proportion for a binary response variable. Nothing else. It’s on a par with Slovin’s formula, which has gained some currency as an “approximate” sample size formula but it is almost never said that Slovin’s rule only applies to that single scenario too. 

The Qualtrics formula doesn’t work for a mean, or for calculating power of a statistical test, or for comparing two proportions, or two means, or more means, or for more complex designs or more complex parameters. Please seek statistical advice if any of these other scenarios apply to you. Indeed, please seek statistical advice in the scenario discussed here is the one that applies to you – there may be other structure lurking in your research question or data collection that leads to more nuanced calculations than the one provided for by Qualtrics.

It’s just like the advice statisticians have been handing out for years around the use of Excel for statistical analysis. Excel is a great product for data management and simple summaries of data. It’s flexible and widely available. However, its menu for data analysis does not promote statistical thinking i.e. thinking carefully about explanatory variables, responses and models for the variability in your data. Few consultant statisticians would recommend Excel as the sole tool for research data analysis. And so it is for Qualtrics. It’s a great product for survey delivery, data collection and management. It’s flexible and widely available for ANU affiliates. Few consultant statisticians would recommend Qualtrics as the sole tool for research data analysis either.

In the updated words of R.A. Fisher, “To consult the statistician after an experiment [or survey analysis] is finished is often merely to ask them to conduct a post mortem examination. They can perhaps say what the experiment died of.”

Please don’t let your Qualtrics survey die. Contact a statistician!
