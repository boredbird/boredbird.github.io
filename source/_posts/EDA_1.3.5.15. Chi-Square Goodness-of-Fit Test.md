---
title: EDA_1.3.5.15. Chi-Square Goodness-of-Fit Test
date: 2018-03-12 17:03:12
categories: "statistics"
tags:
     - Chi-Square Goodness-of-Fit Test
description: EDA_1.3.5.15. Chi-Square Goodness-of-Fit Test
toc: true
---
### Purpose: Test for distributional adequacy
The chi-square test (Snedecor and Cochran, 1989) is used to test if a sample of data came from a population with a specific distribution.

An attractive feature of the chi-square goodness-of-fit test is that it can be applied to any univariate distribution for which you can calculate the cumulative distribution function. The chi-square goodness-of-fit test is applied to binned data (i.e., data put into classes). This is actually not a restriction since for non-binned data you can simply calculate a histogram or frequency table before generating the chi-square test. However, the value of the chi-square test statistic are dependent on how the data is binned. Another disadvantage of the chi-square test is that it requires a sufficient sample size in order for the chi-square approximation to be valid.

The chi-square test is an alternative to theAnderson-Darling and Kolmogorov-Smirnovgoodness-of-fit tests. The chi-square goodness-of-fit test can be applied to discrete distributions such as the binomialand the Poisson. The Kolmogorov-Smirnov and Anderson-Darling tests are restricted to continuous distributions.

Additional discussion of the chi-square goodness-of-fit test is contained in theproduct and process comparisons chapter (chapter 7).

### Definition
The chi-square test is defined for the hypothesis:

![](assets/EDA/eda35f_1.png)
![](assets/EDA/eda35f_2.png)


### Chi-Square Test Example
We generated 1,000 random numbers for normal, double exponential, t with 3 degrees of freedom, and lognormal distributions. In all cases, a chi-square test with k = 32 bins was applied to test for normally distributed data. Because the normal distribution has two parameters, c = 2 + 1 = 3

The normal random numbers were stored in the variable Y1, the double exponential random numbers were stored in the variable Y2, the trandom numbers were stored in the variable Y3, and the lognormal random numbers were stored in the variable Y4.

    H0:  the data are normally distributed
    Ha:  the data are not normally distributed  
    Y1 Test statistic:  Χ2 =   32.256
    Y2 Test statistic:  Χ2 =   91.776
    Y3 Test statistic:  Χ2 =  101.488
    Y4 Test statistic:  Χ2 = 1085.104
    Significance level:  α = 0.05
    Degrees of freedom:  k - c = 32 - 3 = 29
    Critical value:  Χ21-α,k-c = 42.557
    Critical region: Reject H0 if Χ2 > 42.557

As we would hope, the chi-square test fails to reject the null hypothesis for the normally distributed data set and rejects the null hypothesis for the three non-normal data sets.

### Questions
The chi-square test can be used to answer the following types of questions:

	• Are the data from a normal distribution?
	• Are the data from a log-normal distribution?
	• Are the data from a Weibull distribution?
	• Are the data from an exponential distribution?
	• Are the data from a logistic distribution?
	• Are the data from a binomial distribution?

### Importance
Many statistical tests and procedures are based on specific distributional assumptions. The assumption of normality is particularly common in classical statistical tests. Much reliability modeling is based on the assumption that the distribution of the data follows a Weibull distribution.

There are many non-parametric and robust techniques that are not based on strong distributional assumptions. By non-parametric, we mean a technique, such as the sign test, that is not based on a specific distributional assumption. By robust, we mean a statistical technique that performs well under a wide range of distributional assumptions. However, techniques based on specific distributional assumptions are in general more powerful than these non-parametric and robust techniques. By power, we mean the ability to detect a difference when that difference actually exists. Therefore, if the distributional assumption can be confirmed, the parametric techniques are generally preferred.

If you are using a technique that makes a normality (or some other type of distributional) assumption, it is important to confirm that this assumption is in fact justified. If it is, the more powerful parametric techniques can be used. If the distributional assumption is not justified, a non-parametric or robust technique may be required.
### Related Techniques
* Anderson-Darling Goodness-of-Fit Test
* Kolmogorov-Smirnov Test
* Shapiro-Wilk Normality Test
* Probability Plots
* Probability Plot Correlation Coefficient Plot

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda35f.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda35f.htm)
