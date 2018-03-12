---
title: EDA_1.3.5.9. F-Test for Equality of Two Variances
date: 2018-03-12 17:00:12
categories: "statistics"
tags:
     - F-Test for Equality of Two Variances
description: EDA_1.3.5.9. F-Test for Equality of Two Variances
toc: true
---
### Purpose: Test if variances from two populations are equal
An F-test (Snedecor and Cochran, 1983) is used to test if the variances of two populations are equal. This test can be a two-tailed test or a one-tailed test. The two-tailed version tests against the alternative that the variances are not equal. The one-tailed version only tests in one direction, that is the variance from the first population is either greater than or less than (but not both) the second population variance. The choice is determined by the problem. For example, if we are testing a new process, we may only be interested in knowing if the new process is less variable than the old process.

### Definition
The F hypothesis test is defined as:

![](assets/EDA/eda359_1.png)

### F Test Example
The following F-test was generated for theAUTO83B.DAT data set. The data set contains 480 ceramic strength measurements for two batches of material. The summary statistics for each batch are shown below.

    BATCH 1:
       NUMBER OF OBSERVATIONS      =      240
       MEAN                        =    688.9987
       STANDARD DEVIATION          =    65.54909

    BATCH 2:
       NUMBER OF OBSERVATIONS      =      240
       MEAN                        =    611.1559
       STANDARD DEVIATION          =    61.85425
    We are testing the null hypothesis that the variances for the two batches are equal.
    H0:  σ12 = σ22
    Ha:  σ12 ≠ σ22
    Test statistic:  F = 1.123037
    Numerator degrees of freedom:  N1 - 1 = 239
    Denominator degrees of freedom:  N2 - 1 = 239
    Significance level:  α = 0.05
    Critical values:  F(1-α/2,N1-1,N2-1) = 0.7756
                      F(α/2,N1-1,N2-1) = 1.2894
    Rejection region:  Reject H0 if F < 0.7756 or F > 1.2894
    The F test indicates that there is not enough evidence to reject the null hypothesis that the two batch variancess are equal at the 0.05 significance level.

### Questions
The F-test can be used to answer the following questions:

	1. Do two samples come from populations with equal variancess?
	2. Does a new process, treatment, or test reduce the variability of the current process?

### Related Techniques
* Quantile-Quantile Plot
* Bihistogram
* Chi-Square Test
* Bartlett's Test
* Levene Test

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda359.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda359.htm)
