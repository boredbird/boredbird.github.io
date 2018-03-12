---
title: Exploratory Data Analysis(三)
date: 2018-03-02 12:26:12
categories: "statistics"
tags:
     - Comparative
     - Screening
     - Optimization
     - Regression
     - Time Series
     - Multivariate

description: Exploratory Data Analysis(三)
toc: true
---
## 1.3. EDA Techniques
After you have collected a set of data, how do you do an exploratory data analysis? What techniques do you employ? What do the various techniques focus on? What conclusions can you expect to reach?
This section provides answers to these kinds of questions via a gallery of EDA techniques and a detailed description of each technique. The techniques are divided into graphical and quantitative techniques. For exploratory data analysis, the emphasis is primarily on the graphical techniques.
### 1.3.1.Introduction
#### Graphical and Quantitative Techniques
This section describes many techniques that are commonly used in exploratory and classical data analysis. This list is by no means meant to be exhaustive. Additional techniques (both graphical and quantitative) are discussed in the other chapters. Specifically, the product comparisons chapter has a much more detailed description of many classical statistical techniques.
EDA emphasizes graphical techniques while classical techniques emphasize quantitative techniques. In practice, an analyst typically uses a mixture of graphical and quantitative techniques. In this section, we have divided the descriptions into graphical and quantitative techniques. This is for organizational clarity and is not meant to discourage the use of both graphical and quantitiative techniques when analyzing data.

#### Use of Techniques Shown in Case Studies
This section emphasizes the techniques themselves; how the graph or test is defined, published references, and sample output. The use of the techniques to answer engineering questions is demonstrated in the case studiessection. The case studies do not demonstrate all of the techniques.

#### Availability in Software
The sample plots and output in this section were generated with the Dataplot software program. Other general purpose statistical data analysis programs can generate most of the plots, intervals, and tests discussed here, or macros can be written to acheive the same result.

### 1.3.2.Analysis Questions
#### EDA Questions
Some common questions that exploratory data analysis is used to answer are:
	1. What is a typical value?
	2. What is the uncertainty for a typical value?
	3. What is a good distributional fit for a set of numbers?
	4. What is a percentile?
	5. Does an engineering modification have an effect?
	6. Does a factor have an effect?
	7. What are the most important factors?
	8. Are measurements coming from different laboratories equivalent?
	9. What is the best function for relating a response variable to a set of factor variables?
	10. What are the best settings for factors?
	11. Can we separate signal from noise in time dependent data?
	12. Can we extract any structure from multivariate data?
	13. Does the data have outliers?

#### Analyst Should Identify Relevant Questions for his Engineering Problem
A critical early step in any analysis is to identify (for the engineering problem at hand) which of the above questions are relevant. That is, we need to identify which questions we want answered and which questions have no bearing on the problem at hand. After collecting such a set of questions, an equally important step, which is invaluable for maintaining focus, is to prioritize those questions in decreasing order of importance. EDA techniques are tied in with each of the questions. There are some EDA techniques (e.g., the scatter plot) that are broad-brushed and apply almost universally. On the other hand, there are a large number of EDA techniques that are specific and whose specificity is tied in with one of the above questions. Clearly if one chooses not to explicitly identify relevant questions, then one cannot take advantage of these question-specific EDA technqiues.

#### EDA Approach Emphasizes Graphics
Most of these questions can be addressed by techniques discussed in this chapter. The process modeling and process improvement chapters also address many of the questions above. These questions are also relevant for the classical approach to statistics. What distinguishes the EDA approach is an emphasis on graphical techniques to gain insight as opposed to the classical approach of quantitative tests. Most data analysts will use a mix of graphical and classical quantitative techniques to address these problems.

### 1.3.3.Graphical Techniques: Alphabetic
#### 1.3.3.1. Autocorrelation Plot
##### Purpose: Check Randomness
Autocorrelation plots (Box and Jenkins, pp. 28-32) are a commonly-used tool for checking randomness in a data set. This randomness is ascertained by computing autocorrelations for data values at varying time lags. If random, such autocorrelations should be near zero for any and all time-lag separations. If non-random, then one or more of the autocorrelations will be significantly non-zero.
In addition, autocorrelation plots are used in the model identification stage for Box-Jenkinsautoregressive, moving average time series models.

##### Autocorrelation is Only One Measure of Randomness
Note that uncorrelated does not necessarily mean random. Data that has significant autocorrelation is not random. However, data that does not show significant autocorrelation can still exhibit non-randomness in other ways. Autocorrelation is just one measure of randomness. In the context of model validation (which is the primary type of randomness we dicuss in the Handbook), checking for autocorrelation is typically a sufficient test of randomness since the residuals from a poor fitting models tend to display non-subtle randomness. However, some applications require a more rigorous determination of randomness. In these cases, a battery of tests, which might include checking for autocorrelation, are applied since data can be non-random in many different and often subtle ways.
An example of where a more rigorous check for randomness is needed would be in testing random number generators.

##### Sample Plot:
Autocorrelations should be near-zero for randomness. Such is not the case in this example and thus the randomness assumption fails

![](assets/EDA/autocop0.gif)

This sample autocorrelation plot shows that the time series is not random, but rather has a high degree of autocorrelation between adjacent and near-adjacent observations.
##### Definition: r(h) versus h
```
Autocorrelation plots are formed by
	• Vertical axis: Autocorrelation coefficient
        Rh=Ch/C0
        where Ch is the autocovariance function
        Ch=1N∑t=1N−h(Yt−Y¯)(Yt+h−Y¯)
        and C0 is the variance function
        C0=∑Nt=1(Yt−Y¯)2N
        Note that Rh is between -1 and +1.
        Note that some sources may use the following formula for the autocovariance function
        Ch=1N−h∑t=1N−h(Yt−Y¯)(Yt+h−Y¯)
        Although this definition has less bias, the (1/N) formulation has some desirable statistical properties and is the form most commonly used in the statistics literature. See pages 20 and 49-50 in Chatfield for details.
	• Horizontal axis: Time lag h (h = 1, 2, 3, ...)
	• The above line also contains several horizontal reference lines. The middle line is at zero. The other four lines are 95 % and 99 % confidence bands. Note that there are two distinct formulas for generating the confidence bands.
		1. If the autocorrelation plot is being used to test for randomness (i.e., there is no time dependence in the data), the following formula is recommended:
        ±z1−α/2N−−√
        where N is the sample size, z is the cumulative distribution function of the standard normal distribution and αis the significance level. In this case, the confidence bands have fixed width that depends on the sample size. This is the formula that was used to generate the confidence bands in the above plot.
		2. Autocorrelation plots are also used in the model identification stage for fitting ARIMA models. In this case, a moving average model is assumed for the data and the following confidence bands should be generated:
        ±z1−α/21N(1+2∑i=1ky2i)−−−−−−−−−−−−−⎷
        where k is the lag, N is the sample size, z is the cumulative distribution function of the standard normal distribution and α is the significance level. In this case, the confidence bands increase as the lag increases.
```
##### Questions
The autocorrelation plot can provide answers to the following questions:
	1. Are the data random?
	2. Is an observation related to an adjacent observation?
	3. Is an observation related to an observation twice-removed? (etc.)
	4. Is the observed time series white noise?
	5. Is the observed time series sinusoidal?
	6. Is the observed time series autoregressive?
	7. What is an appropriate model for the observed time series?
	8. Is the model
        Y = constant + error
        valid and sufficient?
	9. Is the formula
        sY¯=s/N−−√
        valid?
##### Importance: 
Ensure validity of engineering conclusions

Randomness (along with fixed model, fixed variation, and fixed distribution) is one of the four assumptions that typically underlie all measurement processes. The randomness assumption is critically important for the following three reasons:

	1. Most standard statistical tests depend on randomness. The validity of the test conclusions is directly linked to the validity of the randomness assumption.
	2. Many commonly-used statistical formulae depend on the randomness assumption, the most common formula being the formula for determining the standard deviation of the sample mean:
    sY¯=s/N−−√
    where s is the standard deviation of the data. Although heavily used, the results from using this formula are of no value unless the randomness assumption holds.
	3. For univariate data, the default model is
    Y = constant + error
    If the data are not random, this model is incorrect and invalid, and the estimates for the parameters (such as the constant) become nonsensical and invalid.
    In short, if the analyst does not check for randomness, then the validity of many of the statistical conclusions becomes suspect. The autocorrelation plot is an excellent way of checking for such randomness.
