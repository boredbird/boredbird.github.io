---
title: EDA_1.3.5.10. Levene Test for Equality of Variances
date: 2018-03-12 17:00:12
categories: "statistics"
tags:
     - Levene Test for Equality of Variances
description: EDA_1.3.5.10. Levene Test for Equality of Variances
toc: true
---
### Purpose: Test for Homogeneity of Variances
Levene's test ( Levene 1960) is used to test if ksamples have equal variances. Equal variances across samples is called homogeneity of variance. Some statistical tests, for example the analysis of variance, assume that variances are equal across groups or samples. The Levene test can be used to verify that assumption.

Levene's test is an alternative to the Bartlett test. The Levene test is less sensitive than the Bartlett test to departures from normality. If you have strong evidence that your data do in fact come from a normal, or nearly normal, distribution, then Bartlett's test has better performance.

### Definition
The Levene test is defined as:

![](assets/EDA/eda35a_1.png)

The three choices for defining Zijdetermine the robustness and power of Levene's test. By robustness, we mean the ability of the test to not falsely detect unequal variances when the underlying data are not normally distributed and the variables are in fact equal. By power, we mean the ability of the test to detect unequal variances when the variances are in fact unequal.

Levene's original paper only proposed using the mean. Brown and Forsythe (1974)) extended Levene's test to use either the median or the trimmed mean in addition to the mean. They performed Monte Carlo studies that indicated that using the trimmed mean performed best when the underlying data followed a Cauchy distribution (i.e., heavy-tailed) and the median performed best when the underlying data followed a χ24 (i.e., skewed) distribution. Using the mean provided the best power for symmetric, moderate-tailed, distributions.

Although the optimal choice depends on the underlying distribution, the definition based on the median is recommended as the choice that provides good robustness against many types of non-normal data while retaining good power. If you have knowledge of the underlying distribution of the data, this may indicate using one of the other choices.

Significance Level:	  α

![](assets/EDA/eda35a_2.png)

### Levene's Test Example
Levene's test, based on the median, was performed for the GEAR.DAT data set. The data set includes ten measurements of gear diameter for each of ten batches for a total of 100 measurements.

    H0:  σ12 = ... = σ102
    Ha:  σ12 ≠ ... ≠ σ102
    Test statistic:  W = 1.705910
    Degrees of freedom:  k-1 = 10-1 = 9
                         N-k = 100-10 = 90
    Significance level:  α = 0.05
    Critical value (upper tail):  Fα,k-1,N-k = 1.9855
    Critical region: Reject H0 if F > 1.9855

We are testing the hypothesis that the group variances are equal. We fail to reject the null hypothesis at the 0.05 significance level since the value of the Levene test statistic is less than the critical value. We conclude that there is insufficient evidence to claim that the variances are not equal.

### Question
Levene's test can be used to answer the following question:

	• Is the assumption of equal variances valid?

### Related Techniques
* Standard Deviation Plot
* Box Plot
* Bartlett Test
* Chi-Square Test
* Analysis of Variance

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda35a.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda35a.htm)
