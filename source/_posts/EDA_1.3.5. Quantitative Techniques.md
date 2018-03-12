---
title: EDA_1.3.5. Quantitative Techniques
date: 2018-03-12 16:16:12
categories: "statistics"
tags:
     - Quantitative Techniques
description: EDA_1.3.5. Quantitative Techniques
toc: true
---
### Confirmatory Statistics
The techniques discussed in this section are classical statistical methods as opposed to EDA techniques. EDA and classical techniques are not mutually exclusive and can be used in a complementary fashion. For example, the analysis can start with some simple graphical techniques such as the 4-plot followed by the classical confirmatory methods discussed herein to provide more rigorous statements about the conclusions. If the classical methods yield different conclusions than the graphical analysis, then some effort should be invested to explain why. Often this is an indication that some of the assumptions of the classical techniques are violated.

Many of the quantitative techniques fall into two broad categories:

	1. Interval estimation
	2. Hypothesis tests

### Interval Estimates
It is common in statistics to estimate a parameter from a sample of data. The value of the parameter using all of the possible data, not just the sample data, is called the population parameter or true value of the parameter. An estimate of the true parameter value is made using the sample data. This is called a point estimate or a sample estimate.

For example, the most commonly used measure of location is the mean. The population, or true, mean is the sum of all the members of the given population divided by the number of members in the population. As it is typically impractical to measure every member of the population, a random sample is drawn from the population. The sample mean is calculated by summing the values in the sample and dividing by the number of values in the sample. This sample mean is then used as the point estimate of the population mean.

Interval estimates expand on point estimates by incorporating the uncertainty of the point estimate. In the example for the mean above, different samples from the same population will generate different values for the sample mean. An interval estimate quantifies this uncertainty in the sample estimate by computing lower and upper values of an interval which will, with a given level of confidence (i.e., probability), contain the population parameter.

### Hypothesis Tests
Hypothesis tests also address the uncertainty of the sample estimate. However, instead of providing an interval, a hypothesis test attempts to refute a specific claim about a population parameter based on the sample data. For example, the hypothesis might be one of the following:

	• the population mean is equal to 10
	• the population standard deviation is equal to 5
	• the means from two populations are equal
	• the standard deviations from 5 populations are equal

To reject a hypothesis is to conclude that it is false. However, to accept a hypothesis does not mean that it is true, only that we do not have evidence to believe otherwise. Thus hypothesis tests are usually stated in terms of both a condition that is doubted (null hypothesis) and a condition that is believed (alternative hypothesis).

A common format for a hypothesis test is:

    H0:	A statement of the null hypothesis, e.g., two population means are equal.

    Ha:	A statement of the alternative hypothesis, e.g., two population means are not equal.

    Test Statistic:	The test statistic is based on the specific hypothesis test.

    Significance Level:	The significance level, α,defines the sensitivity of the test. A value of α = 0.05 means that we inadvertently reject the null hypothesis 5% of the time when it is in fact true. This is also called the type I error. The choice of α is somewhat arbitrary, although in practice values of 0.1, 0.05, and 0.01 are commonly used.

	The probability of rejecting the null hypothesis when it is in fact false is called the power of the test and is denoted by 1 - β. Its complement, the probability of accepting the null hypothesis when the alternative hypothesis is, in fact, true (type II error), is called β and can only be computed for a specific alternative hypothesis.

    Critical Region:	The critical region encompasses those values of the test statistic that lead to a rejection of the null hypothesis. Based on the distribution of the test statistic and the significance level, a cut-off value for the test statistic is computed. Values either above or below or both (depending on the direction of the test) this cut-off define the critical region.

### Practical Versus Statistical Significance
It is important to distinguish between statistical significance and practical significance. Statistical significance simply means that we reject the null hypothesis. The ability of the test to detect differences that lead to rejection of the null hypothesis depends on the sample size. For example, for a particularly large sample, the test may reject the null hypothesis that two process means are equivalent. However, in practice the difference between the two means may be relatively small to the point of having no real engineering significance.

Similarly, if the sample size is small, a difference that is large in engineering terms may not lead to rejection of the null hypothesis. The analyst should not just blindly apply the tests, but should combine engineering judgement with statistical analysis.

### Bootstrap Uncertainty Estimates
In some cases, it is possible to mathematically derive appropriate uncertainty intervals. This is particularly true for intervals based on the assumption of a normal distribution. However, there are many cases in which it is not possible to mathematically derive the uncertainty. In these cases, the bootstrap provides a method for empirically determining an appropriate interval.

### Table of Contents
Some of the more common classical quantitative techniques are listed below. This list of quantitative techniques is by no means meant to be exhaustive. Additional discussions of classical statistical techniques are contained in the product comparisons chapter.

	• Location
		1. Measures of Location
		2. Confidence Limits for the Mean and One Sample t-Test
		3. Two Sample t-Test for Equal Means
		4. One Factor Analysis of Variance
		5. Multi-Factor Analysis of Variance
	• Scale (or variability or spread)
		1. Measures of Scale
		2. Bartlett's Test
		3. Chi-Square Test
		4. F-Test
		5. Levene Test
	• Skewness and Kurtosis
		1. Measures of Skewness and Kurtosis
	• Randomness
		1. Autocorrelation
		2. Runs Test
	• Distributional Measures
		1. Anderson-Darling Test
		2. Chi-Square Goodness-of-Fit Test
		3. Kolmogorov-Smirnov Test
	• Outliers
		1. Detection of Outliers
		2. Grubbs Test
		3. Tietjen-Moore Test
		4. Generalized Extreme Deviate Test
	• 2-Level Factorial Designs
		1. Yates Algorithm
