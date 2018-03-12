---
title: EDA_1.3.3.6. Box-Cox Normality Plot
date: 2018-03-02 15:26:12
categories: "statistics"
tags:
     - Box-Cox Normality Plot

description: EDA_1.3.3.6. Box-Cox Normality Plot
toc: true
---
### Purpose: 
Find transformation to normalize data

Many statistical tests and intervals are based on the assumption of normality. The assumption of normality often leads to tests that are simple, mathematically tractable, and powerful compared to tests that do not make the normality assumption. Unfortunately, many real data sets are in fact not normal. However, an appropriate transformation of a data set can often yield a data set that does follow a normal distribution. This increases the applicability and usefulness of statistical techniques based on the normality assumption.
The Box-Cox transformation is a particulary useful family of transformations. It is defined as:

![](assets/EDA/boxcoxeq.gif)

where X is the response variable and 

lamda is the transformation parameter. For 
lamda = 0, the log of the data is taken instead of using the above formula.
Given a particular transformation, it is helpful to define a measure of the normality of the resulting transformation. One measure is to compute the correlation coefficient of a normal probability plot. The correlation is computed between the vertical and horizontal axis variables of the probability plot and is a convenient measure of the linearity of the probability plot (the more linear the probability plot, the better a normal distribution fits the data).
The Box-Cox normality plot is a plot of these correlation coefficients for various values of the lambda parameter. The value of lambda corresponding to the maximum correlation on the plot is then the optimal choice for 

### Sample Plot

![](assets/EDA/boxcox.gif)

The histogram in the upper left-hand shows a data set that has significant right skewness (and so does not follow a normal distribution).

The Box-Cox normality plot shows that the maximum value of the correlation coefficient is at 
lamda = -0.3.
The histogram of the data after applying the Box-Cox transformation with lamda = -0.3. shows a data set for which the normality assumption is reasonable. This is verified with a normal probability plot of the transformed data.

### Definition
Box-Cox normality plots are formed by:
* Vertical axis: Correlation coefficient from the normal probability plot after applying Box-Cox transformation
* Horizontal axis: Value for 

	 
### Questions
The Box-Cox normality plot can provide answers to the following questions:
	1. Is there a transformation that will normalize my data?
	2. What is the optimal value of the transformation parameter?

### Importance: 
Normalization improves validity of tests

Normality assumptions are critical for many univariate intervals and tests. It is important to test this normality assumption. If the data are in fact not normal, the Box-Cox normality plot can often be used to find a transformation that will normalize the data.

### Related Techniques
* Normal Probability Plot 
* Box-Cox Linearity Plot
