---
title: EDA_1.3.3.31. Youden Plot
date: 2018-03-12 15:56:12
categories: "statistics"
tags:
     - Youden Plot
description: EDA_1.3.3.31. Youden Plot
toc: true
---
### Purpose: Interlab Comparisons
Youden plots are a graphical technique for analyzing interlab data when each lab has made two runs on the same product or one run on two different products.
The Youden plot is a simple but effective method for comparing both the within-laboratory variability and the between-laboratory variability.
### Sample Plot
![](assets/EDA/youdenpl.gif)

This plot shows:

	1. Not all labs are equivalent.
	2. Lab 4 is biased low.
	3. Lab 3 has within-lab variability problems.
	4. Lab 5 has an outlying run.

### Definition:
Response 1 Versus Response 2 Coded by Lab

Youden plots are formed by:

	1. Vertical axis: Response variable 1 (i.e., run 1 or product 1 response value)
	2. Horizontal axis: Response variable 2 (i.e., run 2 or product 2 response value)

In addition, the plot symbol is the lab id (typically an integer from 1 to k where k is the number of labs). Sometimes a 45-degree reference line is drawn. Ideally, a lab generating two runs of the same product should produce reasonably similar results. Departures from this reference line indicate inconsistency from the lab. If two different products are being tested, then a 45-degree line may not be appropriate. However, if the labs are consistent, the points should lie near some fitted straight line.

### Questions
The Youden plot can be used to answer the following questions:

	1. Are all labs equivalent?
	2. What labs have between-lab problems (reproducibility)?
	3. What labs have within-lab problems (repeatability)?
	4. What labs are outliers?

### Importance
In interlaboratory studies or in comparing two runs from the same lab, it is useful to know if consistent results are generated. Youden plots should be a routine plot for analyzing this type of data.

DOE Youden Plot

The DOE Youden plot is a specialized Youden plot used in the design of experiments. In particular, it is useful for full and fractional designs.
### Related Techniques
Scatter Plot
