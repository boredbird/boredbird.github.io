---
title: EDA_1.3.3.17. Linear Intercept Plot
date: 2018-03-12 12:26:12
categories: "statistics"
tags:
     - Linear Intercept Plot
description: EDA_1.3.3.17. Linear Intercept Plot
toc: true
---
### Purpose: Detect changes in linear intercepts between groups
Linear intercept plots are used to graphically assess whether or not linear fits are consistent across groups. That is, if your data have groups, you may want to know if a single fit can be used across all the groups or whether separate fits are required for each group.

Linear intercept plots are typically used in conjunction with linear slope and linear residual standard deviation plots.

In some cases you might not have groups. Instead, you have different data sets and you want to know if the same fit can be adequately applied to each of the data sets. In this case, simply think of each distinct data set as a group and apply the linear intercept plot as for groups.

### Sample Plot
![](assets/EDA/linintpl.gif)

This linear intercept plot shows that there is a shift in intercepts. Specifically, the first three intercepts are lower than the intercepts for the other groups. Note that these are small differences in the intercepts.

### Definition:
Group Intercepts Versus Group ID

Linear intercept plots are formed by:

	• Vertical axis: Group intercepts from linear fits
	• Horizontal axis: Group identifier

A reference line is plotted at the intercept from a linear fit using all the data.

### Questions
The linear intercept plot can be used to answer the following questions.
	1. Is the intercept from linear fits relatively constant across groups?
	2. If the intercepts vary across groups, is there a discernible pattern?

### Importance:Checking Group Homogeneity
For grouped data, it may be important to know whether the different groups are homogeneous (i.e., similar) or heterogeneous (i.e., different). Linear intercept plots help answer this question in the context of linear fitting.

### Related Techniques
* Linear Correlation Plot
* Linear Slope Plot
* Linear Residual Standard Deviation Plot 
* Linear Fitting
