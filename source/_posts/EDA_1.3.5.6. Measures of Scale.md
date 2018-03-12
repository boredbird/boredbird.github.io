---
title: EDA_1.3.5.6. Measures of Scale
date: 2018-03-12 16:59:12
categories: "statistics"
tags:
     - Measures of Scale
description: EDA_1.3.5.6. Measures of Scale
toc: true
---
### Scale, Variability, or Spread
A fundamental task in many statistical analyses is to characterize the spread, or variability, of a data set. Measures of scale are simply attempts to estimate this variability.
When assessing the variability of a data set, there are two key components:

	1. How spread out are the data values near the center?
	2. How spread out are the tails?

Different numerical summaries will give different weight to these two elements. The choice of scale estimator is often driven by which of these components you want to emphasize.

The histogram is an effective graphical technique for showing both of these components of the spread.

### Definitions of Variability
For univariate data, there are several common numerical measures of the spread:

	1. variance - the variance is defined as
    s2=∑Ni=1(Yi−Y¯)2/(N−1)
    where Y¯ is the mean of the data.
    The variance is roughly the arithmetic average of the squared distance from the mean. Squaring the distance from the mean has the effect of giving greater weight to values that are further from the mean. For example, a point 2 units from the mean adds 4 to the above sum while a point 10 units from the mean adds 100 to the sum. Although the variance is intended to be an overall measure of spread, it can be greatly affected by the tail behavior.
	2. standard deviation - the standard deviation is the square root of the variance. That is,
    s=∑Ni=1(Yi−Y¯)2/(N−1)−−−−−−−−−−−−−−−−−−−√
    The standard deviation restores the units of the spread to the original data units (the variance squares the units).
	3. range - the range is the largest value minus the smallest value in a data set. Note that this measure is based only on the lowest and highest extreme values in the sample. The spread near the center of the data is not captured at all.
	4. average absolute deviation - the average absolute deviation (AAD) is defined as
    AAD=∑Ni=1(|Yi−Y¯|)/N
    where Y¯ is the mean of the data and |Y|is the absolute value of Y. This measure does not square the distance from the mean, so it is less affected by extreme observations than are the variance and standard deviation.
	5. median absolute deviation - the median absolute deviation (MAD) is defined as
    MAD=median(|Yi−Y~|)
    where Y~ is the median of the data and |Y|is the absolute value of Y. This is a variation of the average absolute deviation that is even less affected by extremes in the tail because the data in the tails have less influence on the calculation of the median than they do on the mean.
	6. interquartile range - this is the value of the 75th percentile minus the value of the 25th percentile. This measure of scale attempts to measure the variability of points near the center.

In summary, the variance, standard deviation, average absolute deviation, and median absolute deviation measure both aspects of the variability; that is, the variability near the center and the variability in the tails. They differ in that the average absolute deviation and median absolute deviation do not give undue weight to the tail behavior. On the other hand, the range only uses the two most extreme points and the interquartile range only uses the middle portion of the data.

### Why Different Measures?

The following example helps to clarify why these alternative defintions of spread are useful and necessary.
This plot shows histograms for 10,000 random numbers generated from a normal, a double exponential, a Cauchy, and a Tukey-Lambda distribution.

### Normal Distribution
The first histogram is a sample from a normal distribution. The standard deviation is 0.997, the median absolute deviation is 0.681, and the range is 7.87.

The normal distribution is a symmetric distribution with well-behaved tails and a single peak at the center of the distribution. By symmetric, we mean that the distribution can be folded about an axis so that the two sides coincide. That is, it behaves the same to the left and right of some center point. In this case, the median absolute deviation is a bit less than the standard deviation due to the downweighting of the tails. The range of a little less than 8 indicates the extreme values fall within about 4 standard deviations of the mean. If a histogram or normal probability plot indicates that your data are approximated well by a normal distribution, then it is reasonable to use the standard deviation as the spread estimator.

### Double Exponential Distribution
The second histogram is a sample from a double exponential distribution. The standard deviation is 1.417, the median absolute deviation is 0.706, and the range is 17.556.

Comparing the double exponential and the normal histograms shows that the double exponential has a stronger peak at the center, decays more rapidly near the center, and has much longer tails. Due to the longer tails, the standard deviation tends to be inflated compared to the normal. On the other hand, the median absolute deviation is only slightly larger than it is for the normal data. The longer tails are clearly reflected in the value of the range, which shows that the extremes fall about 6 standard deviations from the mean compared to about 4 for the normal data.

### Cauchy Distribution
The third histogram is a sample from a Cauchy distribution. The standard deviation is 998.389, the median absolute deviation is 1.16, and the range is 118,953.6.

The Cauchy distribution is a symmetric distribution with heavy tails and a single peak at the center of the distribution. The Cauchy distribution has the interesting property that collecting more data does not provide a more accurate estimate for the mean or standard deviation. That is, the sampling distribution of the means and standard deviation are equivalent to the sampling distribution of the original data. That means that for the Cauchy distribution the standard deviation is useless as a measure of the spread. From the histogram, it is clear that just about all the data are between about -5 and 5. However, a few very extreme values cause both the standard deviation and range to be extremely large. However, the median absolute deviation is only slightly larger than it is for the normal distribution. In this case, the median absolute deviation is clearly the better measure of spread.

Although the Cauchy distribution is an extreme case, it does illustrate the importance of heavy tails in measuring the spread. Extreme values in the tails can distort the standard deviation. However, these extreme values do not distort the median absolute deviation since the median absolute deviation is based on ranks. In general, for data with extreme values in the tails, the median absolute deviation or interquartile range can provide a more stable estimate of spread than the standard deviation.

### Tukey-Lambda Distribution
The fourth histogram is a sample from a Tukey lambda distribution with shape parameter λ = 1.2. The standard deviation is 0.49, the median absolute deviation is 0.427, and the range is 1.666.

The Tukey lambda distribution has a range limited to (-1/λ,1/λ). That is, it has truncated tails. In this case the standard deviation and median absolute deviation have closer values than for the other three examples which have significant tails.

### Robustness
Tukey and Mosteller defined two types of robustness where robustness is a lack of susceptibility to the effects of nonnormality.

	1. Robustness of validity means that the confidence intervals for a measure of the population spread (e.g., the standard deviation) have a 95 % chance of covering the true value (i.e., the population value) of that measure of spread regardless of the underlying distribution.
	2. Robustness of efficiency refers to high effectiveness in the face of non-normal tails. That is, confidence intervals for the measure of spread tend to be almost as narrow as the best that could be done if we knew the true shape of the distribution.

The standard deviation is an example of an estimator that is the best we can do if the underlying distribution is normal. However, it lacks robustness of validity. That is, confidence intervals based on the standard deviation tend to lack precision if the underlying distribution is in fact not normal.

The median absolute deviation and the interquartile range are estimates of scale that have robustness of validity. However, they are not particularly strong for robustness of efficiency.
If histograms and probability plots indicate that your data are in fact reasonably approximated by a normal distribution, then it makes sense to use the standard deviation as the estimate of scale. However, if your data are not normal, and in particular if there are long tails, then using an alternative measure such as the median absolute deviation, average absolute deviation, or interquartile range makes sense. The range is used in some applications, such as quality control, for its simplicity. In addition, comparing the range to the standard deviation gives an indication of the spread of the data in the tails.

Since the range is determined by the two most extreme points in the data set, we should be cautious about its use for large values of N.

Tukey and Mosteller give a scale estimator that has both robustness of validity and robustness of efficiency. However, it is more complicated and we do not give the formula here.

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda356.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda356.htm)
