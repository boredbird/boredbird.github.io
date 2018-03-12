---
title: EDA_1.3.5.7. Bartlett's Test
date: 2018-03-12 16:59:12
categories: "statistics"
tags:
     - Bartlett's Test
description: EDA_1.3.5.7. Bartlett's Test
toc: true
---
### Purpose: Test for Homogeneity of Variances
Bartlett's test (Snedecor and Cochran, 1983) is used to test if k samples have equal variances. Equal variances across samples is called homogeneity of variances. Some statistical tests, for example the analysis of variance, assume that variances are equal across groups or samples. The Bartlett test can be used to verify that assumption.

Bartlett's test is sensitive to departures from normality. That is, if your samples come from non-normal distributions, then Bartlett's test may simply be testing for non-normality. The Levene test is an alternative to the Bartlett test that is less sensitive to departures from normality.

### Definition
The Bartlett test is defined as:

![](assets/EDA/eda357_1.png)

### Example
Bartlett's test was performed for the GEAR.DATdata set. The data set contains 10 measurements of gear diameter for ten different batches for a total of 100 measurements.

    H0:  σ12 = σ22 = ... = σ102
    Ha:  At least one σi2 is not equal to the others.
    Test statistic:  T = 20.78580
    Degrees of freedom:  k - 1 = 9
    Significance level:  α = 0.05
    Critical value:  Χ21-α,k-1 = 16.919
    Critical region: Reject H0 if T > 16.919

We are testing the null hypothesis that the batch variances are all equal. Because the test statistic is larger than the critical value, we reject the null hypotheses at the 0.05 significance level and conclude that at least one batch variance is different from the others.

### Question
Bartlett's test can be used to answer the following question:

	• Is the assumption of equal variances valid?

### Importance
Bartlett's test is useful whenever the assumption of equal variances is made. In particular, this assumption is made for the frequently used one-way analysis of variance. In this case, Bartlett's or Levene's test should be applied to verify the assumption.

### Related Techniques
* Standard Deviation Plot
* Box Plot
* Levene Test
* Chi-Square Test
* Analysis of Variance

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda357.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda357.htm)
