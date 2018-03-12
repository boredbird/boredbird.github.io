---
title: EDA_1.3.5.2 Confidence Limits for the Mean
date: 2018-03-12 16:46:12
categories: "statistics"
tags:
     - Confidence Limits for the Mean
description: EDA_1.3.5.2 Confidence Limits for the Mean
toc: true
---
### Purpose: Interval Estimate for Mean
Confidence limits for the mean (Snedecor and Cochran, 1989) are an interval estimate for the mean. Interval estimates are often desirable because the estimate of the mean varies from sample to sample. Instead of a single estimate for the mean, a confidence interval generates a lower and upper limit for the mean. The interval estimate gives an indication of how much uncertainty there is in our estimate of the true mean. The narrower the interval, the more precise is our estimate.

Confidence limits are expressed in terms of a confidence coefficient. Although the choice of confidence coefficient is somewhat arbitrary, in practice 90 %, 95 %, and 99 % intervals are often used, with 95 % being the most commonly used.

As a technical note, a 95 % confidence interval does not mean that there is a 95 % probability that the interval contains the true mean. The interval computed from a given sample either contains the true mean or it does not. Instead, the level of confidence is associated with the method of calculating the interval. The confidence coefficient is simply the proportion of samples of a given size that may be expected to contain the true mean. That is, for a 95 % confidence interval, if many samples are collected and the confidence interval computed, in the long run about 95 % of these intervals would contain the true mean.

### Definition: Confidence Interval
Confidence limits are defined as:

	Y¯±t1−α/2,N−1sN−−√

where Y¯ is the sample mean, s is the sample standard deviation, N is the sample size, α is the desired significance level, and t1-α/2,N-1 is the 100(1-α/2) percentile of the t distribution with N - 1 degrees of freedom. Note that the confidence coefficient is 1 - α.
From the formula, it is clear that the width of the interval is controlled by two factors:

	1. As N increases, the interval gets narrower from the N−−√ term.
    That is, one way to obtain more precise estimates for the mean is to increase the sample size.
	2. The larger the sample standard deviation, the larger the confidence interval. This simply means that noisy data, i.e., data with a large standard deviation, are going to generate wider intervals than data with a smaller standard deviation.

#### Definition: Hypothesis Test
To test whether the population mean has a specific value, μ0, against the two-sided alternative that it does not have a value μ0, the confidence interval is converted to hypothesis-test form. The test is a one-sample t-test, and it is defined as:

    H0:	μ=μ0
    Ha:	μ≠μ0
    Test Statistic:	T=(Y¯−μ0)/(s/N−−√) 
    	where Y¯, N, and s are defined as above.
    Significance Level:	α. The most commonly used value for α is 0.05.
    Critical Region:	Reject the null hypothesis that the mean is a specified value, μ0, if
    	        T<tα/2,N−1
    	or
    	        T>t1−α/2,N−1
    Confidence Interval Example
    We generated a 95 %, two-sided confidence interval for the ZARR13.DAT data set based on the following information.
    N                          = 195
    MEAN                       =   9.261460
    STANDARD DEVIATION         =   0.022789
    t1-0.025,N-1                 =   1.9723
    LOWER LIMIT = 9.261460 - 1.9723*0.022789/√195 
    UPPER LIMIT = 9.261460 + 1.9723*0.022789/√195 
    Thus, a 95 % confidence interval for the mean is (9.258242, 9.264679).
    t-Test Example
    We performed a two-sided, one-sample t-test using the ZARR13.DAT data set to test the null hypothesis that the population mean is equal to 5.
    H0:  μ = 5
    Ha:  μ ≠ 5
    Test statistic:  T = 2611.284
    Degrees of freedom:  ν = 194
    Significance level:  α = 0.05
    Critical value:  t1-α/2,ν = 1.9723
    Critical region:  Reject H0 if |T| > 1.9723

We reject the null hypotheses for our two-tailed t-test because the absolute value of the test statistic is greater than the critical value. If we were to perform an upper, one-tailed test, the critical value would be t1-α,ν = 1.6527, and we would still reject the null hypothesis.
The confidence interval provides an alternative to the hypothesis test. If the confidence interval contains 5, then H0 cannot be rejected. In our example, the confidence interval (9.258242, 9.264679) does not contain 5, indicating that the population mean does not equal 5 at the 0.05 level of significance.

In general, there are three possible alternative hypotheses and rejection regions for the one-sample t-test:

### Alternative Hypothesis	Rejection Region
    Ha: μ ≠ μ0	|T| > t1-α/2,ν
    Ha: μ > μ0	T > t1-α,ν
    Ha: μ < μ0	T < tα,ν

The rejection regions for three posssible alternative hypotheses using our example data are shown in the following graphs.

![](assets/EDA/eda352_r.gif)

### Questions
Confidence limits for the mean can be used to answer the following questions:

	1. What is a reasonable estimate for the mean?
	2. How much variability is there in the estimate of the mean?
	3. Does a given target value fall within the confidence limits?

### Related Techniques
* Two-Sample t-Test
* Confidence intervals for other location estimators such as the median or mid-mean tend to be mathematically difficult or intractable. For these cases, confidence intervals can be obtained using the bootstrap.


via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda352.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda352.htm)
