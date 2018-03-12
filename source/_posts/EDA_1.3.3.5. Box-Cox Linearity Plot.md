---
title: EDA_1.3.3.5. Box-Cox Linearity Plot
date: 2018-03-02 14:26:12
categories: "statistics"
tags:
     - Box-Cox Linearity Plot

description: EDA_1.3.3.5. Box-Cox Linearity Plot
toc: true
---
### Purpose: 
Find the transformation of the X variable that maximizes the correlation between a Y and an X variable

When performing a linear fit of Y against X, an appropriate transformation of X can often significantly improve the fit. The Box-Cox transformation (Box and Cox, 1964) is a particularly useful family of transformations. It is defined as:
>	T(X)=(Xλ−1)/λ

where X is the variable being transformed and λis the transformation parameter. For λ = 0, the natural log of the data is taken instead of using the above formula.

The Box-Cox linearity plot is a plot of the correlation between Y and the transformed X for given values of λ. That is, λ is the coordinate for the horizontal axis variable and the value of the correlation between Y and the transformed X is the coordinate for the vertical axis of the plot. The value of λcorresponding to the maximum correlation (or minimum for negative correlation) on the plot is then the optimal choice for λ.

Transforming X is used to improve the fit. The Box-Cox transformation applied to Y can be used as the basis for meeting the error assumptions. That case is not covered here. See page 225 of (Draper and Smith, 1981) or page 77 of (Ryan, 1997) for a discussion of this case.

### Sample Plot

![](assets/EDA/bootstra.gif)

The plot of the original data with the predicted values from a linear fit indicate that a quadratic fit might be preferable. The Box-Cox linearity plot shows a value of λ = 2.0. The plot of the transformed data with the predicted values from a linear fit with the transformed data shows a better fit (verified by the significant reduction in the residual standard deviation).

### Definition
Box-Cox linearity plots are formed by
* Vertical axis: Correlation coefficient from the transformed X and Y
* Horizontal axis: Value for λ

### Questions
The Box-Cox linearity plot can provide answers to the following questions:
	1. Would a suitable transformation improve my fit?
	2. What is the optimal value of the transformation parameter?

### Importance: 
Find a suitable transformation

Transformations can often significantly improve a fit. The Box-Cox linearity plot provides a convenient way to find a suitable transformation without engaging in a lot of trial and error fitting.

### Related Techniques
* Linear Regression 
* Box-Cox Normality Plot
