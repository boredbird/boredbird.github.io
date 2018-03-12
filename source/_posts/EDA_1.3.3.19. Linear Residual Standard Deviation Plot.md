---
title: EDA_1.3.3.19. Linear Residual Standard Deviation Plot
date: 2018-03-12 13:26:12
categories: "statistics"
tags:
     - Linear Residual Standard Deviation Plot
description: EDA_1.3.3.19. Linear Residual Standard Deviation Plot
toc: true
---
### Purpose: Detect Changes in Linear Residual Standard Deviation Between Groups
Linear residual standard deviation (RESSD) plots are used to graphically assess whether or not linear fits are consistent across groups. That is, if your data have groups, you may want to know if a single fit can be used across all the groups or whether separate fits are required for each group.

The residual standard deviation is a goodness-of-fit measure. That is, the smaller the residual standard deviation, the closer is the fit to the data.

Linear RESSD plots are typically used in conjunction with linear intercept and linear slope plots. The linear intercept and slope plots convey whether or not the fits are consistent across groups while the linear RESSD plot conveys whether the adequacy of the fit is consistent across groups.

In some cases you might not have groups. Instead, you have different data sets and you want to know if the same fit can be adequately applied to each of the data sets. In this case, simply think of each distinct data set as a group and apply the linear RESSD plot as for groups.

### Sample Plot
![](assets/EDA/linressd.gif)

This linear RESSD plot shows that the residual standard deviations from a linear fit are about 0.0025 for all the groups.

### Definition:
Group Residual Standard Deviation Versus Group ID

Linear RESSD plots are formed by:

	• Vertical axis: Group residual standard deviations from linear fits
	• Horizontal axis: Group identifier

A reference line is plotted at the residual standard deviation from a linear fit using all the data. This reference line will typically be much greater than any of the individual residual standard deviations.

### Questions
The linear RESSD plot can be used to answer the following questions.

	1. Is the residual standard deviation from a linear fit constant across groups?
	2. If the residual standard deviations vary, is there a discernible pattern across the groups?

### Importance: Checking Group Homogeneity
For grouped data, it may be important to know whether the different groups are homogeneous (i.e., similar) or heterogeneous (i.e., different). Linear RESSD plots help answer this question in the context of linear fitting.

### Related Techniques
* Linear Intercept Plot
* Linear Slope Plot
* Linear Correlation Plot
* Linear Fitting
