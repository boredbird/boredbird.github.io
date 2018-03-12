---
title: EDA_1.3.5.18. Yates Algorithm
date: 2018-03-12 17:07:12
categories: "statistics"
tags:
     - Yates Algorithm
description: EDA_1.3.5.18. Yates Algorithm
toc: true
---
### Purpose: Estimate Factor Effects in a 2-Level Factorial Design
Full factorial and fractional factorial designs are common in designed experiments for engineering and scientific applications.

In these designs, each factor is assigned two levels. These are typically called the low and high levels. For computational purposes, the factors are scaled so that the low level is assigned a value of -1 and the high level is assigned a value of +1. These are also commonly referred to as "-" and "+".

A full factorial design contains all possible combinations of low/high levels for all the factors. A fractional factorial design contains a carefully chosen subset of these combinations. The criterion for choosing the subsets is discussed in detail in the process improvement chapter.

The Yates algorithm exploits the special structure of these designs to generate least squares estimates for factor effects for all factors and all relevant interactions.

The mathematical details of the Yates algorithm are given in chapter 10 of Box, Hunter, and Hunter (1978). Natrella (1963) also provides a procedure for testing the significance of effect estimates.
The effect estimates are typically complemented by a number of graphical techniques such as theDOE mean plot and the DOE contour plot ("DOE" represents "design of experiments"). These are demonstrated in the eddy current case study.

### Yates Order
Before performing the Yates algorithm, the data should be arranged in "Yates order". That is, given k factors, the kth column consists of 2k-1minus signs (i.e., the low level of the factor) followed by 2k-1 plus signs (i.e., the high level of the factor). For example, for a full factorial design with three factors, the design matrix is

    - - -
    + - -
    - + -
    + + -
    - - +
    + - +
    - + +
    + + +

Determining the Yates order for fractional factorial designs requires knowledge of theconfounding structure of the fractional factorial design.

### Yates Algorithm
The Yates algorithm is demonstrated for the eddy current data set. The data set contains eight measurements from a two-level, full factorial design with three factors. The purpose of the experiment is to identify factors that have the most effect on eddy current measurements.

In the "Effect" column, we list the main effects and interactions from our factorial experiment in standard order. In the "Response" column, we list the measurement results from our experiment in Yates order.

    Effect    Response  Col 1    Col 2    Col 3  Estimate
    ------    --------  -----    -----    -----  --------
    Mean       1.70      6.27    10.21    21.27   2.65875
    X1         4.57      3.94    11.06    12.41   1.55125
    X2         0.55      6.10     5.71    -3.47  -0.43375
    X1*X2      3.39      4.96     6.70     0.51   0.06375
    X3         1.51      2.87    -2.33     0.85   0.10625
    X1*X3      4.59      2.84    -1.14     0.99   0.12375
    X2*X3      0.67      3.08    -0.03     1.19   0.14875
    X1*X2*X3   4.29      3.62     0.54     0.57   0.07125
    Sum of responses:           21.27			
    Sum-of-squared responses:   77.7707
    Sum-of-squared Col 3:      622.1656

The first four values in Col 1 are obtained by adding adjacent pairs of responses, for example 4.57 + 1.70 = 6.27, and 3.39 + 0.55 = 3.94. The second four values in Col 1 are obtained by subtracting the same adjacent pairs of responses, for example, 4.57 - 1.70 = 2.87, and 3.39 - 0.55 = 2.84. The values in Col 2 are calculated in the same way, except that we are adding and subtracting adjacent values from Col 1. Col 3 is computed using adjacent values from Col 2. Finally, we obtain the "Estimate" column by dividing the values in Col 3 by the total number of responses, 8.
We can check our calculations by making sure that the first value in Col 3 (21.27) is the sum of all the responses. In addition, the sum-of-squared responses (77.7707) should equal the sum-of-squared Col 3 values divided by 8 (622.1656/8 = 77.7707).

### Practical Considerations
The Yates algorithm provides a convenient method for computing effect estimates; however, the same information is easily obtained from statistical software using either an analysis of variance or regression procedure. The methods for analyzing data from a designed experiment are discussed more fully in the chapter on Process Improvement.

### Graphical Presentation
The following plots may be useful to complement the quantitative information from the Yates algorithm.

	1. Ordered data plot
	2. Ordered absolute effects plot
	3. Cumulative residual standard deviation plot

### Questions
The Yates algorithm can be used to answer the following question.

	1. What is the estimated effect of a factor on the response?

### Related Techniques
* Multi-factor analysis of variance
* DOE mean plot
* Block plot
* DOE contour plot

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda35i.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda35i.htm)
