---
title: EDA_1.3.5.14. Anderson-Darling Test
date: 2018-03-12 17:02:12
categories: "statistics"
tags:
     - Anderson-Darling Test
description: EDA_1.3.5.14. Anderson-Darling Test
toc: true
---
### Purpose: Test for Distributional Adequacy
The Anderson-Darling test (Stephens, 1974) is used to test if a sample of data came from a population with a specific distribution. It is a modification of theKolmogorov-Smirnov (K-S) test and gives more weight to the tails than does the K-S test. The K-S test is distribution free in the sense that the critical values do not depend on the specific distribution being tested (note that this is true only for a fully specified distribution, i.e. the parameters are known). The Anderson-Darling test makes use of the specific distribution in calculating critical values. This has the advantage of allowing a more sensitive test and the disadvantage that critical values must be calculated for each distribution. Currently, tables of critical values are available for the normal, uniform, lognormal,exponential, Weibull, extreme value type I, generalized Pareto, and logistic distributions. We do not provide the tables of critical values in this Handbook (seeStephens 1974, 1976, 1977, and 1979) since this test is usually applied with a statistical software program that will print the relevant critical values.
The Anderson-Darling test is an alternative to the chi-square and Kolmogorov-Smirnov goodness-of-fit tests.

### Definition

![](assets/EDA/eda35e_1.png)

### Sample Output
We generated 1,000 random numbers for normal, double exponential, Cauchy, and lognormal distributions. In all four cases, the Anderson-Darling test was applied to test for a normal distribution.
The normal random numbers were stored in the variable Y1, the double exponential random numbers were stored in the variable Y2, the Cauchy random numbers were stored in the variable Y3, and the lognormal random numbers were stored in the variable Y4.

      Distribution                 Mean       Standard Deviation
      ------------               --------     ------------------
      Normal (Y1)                0.004360          1.001816
      Double Exponential (Y2)    0.020349          1.321627
      Cauchy (Y3)                1.503854         35.130590
      Lognormal (Y4)             1.518372          1.719969

      H0:  the data are normally distributed
      Ha:  the data are not normally distributed
      Y1 adjusted test statistic:  A2 =   0.2576
      Y2 adjusted test statistic:  A2 =   5.8492
      Y3 adjusted test statistic:  A2 = 288.7863
      Y4 adjusted test statistic:  A2 =  83.3935
      Significance level:  α = 0.05
      Critical value:  0.752   
      Critical region:  Reject H0 if A2 > 0.752

When the data were generated using a normal distribution, the test statistic was small and the hypothesis of normality was not rejected. When the data were generated using the double exponential, Cauchy, and lognormal distributions, the test statistics were large, and the hypothesis of an underlying normal distribution was rejected at the 0.05 significance level.

### Questions
The Anderson-Darling test can be used to answer the following questions:

	• Are the data from a normal distribution?
	• Are the data from a log-normal distribution?
	• Are the data from a Weibull distribution?
	• Are the data from an exponential distribution?
	• Are the data from a logistic distribution?

### Importance
Many statistical tests and procedures are based on specific distributional assumptions. The assumption of normality is particularly common in classical statistical tests. Much reliability modeling is based on the assumption that the data follow a Weibull distribution.

There are many non-parametric and robust techniques that do not make strong distributional assumptions. However, techniques based on specific distributional assumptions are in general more powerful than non-parametric and robust techniques. Therefore, if the distributional assumptions can be validated, they are generally preferred.

### Related Techniques
* Chi-Square goodness-of-fit Test
* Kolmogorov-Smirnov Test
* Shapiro-Wilk Normality Test
* Probability Plot
* Probability Plot Correlation Coefficient Plot

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda35e.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda35e.htm)
