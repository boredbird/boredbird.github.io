---
title: One-Way Tables and Goodness-of-Fit Test
date: 2017-12-04 20:26:12 
categories: "statistics" 
tags: 
     - Sampling distribution
     - Central Limit Theorem
description: One-Way Tables and Goodness-of-Fit Test
toc: true
---
# Statistical Inference

Recall, a **statistical inference** aims at learning characteristics of the population from a sample; the population characteristics are *parameters* and sample characteristics are *statistics*.

A **statistical model** is a representation of a complex phenomena that generated the data.

* It has mathematical formulations that describe relationships between random variables and parameters.
* It makes assumptions about the random variables, and sometimes parameters.
* A general form: data = model + residuals
* Model should explain most of the variation in the data
* Residuals are a representation of a lack-of-fit, that is of the portion of the data unexplained by the model.

<!--more-->

**Estimation** represents ways or a process of learning and determining the population parameter based on the model fitted to the data.

Point estimation and interval estimation, and hypothesis testing are three main ways of learning about the population parameter from the sample statistic.

An **estimator** is particular example of a statistic, which becomes an **estimate** when the formula is replaced with actual observed sample values.

**Point estimation** = a single value that estimates the parameter. Point estimates are single values calculated from the sample

**Confidence Intervals** = gives a range of values for the parameter Interval estimates are intervals within which the parameter is expected to fall, with a certain degree of confidence.

**Hypothesis tests** = tests for a specific value(s) of the parameter.

In order to perform these inferential tasks, i.e., make inference about the unknown population parameter from the sample statistic, we need to know the likely values of the sample statistic. What would happen if we do sampling many times?

![](https://onlinecourses.science.psu.edu/stat504/sites/onlinecourses.science.psu.edu.stat504/files/lesson01/height_plot.gif)

## CLT,Central Limit Theorem
Sampling distribution of the sample mean:

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204144632.png)

For categorical data, the CLT holds for the sampling distribution of the sample proportion.

So, what is the 95% confidence interval? Based on the CLT, the 95% CI is

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204145320.png)

# Point Estimation
**Estimation** represents ways or a process of learning and determining the population parameter based on the model fitted to the data.

*Point estimation* and interval estimation, and hypothesis testing are three main ways of learning about the population parameter from the sample statistic.

An **estimator** is particular example of a statistic, which becomes an **estimate** when the formula is replaced with actual observed sample values.

**Point estimation** = a single value that estimates the parameter. Point estimates are single values calculated from the sample

# Model & Estimation
A statistical model is a representation of a complex phenomena that generated the data.

* It has mathematical formulations that describe relationships between random variables and parameters.
* It makes assumptions about the random variables, and sometimes parameters.
* A general form: data = model + residuals
* Model should explain most of the variation in the data
* Residuals are a representation of a lack-of-fit, that is of the portion of the data unexplained by the model.

In models, the focus is on estimating the model parameters. The basic inference tools (e.g., point estimation, hypothesis testing, and confidence intervals) will be applied to the these parameters. When discussing models, we will keep in mind the following parts:

## Objective

State what the objective is for this model. For instance, "Estimate the probability that a characteristic is present given the value of the explanatory values are ... "

## Model Structure

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204150533.png)

# Confidence Intervals
## General form of a confidence interval (CI)
A confidence interval estimates are intervals within which the parameter is expected to fall, with a certain degree of confidence.

The general form:

* estimate ± critical value × std.dev of the estimate
* estimate ± margin of error
For example:

* sample mean ± critical value × estimated standard error

The CIs differ based on:

* The parameter of interest, e.g., population mean, population proportion, difference in population's means, etc…
* Design of the sample: SRS, stratified, experiments
* Confidence level or a confidence coefficient, (1 - α)100%, e.g., 95%, 99%, 90%, 80%, corresponding, respectively, to α values of 0.05, 0.01, 0.1, 0.2, etc…

## Interpretation of a Confidence Interval
In most general terms, for a 95% CI, we say “we are 95% confident that the true population parameter is between the lower and upper calculated values”.

A 95% CI for a population parameter DOES NOT mean that the interval has a probability of 0.95 that the true value of the parameter falls in the interval.

The CI either contains the parameter or it does not contain it.

The probability is associated with the process that generated the interval. And if we repeat this process many times, 95% of all intervals should in fact contain the true value of the parameter.

What does a 99% CI say?

Would you choose a 99% or 95% CI, and why?

## Tradeoffs
We want confidence coefficient to be closer to 1.

We want the sample size to be as small as possible (but not too small). This is a practical issue.

We want the CI to be as narrow as possible

* As we increase the sample estimate, the CI …?
* As we decrease st. dev, the CI …?
* As we decrease the confidence level, (1-α), the CI …?
* As we increase sample size….?

## z-Tests & Intervals
![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204151437.png)

## More About Confidence Intervals
### Simplified Expression for a 95% Confidence Interval
![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204151631.png)
### Generalizing the 95% Confidence Interval
![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204151714.png)

> **Height Example**
>
* Assume that the s is known and is equal to 3.
* We want to estimate the unknown true height of our population.
* Point sample estimate, can be the sample mean, 66.463.
* What is the distribution of the sample mean?
* What is the 95% confidence interval? What does it mean?
>
![](https://onlinecourses.science.psu.edu/stat504/sites/onlinecourses.science.psu.edu.stat504/files/lesson01/sas_output_height.gif)

## Confidence Intervals for Proportions in Newspapers
As found in CNN in June, 2006:
![](https://onlinecourses.science.psu.edu/stat504/sites/onlinecourses.science.psu.edu.stat504/files/lesson01/cnn_01.gif)

The stated **Margin of error**: +/- 3%

Therefore, this would be the **Confidence interval**: 62%+/- 3%.

We can be really confident that between 59% and 65% of all U.S. adults disapprove of how President Bush is handling the situation in Iraq.

# Hypothesis Testing
## Basic approach to hypothesis testing
* 1. **State a model** describing the relationship between the explanatory variables and the outcome variable(s) in the population and the nature of the variability. **State all of your assumptions**.
* 2. **Specify the null and alternative hypotheses** in terms of the parameters of the model.
* 3. Invent a **test statistic** that will tend to be different under the null and alternative hypotheses.
* 4. Using the assumptions of step 1, **find the theoretical sampling distribution** of the statistic under the null hypothesis of step 2. Ideally the form of the sampling distribution should be one of the “standard distributions”(e.g. normal, t, binomial..)
* 5. **Calculate a p-value**, as the area under the sampling distribution more extreme than your statistic. Depends on the form of the alternative hypothesis.
* 6. **Choose your acceptable type 1 error rate** (alpha) and **apply the decision rule**: reject the null hypothesis if the p-value is less than alpha, otherwise do not reject.

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204153045.png)

## Making the Decision

It is either **likely** or **unlikely** that we would collect the evidence we did given the initial assumption. (Note: “likely” or “unlikely” is measured by calculating a probability!)

If it is likely, then we “do not reject” our initial assumption. There is not enough evidence to do otherwise.

If it is unlikely, then:

either our initial assumption is correct and we experienced an unusual event or,
our initial assumption is incorrect
In statistics, if it is unlikely, we decide to “reject” our initial assumption.

## Example: Criminal Trial Analogy
First, state 2 hypotheses, the **null hypothesis** (“H0”) and the **alternative hypothesis** (“HA”)

* H0: Defendant is not guilty.
* HA: Defendant is guilty.

Usually the H0 is a statement of “no effect”, or “no change”, or “chance only” about a population parameter.

While the HA , depending on the situation, is that there is a difference, trend, effect, or a relationship with respect to a population parameter.

* It can one-sided and two-sided.
* In two-sided we only care there is a difference, but not the direction of it. In one-sided we care about a particular direction of the relationship. We want to know if the value is strictly larger or smaller.

Then, collect evidence, such as finger prints, blood spots, hair samples, carpet fibers, shoe prints, ransom notes, handwriting samples, etc. (In statistics, the data are the evidence.)

Next, you make your initial assumption.

* Defendant is innocent until proven guilty.

In statistics, **we always assume the null hypothesis is true**.

Then, make a decision based on the available evidence.

* If there is sufficient evidence (“beyond a reasonable doubt”), **reject the null hypothesis**. (Behave as if defendant is guilty.)
* If there is not enough evidence, **do not reject the null hypothesis**. (Behave as if defendant is not guilty.)

If the observed outcome, e.g., a sample statistic, is surprising under the assumption that the null hypothesis is true, but more probable if the alternative is true, then this outcome is evidence against H0 and in favor of HA.

An observed effect so large that it would rarely occur by chance is called statistically significant (i.e., not likely to happen by chance).

## Using the p-value to make the decision
The p-value represents **how likely** we would be to observe such an extreme sample if the null hypothesis were true. The **p-value is a probability** computed assuming the null hypothesis is true, that the test statistic would take a value as extreme or more extreme than that actually observed. Since it's a probability, it is a number between 0 and 1. The closer the number is to 0 means the event is “unlikely.” So if p-value is “small,” (typically, less than 0.05), we can then reject the null hypothesis.

### Significance level and p-value
Significance level, α, is a decisive value for p-value. In this context, significant does not mean “important”, but it means “not likely to happened just by chance”.

α is the maximum probability of rejecting the null hypothesis when the null hypothesis is true. If α = 1 we always reject the null, if α = 0 we never reject the null hypothesis. In articles, journals, etc… you may read: “The results were significant (p<0.05).” So if p=0.03, it's significant at the level of α = 0.05 but not at the level of α = 0.01. If we reject the H0 at the level of α = 0.05 (which corresponds to 95% CI), we are saying that if H0 is true, the observed phenomenon would happen no more than 5% of the time (that is 1 in 20). If we choose to compare the p-value to α = 0.01, we are insisting on a stronger evidence!

### Errors in Hypothesis Testing
![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204154105.png)

## Power
The power of a statistical test is its probability of rejecting the null hypothesis if the null hypothesis is false. That is, power is the ability to correctly reject H0 and detect a significant effect. In other words, power is one minus the type II error risk.

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204154312.png)

Which error is worse?

Type I = you are innocent, yet accused of cheating on the test.

Type II = you cheated on the test, but you are found innocent.

This depends on the context of the problem too. But in most cases scientists are trying to be “conservative”; it's worse to make a spurious discovery than to fail to make a good one. Our goal it to increase the power of the test that is to minimize the length of the CI.

We need to keep in mind:
* the effect of the sample size,
* the correctness of the underlying assumptions about the population,
* statistical vs. practical significance, etc…

**sometimes the p-value is too low because of the large sample size, and we may have statistical significance but not really practical significance! **

That's why most statisticians are much more comfortable with **using CI than tests**.


There is a need for a further generalization. What if we can't assume that σ is known? In this case we would use s (the sample standard deviation) to estimate σ.

If the sample is very large, we can treat σ as known by assuming that σ = s. According to the law of large numbers, this is not too bad a thing to do. But if the sample is small, the fact that we have to estimate both the standard deviation and the mean adds extra uncertainty to our inference. In practice this means that we need a larger multiplier for the standard error.

We need one-sample t-test.
### One sample t-test
![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204155319.png)







