---
title: EDA_1.3.5.13. Runs Test for Detecting Non-randomness
date: 2018-03-12 17:02:12
categories: "statistics"
tags:
     - Runs Test for Detecting Non-randomness
description: EDA_1.3.5.13. Runs Test for Detecting Non-randomness
toc: true
---
### Purpose: Detect Non-Randomness
The runs test (Bradley, 1968) can be used to decide if a data set is from a random process.

A run is defined as a series of increasing values or a series of decreasing values. The number of increasing, or decreasing, values is the length of the run. In a random data set, the probability that the (I+1)th value is larger or smaller than the Ith value follows a binomial distribution, which forms the basis of the runs test.

### Typical Analysis and Test Statistics
The first step in the runs test is to count the number of runs in the data sequence. There are several ways to define runs in the literature, however, in all cases the formulation must produce a dichotomous sequence of values. For example, a series of 20 coin tosses might produce the following sequence of heads (H) and tails (T).

	H H T T H T H H H H T H H T T T T T H H

The number of runs for this series is nine. There are 11 heads and 9 tails in the sequence.

### Definition
We will code values above the median as positive and values below the median as negative. A run is defined as a series of consecutive positive (or negative) values. The runs test is defined as:

![](assets/EDA/eda35d_1.png)

### Runs Test Example
A runs test was performed for 200 measurements of beam deflection contained in the LEW.DAT data set.

![](assets/EDA/eda35d_2.png)

Since the test statistic is greater than the critical value, we conclude that the data are not random at the 0.05 significance level.

### Question
The runs test can be used to answer the following question:

	• Were these sample data generated from a random process?

### Importance
Randomness is one of the key assumptions in determining if a univariate statistical process is in control. If the assumptions of constant location and scale, randomness, and fixed distribution are reasonable, then the univariate process can be modeled as:

	Yi=A0+Ei

where Ei is an error term.

If the randomness assumption is not valid, then a different model needs to be used. This will typically be either a times series model or a non-linear model (with time as the independent variable).
### Related Techniques
* Autocorrelation
* Run Sequence Plot
* Lag Plot

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda35d.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda35d.htm)
