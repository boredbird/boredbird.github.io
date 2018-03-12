---
title: EDA_1.3.3.9. Complex Demodulation Phase Plot
date: 2018-03-02 16:26:12
categories: "statistics"
tags:
     - Complex Demodulation Phase Plot

description: EDA_1.3.3.9. Complex Demodulation Phase Plot
toc: true
---
### Purpose:
Improve the estimate of frequency in sinusoidal time series models
As stated previously, in the frequency analysis of time series models, a common model is the sinusoidal model:

	Yi=C+αsin(2πωti+ϕ)+Ei

In this equation, α is the amplitude, φ is the phase shift, and ω is the dominant frequency. In the above model, α and φ are constant, that is they do not vary with time ti.
The complex demodulation phase plot (Granger, 1964) is used to improve the estimate of the frequency (i.e., ω) in this model.

If the complex demodulation phase plot shows lines sloping from left to right, then the estimate of the frequency should be increased. If it shows lines sloping right to left, then the frequency should be decreased. If there is essentially zero slope, then the frequency estimate does not need to be modified.

### Sample Plot:
![](assets/EDA/cdphasep.gif)

This complex demodulation phase plot shows that:
* the specified demodulation frequency is incorrect;
* the demodulation frequency should be increased.

### Definition
The complex demodulation phase plot is formed by:
* Vertical axis: Phase
* Horizontal axis: Time

The mathematical computations for the phase plot are beyond the scope of the Handbook. Consult Granger (Granger, 1964) for details.

### Questions
The complex demodulation phase plot answers the following question:

	Is the specified demodulation frequency correct?

### Importance of a Good Initial Estimate for the Frequency
The non-linear fitting for the sinusoidal model:

	Yi=C+αsin(2πωti+ϕ)+Ei

is usually quite sensitive to the choice of good starting values. The initial estimate of the frequency, ω, is obtained from a spectral plot. The complex demodulation phase plot is used to assess whether this estimate is adequate, and if it is not, whether it should be increased or decreased. Using the complex demodulation phase plot with the spectral plot can significantly improve the quality of the non-linear fits obtained.

### Related Techniques
* Spectral Plot
* Complex Demodulation Phase Plot
* Non-Linear Fitting
