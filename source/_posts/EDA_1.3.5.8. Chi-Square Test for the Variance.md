---
title: EDA_1.3.5.8. Chi-Square Test for the Variance
date: 2018-03-12 17:00:12
categories: "statistics"
tags:
     - Chi-Square Test for the Variance
description: EDA_1.3.5.8. Chi-Square Test for the Variance
toc: true
---
### Purpose: Test if the variance is equal to a specified value
A chi-square test ( Snedecor and Cochran, 1983) can be used to test if the variance of a population is equal to a specified value. This test can be either a two-sided test or a one-sided test. The two-sided version tests against the alternative that the true variance is either less than or greater than the specified value. The one-sided version only tests in one direction. The choice of a two-sided or one-sided test is determined by the problem. For example, if we are testing a new process, we may only be concerned if its variability is greater than the variability of the current process.

### Definition
The chi-square hypothesis test is defined as:

![](assets/EDA/eda358_1.png)

### Chi-Square Test Example
A chi-square test was performed for the GEAR.DAT data set. The observed variance for the 100 measurements of gear diameter is 0.00003969 (the standard deviation is 0.0063). We will test the null hypothesis that the true variance is equal to 0.01.

![](assets/EDA/eda358_2.png)


### Questions
The chi-square test can be used to answer the following questions:

    Is the variance equal to some pre-determined threshold value?
    Is the variance greater than some pre-determined threshold value?
    Is the variance less than some pre-determined threshold value?

### Related Techniques
* F Test
* Bartlett Test
* Levene Test

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda358.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda358.htm)
