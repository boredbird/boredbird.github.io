---
title: EDA_1.3.3.13. DOE Standard Deviation Plot
date: 2018-03-02 19:26:12
categories: "statistics"
tags:
     - DOE Standard Deviation Plot

description: EDA_1.3.3.13. DOE Standard Deviation Plot
toc: true
---
### Purpose:
Detect Important Factors With Respect to Scale

The DOE standard deviation plot is appropriate for analyzing data from a designed experiment, with respect to important factors, where the factors are at two or more levels and there are repeated values at each level. The plot shows standard deviation values for the two or more levels of each factor plotted by factor. The standard deviations for a single factor are connected by a straight line. The DOE standard deviation plot is a complement to the traditional analysis of varianceof designed experiments.

This plot is typically generated for the standard deviation. However, it can also be generated for other scale statistics such as the range, the median absolute deviation, or the average absolute deviation.
### Sample Plot

![](assets/EDA/eda_dexboxbike_r03.gif)

This sample DOE standard deviation plot shows that:
	1. factor 1 has the greatest difference in standard deviations between factor levels;
	2. factor 4 has a significantly lower average standard deviation than the average standard deviations of other factors (but the level 1 standard deviation for factor 1 is about the same as the level 1 standard deviation for factor 4);
	3. for all factors, the level 1 standard deviation is smaller than the level 2 standard deviation.

### Definition:
Response Standard Deviations Versus Factor Variables

DOE standard deviation plots are formed by:
* Vertical axis: Standard deviation of the response variable for each level of the factor
* Horizontal axis: Factor variable

### Questions
The DOE standard deviation plot can be used to answer the following questions:
	1. How do the standard deviations vary across factors?
	2. How do the standard deviations vary within a factor?
	3. Which are the most important factors with respect to scale?
	4. What is the ranked list of the important factors with respect to scale?

### Importance:
Assess Variability

The goal with many designed experiments is to determine which factors are significant. This is usually determined from the means of the factor levels (which can be conveniently shown with a DOE mean plot). A secondary goal is to assess the variability of the responses both within a factor and between factors. The DOE standard deviation plot is a convenient way to do this.

### Related Techniques
* DOE scatter plot
* DOE mean plot
* Block plot
* Box plot
* Analysis of variance
