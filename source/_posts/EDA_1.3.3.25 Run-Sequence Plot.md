---
title: EDA_1.3.3.25 Run-Sequence Plot
date: 2018-03-12 15:36:12
categories: "statistics"
tags:
     - Run-Sequence Plot
description: EDA_1.3.3.25 Run-Sequence Plot
toc: true
---
### Purpose: Check for Shifts in Location and Scale and Outliers
Run sequence plots (Chambers 1983) are an easy way to graphically summarize a univariate data set. A common assumption of univariate data sets is that they behave like:

	1. random drawings;
	2. from a fixed distribution;
	3. with a common location; and
	4. with a common scale.

With run sequence plots, shifts in location and scale are typically quite evident. Also, outliers can easily be detected.

### Sample Plot:
![](assets/EDA/runseq.gif)

Last Third of Data Shows a Shift of Location

This sample run sequence plot shows that the location shifts up for the last third of the data.
### Definition:

    y(i) Versus i

Run sequence plots are formed by:

	• Vertical axis: Response variable Yi
	• Horizontal axis: Index i (i = 1, 2, 3, ... )

### Questions
The run sequence plot can be used to answer the following questions

	1. Are there any shifts in location?
	2. Are there any shifts in variation?
	3. Are there any outliers?

The run sequence plot can also give the analyst an excellent feel for the data.

### Importance: Check Univariate Assumptions
For univariate data, the default model is

	Y = constant + error

where the error is assumed to be random, from a fixed distribution, and with constant location and scale. The validity of this model depends on the validity of these assumptions. The run sequence plot is useful for checking for constant location and scale.

Even for more complex models, the assumptions on the error term are still often the same. That is, a run sequence plot of the residuals (even from very complex models) is still vital for checking for outliers and for detecting shifts in location and scale.

### Related Techniques
* Scatter Plot
* Histogram
* Autocorrelation Plot
* Lag Plot