---
title: EDA_1.3.3.30. Weibull Plot
date: 2018-03-12 15:56:12
categories: "statistics"
tags:
     - Weibull Plot
description: EDA_1.3.3.30. Weibull Plot
toc: true
---
### Purpose: Graphical Check To See If Data Come From a Population That Would Be Fit by a Weibull Distribution
The Weibull plot (Nelson 1982) is a graphical technique for determining if a data set comes from a population that would logically be fit by a 2-parameter Weibull distribution (the location is assumed to be zero).

The Weibull plot has special scales that are designed so that if the data do in fact follow a Weibull distribution, the points will be linear (or nearly linear). The least squares fit of this line yields estimates for the shape and scale parameters of the Weibull distribution (the location is assumed to be zero).

Specifically, the shape parameter is the reciprocal of the slope of the fitted line and the scale parameter is the exponent of the intercept of the fitted line.
The Weibull distribution also has the property that the scale parameter falls at the 63.2% point irrespective of the value of the shape parameter. The plot shows a horizontal line at this 63.2% point and a vertical line where the horizontal line intersects the least squares fitted line. This vertical line shows the value of scale parameter.
### Sample Plot
![](assets/EDA/weibullp.gif)

This Weibull plot shows that:

	1. the assumption of a Weibull distribution is reasonable;
	2. the scale parameter estimate is computed to be 33.32;
	3. the shape parameter estimate is computed to be 5.28; and
	4. there are no outliers.

Note that the values on the x-axis ("0", "1", and "2") are the exponents. These actually denote the value 100 = 1, 101 = 10, and 102 = 100.

### Definition:
Weibull Cumulative Probability Versus LN(Ordered Response)

The Weibull plot is formed by:

	• Vertical axis: Weibull cumulative probability expressed as a percentage
	• Horizontal axis: ordered failure times (in a LOG10 scale)

The vertical scale is ln(-ln(1-p)) where p=(i-0.3)/(n+0.4) and i is the rank of the observation. This scale is chosen in order to linearize the resulting plot for Weibull data.
### Questions
The Weibull plot can be used to answer the following questions:

	1. Do the data follow a 2-parameter Weibull distribution?
	2. What is the best estimate of the shape parameter for the 2-parameter Weibull distribution?
	3. What is the best estimate of the scale (= variation) parameter for the 2-parameter Weibull distribution?

### Importance:
Check Distributional Assumptions

Many statistical analyses, particularly in the field of reliability, are based on the assumption that the data follow a Weibull distribution. If the analysis assumes the data follow a Weibull distribution, it is important to verify this assumption and, if verified, find good estimates of the Weibull parameters.

### Related Techniques
* Weibull Probability Plot
* Weibull PPCC Plot
* Weibull Hazard Plot

The Weibull probability plot (in conjunction with the Weibull PPCC plot), the Weibull hazard plot, and the Weibull plot are all similar techniques that can be used for assessing the adequacy of the Weibull distribution as a model for the data, and additionally providing estimation for the shape, scale, or location parameters.
The Weibull hazard plot and Weibull plot are designed to handle censored data (which the Weibull probability plot does not).
