---
title: EDA_1.3.3.20. Mean Plot
date: 2018-03-12 14:26:12
categories: "statistics"
tags:
     - Mean Plot
description: EDA_1.3.3.20. Mean Plot
toc: true
---
### Purpose: Detect changes in location between groups
Mean plots are used to see if the mean varies between different groups of the data. The grouping is determined by the analyst. In most cases, the data set contains a specific grouping variable. For example, the groups may be the levels of a factor variable. In the sample plot below, the months of the year provide the grouping.

Mean plots can be used with ungrouped data to determine if the mean is changing over time. In this case, the data are split into an arbitrary number of equal-sized groups. For example, a data series with 400 points can be divided into 10 groups of 40 points each. A mean plot can then be generated with these groups to see if the mean is increasing or decreasing over time.

Although the mean is the most commonly used measure of location, the same concept applies to other measures of location. For example, instead of plotting the mean of each group, the median or the trimmed mean might be plotted instead. This might be done if there were significant outliers in the data and a more robust measure of location than the mean was desired.

Mean plots are typically used in conjunction with standard deviation plots. The mean plot checks for shifts in location while the standard deviation plot checks for shifts in scale.

### Sample Plot
![](assets/EDA/meanplot.gif)

This sample mean plot shows a shift of location after the 6th month.

### Definition:
Group Means Versus Group ID

Mean plots are formed by:

	• Vertical axis: Group mean
	• Horizontal axis: Group identifier

A reference line is plotted at the overall mean.

### Questions
The mean plot can be used to answer the following questions.
	1. Are there any shifts in location?
	2. What is the magnitude of the shifts in location?
	3. Is there a distinct pattern in the shifts in location?

### Importance: Checking Assumptions
A common assumption in 1-factor analyses is that of constant location. That is, the location is the same for different levels of the factor variable. The mean plot provides a graphical check for that assumption. A common assumption for univariate data is that the location is constant. By grouping the data into equal intervals, the mean plot can provide a graphical test of this assumption.

### Related Techniques
* Standard Deviation Plot
* DOE Mean Plot
* Box Plot
