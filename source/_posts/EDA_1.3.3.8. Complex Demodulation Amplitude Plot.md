---
title: EDA_1.3.3.8. Complex Demodulation Amplitude Plot
date: 2018-03-02 16:26:12
categories: "statistics"
tags:
     - Complex Demodulation Amplitude Plot

description: EDA_1.3.3.8. Complex Demodulation Amplitude Plot
toc: true
---
### Purpose:
Detect Changing Amplitude in Sinusoidal Models

In the frequency analysis of time series models, a common model is the sinusoidal model:

	Yi=C+αsin(2πωti+ϕ)+Ei

In this equation, α is the amplitude, φ is the phase shift, and ω is the dominant frequency. In the above model, α and φ are constant, that is they do not vary with time, ti.

The complex demodulation amplitude plot (Granger, 1964) is used to determine if the assumption of constant amplitude is justifiable. If the slope of the complex demodulation amplitude plot is not zero, then the above model is typically replaced with the model:

	Yi=C+αisin(2πωti+ϕ)+Ei

where α^i is some type of linear model fit with standard least squares. The most common case is a linear fit, that is the model becomes

	Yi=C+(B0+B1∗ti)sin(2πωti+ϕ)+Ei

Quadratic models are sometimes used. Higher order models are relatively rare.

### Sample Plot:

![](assets/EDA/cdampplo.gif)

This complex demodulation amplitude plot shows that:
* the amplitude is fixed at approximately 390;
* there is a start-up effect; and
* there is a change in amplitude at around x = 160 that should be investigated for an outlier.

### Definition:
The complex demodulation amplitude plot is formed by:
* Vertical axis: Amplitude
* Horizontal axis: Time

The mathematical computations for determining the amplitude are beyond the scope of the Handbook. Consult Granger (Granger, 1964) for details.

### Questions
The complex demodulation amplitude plot answers the following questions:
	1. Does the amplitude change over time?
	2. Are there any outliers that need to be investigated?
	3. Is the amplitude different at the beginning of the series (i.e., is there a start-up effect)?

### Importance:
Assumption Checking

As stated previously, in the frequency analysis of time series models, a common model is the sinusoidal model:
	Yi=C+αsin(2πωti+ϕ)+Ei
In this equation, α is assumed to be constant, that is it does not vary with time. It is important to check whether or not this assumption is reasonable.

The complex demodulation amplitude plot can be used to verify this assumption. If the slope of this plot is essentially zero, then the assumption of constant amplitude is justified. If it is not, α should be replaced with some type of time-varying model. The most common cases are linear (B0 + B1*t) and quadratic (B0 + B1*t +B2*t2).

### Related Techniques
* Spectral Plot
* Complex Demodulation Phase Plot
* Non-Linear Fitting
