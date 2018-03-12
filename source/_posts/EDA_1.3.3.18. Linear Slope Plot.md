---
title: EDA_1.3.3.18. Linear Slope Plot
date: 2018-03-12 13:26:12
categories: "statistics"
tags:
     - Linear Slope Plot
description: EDA_1.3.3.18. Linear Slope Plot
toc: true
---
### Purpose: Detect changes in linear slopes between groups
Linear slope plots are used to graphically assess whether or not linear fits are consistent across groups. That is, if your data have groups, you may want to know if a single fit can be used across all the groups or whether separate fits are required for each group.

Linear slope plots are typically used in conjunction with linear intercept and linear residual standard deviation plots.

In some cases you might not have groups. Instead, you have different data sets and you want to know if the same fit can be adequately applied to each of the data sets. In this case, simply think of each distinct data set as a group and apply the linear slope plot as for groups.

### Sample Plot
![](assets/EDA/linslopl.gif)

This linear slope plot shows that the slopes are about 0.174 (plus or minus 0.002) for all groups. There does not appear to be a pattern in the variation of the slopes. This implies that a single fit may be adequate.

### Definition:
Group Slopes Versus Group ID

Linear slope plots are formed by:

	• Vertical axis: Group slopes from linear fits
	• Horizontal axis: Group identifier

A reference line is plotted at the slope from a linear fit using all the data.

### Questions
The linear slope plot can be used to answer the following questions.

	1. Do you get the same slope across groups for linear fits?
	2. If the slopes differ, is there a discernible pattern in the slopes?

### Importance: Checking Group Homogeneity
For grouped data, it may be important to know whether the different groups are homogeneous (i.e., similar) or heterogeneous (i.e., different). Linear slope plots help answer this question in the context of linear fitting.

### Related Techniques
* Linear Intercept Plot
* Linear Correlation Plot
* Linear Residual Standard Deviation Plot 
* Linear Fitting
