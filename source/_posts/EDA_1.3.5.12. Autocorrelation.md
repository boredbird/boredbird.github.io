---
title: EDA_1.3.5.12. Autocorrelation
date: 2018-03-12 17:02:12
categories: "statistics"
tags:
     - Autocorrelation
description: EDA_1.3.5.12. Autocorrelation
toc: true
---
### Purpose: Detect Non-Randomness, Time Series Modeling
The autocorrelation ( Box and Jenkins, 1976) function can be used for the following two purposes:

	1. To detect non-randomness in data.
	2. To identify an appropriate time series model if the data are not random.

### Definition
Given measurements, Y1, Y2, ..., YN at timeX1, X2, ..., XN, the lag k autocorrelation function is defined as

	rk=∑N−ki=1(Yi−Y¯)(Yi+k−Y¯)∑Ni=1(Yi−Y¯)2

Although the time variable, X, is not used in the formula for autocorrelation, the assumption is that the observations are equi-spaced.

Autocorrelation is a correlation coefficient. However, instead of correlation between two different variables, the correlation is between two values of the same variable at times Xi and Xi+k.
When the autocorrelation is used to detect non-randomness, it is usually only the first (lag 1) autocorrelation that is of interest. When the autocorrelation is used to identify an appropriate time series model, the autocorrelations are usually plotted for many lags.

### Autocorrelation Example
Lag-one autocorrelations were computed for the the LEW.DAT data set.

     lag     autocorrelation
      0.      1.00
      1.     -0.31
      2.     -0.74
      3.      0.77
      4.      0.21
      5.     -0.90
      6.      0.38
      7.      0.63
      8.     -0.77
      9.     -0.12
     10.      0.82
     11.     -0.40
     12.     -0.55
     13.      0.73
     14.      0.07
     15.     -0.76
     16.      0.40
     17.      0.48
     18.     -0.70
     19.     -0.03
     20.      0.70
     21.     -0.41
     22.     -0.43
     23.      0.67
     24.      0.00
     25.     -0.66
     26.      0.42
     27.      0.39
     28.     -0.65
     29.      0.03
     30.      0.63
     31.     -0.42
     32.     -0.36
     33.      0.64
     34.     -0.05
     35.     -0.60
     36.      0.43
     37.      0.32
     38.     -0.64
     39.      0.08
     40.      0.58
     41.     -0.45
     42.     -0.28
     43.      0.62
     44.     -0.10
     45.     -0.55
     46.      0.45
     47.      0.25
     48.     -0.61
     49.      0.14

### Questions
The autocorrelation function can be used to answer the following questions.

	1. Was this sample data set generated from a random process?
	2. Would a non-linear or time series model be a more appropriate model for these data than a simple constant plus error model?

### Importance
Randomness is one of the key assumptions in determining if a univariate statistical process is in control. If the assumptions of constant location and scale, randomness, and fixed distribution are reasonable, then the univariate process can be modeled as:

	Yi=A0+Ei

where Ei is an error term.

If the randomness assumption is not valid, then a different model needs to be used. This will typically be either a time series modelor a non-linear model (with time as the independent variable).
### Related Techniques
* Autocorrelation Plot
* Run Sequence Plot
* Lag Plot
* Runs Test