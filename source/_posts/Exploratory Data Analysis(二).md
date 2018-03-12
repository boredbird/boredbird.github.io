---
title: Exploratory Data Analysis(二)
date: 2018-03-02 11:26:12
categories: "statistics"
tags:
     - Comparative
     - Screening
     - Optimization
     - Regression
     - Time Series
     - Multivariate

description: Exploratory Data Analysis(二)
toc: true
---
## 1.2. EDA Assumptions
The gamut of scientific and engineering experimentation is virtually limitless. In this sea of diversity is there any common basis that allows the analyst to systematically and validly arrive at supportable, repeatable research conclusions?

Fortunately, there is such a basis and it is rooted in the fact that every measurement process, however complicated, has certain underlying assumptions. This section deals with what those assumptions are, why they are important, how to go about testing them, and what the consequences are if the assumptions do not hold.

### 1.2.1. Underlying Assumptions
#### Assumptions Underlying a Measurement Process
There are four assumptions that typically underlie all measurement processes; namely, that the data from the process at hand "behave like":

	1. random drawings;
	2. from a fixed distribution;
	3. with the distribution having fixed location; and
	4. with the distribution having fixed variation.

#### Univariate or Single Response Variable
The "fixed location" referred to in item 3 above differs for different problem types. The simplest problem type is univariate; that is, a single variable.

    For the univariate problem, the general model
    	response = deterministic component + random component
    becomes
    	response = constant + error

#### Assumptions for Univariate Model
For this case, the "fixed location" is simply the unknown constant. We can thus imagine the process at hand to be operating under constant conditions that produce a single column of data with the properties that

	• the data are uncorrelated with one another;
	• the random component has a fixed distribution;
	• the deterministic component consists of only a constant; and
	• the random component has fixed variation.
#### Extrapolation to a Function of Many Variables
The universal power and importance of the univariate model is that it can easily be extended to the more general case where the deterministic component is not just a constant, but is in fact a function of many variables, and the engineering objective is tocharacterize and model the function.
#### Residuals Will Behave According to Univariate Assumptions
The key point is that regardless of how many factors there are, and regardless of how complicated the function is, if the engineer succeeds in choosing a good model, then the differences (residuals) between the raw response data and the predicted values from the fitted model should themselves behave like a univariate process. Furthermore, the residuals from this univariate process fit will behave like:

	• random drawings;
	• from a fixed distribution;
	• with fixed location (namely, 0 in this case); and
	• with fixed variation.

#### Validation of Model
Thus if the residuals from the fitted model do in fact behave like the ideal, then testing of underlying assumptions becomes a tool for the validation and quality of fit of the chosen model. On the other hand, if the residuals from the chosen fitted model violate one or more of the above univariate assumptions, then the chosen fitted model is inadequate and an opportunity exists for arriving at an improved model.

### 1.2.2.Importance
#### Predictability and Statistical Control

Predictability is an all-important goal in science and engineering. If the four underlying assumptions hold, then we have achieved probabilistic predictability--the ability to make probability statements not only about the process in the past, but also about the process in the future. In short, such processes are said to be "in statistical control".

#### Validity of Engineering Conclusions

Moreover, if the four assumptions are valid, then the process is amenable to the generation of valid scientific and engineering conclusions. If the four assumptions are not valid, then the process is drifting (with respect to location, variation, or distribution), unpredictable, and out of control. A simple characterization of such processes by a location estimate, a variation estimate, or a distribution "estimate" inevitably leads to engineering conclusions that are not valid, are not supportable (scientifically or legally), and which are not repeatable in the laboratory.

### 1.2.3. Techniques for Testing Assumptions
#### Testing Underlying Assumptions Helps Assure the Validity of Scientific and Engineering Conclusions

Because the validity of the final scientific/engineering conclusions is inextricably linked to the validity of the underlying univariate assumptions, it naturally follows that there is a real necessity that each and every one of the above four assumptions be routinely tested.

#### Four Techniques to Test Underlying Assumptions

The following EDA techniques are simple, efficient, and powerful for the routine testing of underlying assumptions:

	1. run sequence plot (Yi versus i)
	2. lag plot (Yi versus Yi-1)
	3. histogram (counts versus subgroups of Y)
	4. normal probability plot (ordered Y versus theoretical ordered Y)

#### Plot on a Single Page for a Quick Characterization of the Data

The four EDA plots can be juxtaposed for a quick look at the characteristics of the data. The plots below are ordered as follows:

	1. Run sequence plot - upper left
	2. Lag plot - upper right
	3. Histogram - lower left
	4. Normal probability plot - lower right

#### Sample Plot: Assumptions Hold
![](assets/EDA/randn4p.gif)

This 4-plot reveals a process that has fixed location, fixed variation, is random, apparently has a fixed approximately normal distribution, and has no outliers.
#### Sample Plot: Assumptions Do Not Hold
If one or more of the four underlying assumptions do not hold, then it will show up in the various plots as demonstrated in the following example.

![](assets/EDA/lew4p.gif)

This 4-plot reveals a process that has fixed location, fixed variation, is non-random (oscillatory), has a non-normal, U-shaped distribution, and has several outliers.

### 1.2.4. Interpretation of 4-Plot
#### Interpretation of EDA Plots:
Flat and Equi-Banded, Random, Bell-Shaped, and Linear

The four EDA plots discussed on the previous page are used to test the underlying assumptions:

	1. Fixed Location:
        If the fixed location assumption holds, then the run sequence plot will be flat and non-drifting.
	2. Fixed Variation:
        If the fixed variation assumption holds, then the vertical spread in the run sequence plot will be the approximately the same over the entire horizontal axis.
	3. Randomness:
        If the randomness assumption holds, then the lag plot will be structureless and random.
	4. Fixed Distribution:
        If the fixed distribution assumption holds, in particular if the fixed normal distribution holds, then
        		1. the histogram will be bell-shaped, and
        		2. the normal probability plot will be linear.
#### Plots Utilized to Test the Assumptions
Conversely, the underlying assumptions are tested using the EDA plots:

* Run Sequence Plot:
    >If the run sequence plot is flat and non-drifting, the fixed-location assumption holds. If the run sequence plot has a vertical spread that is about the same over the entire plot, then the fixed-variation assumption holds.
* Lag Plot:
    >If the lag plot is structureless, then the randomness assumption holds.
* Histogram:
    >If the histogram is bell-shaped, the underlying distribution is symmetric and perhaps approximately normal.
* Normal Probability Plot:
    >If the normal probability plot is linear, the underlying distribution is approximately normal.
    If all four of the assumptions hold, then the process is said definitionally to be "in statistical control".

### 1.2.5 Consequences

#### What If Assumptions Do Not Hold?

If some of the underlying assumptions do not hold, what can be done about it? What corrective actions can be taken? The positive way of approaching this is to view the testing of underlying assumptions as a framework for learning about the process. Assumption-testing promotes insight into important aspects of the process that may not have surfaced otherwise.

#### Primary Goal is Correct and Valid Scientific Conclusions

The primary goal is to have correct, validated, and complete scientific/engineering conclusions flowing from the analysis. This usually includes intermediate goals such as the derivation of a good-fitting model and the computation of realistic parameter estimates. It should always include the ultimate goal of an understanding and a "feel" for "what makes the process tick". There is no more powerful catalyst for discovery than the bringing together of an experienced/expert scientist/engineer and a data set ripe with intriguing "anomalies" and characteristics.

#### Consequences of Invalid Assumptions

The following sections discuss in more detail the consequences of invalid assumptions:
	1. Consequences of non-randomness
	2. Consequences of non-fixed location parameter
	3. Consequences of non-fixed variation
	4. Consequences related to distributional assumptions

#### 1.2.5.1.	Consequences of Non-Randomness
##### Randomness Assumption

There are four underlying assumptions:
	1. randomness;
	2. fixed location;
	3. fixed variation; and
	4. fixed distribution.
The randomness assumption is the most critical but the least tested.

##### Consequeces of Non-Randomness

If the randomness assumption does not hold, then
	1. All of the usual statistical tests are invalid.
	2. The calculated uncertainties for commonly used statistics become meaningless.
	3. The calculated minimal sample size required for a pre-specified tolerance becomes meaningless.
	4. The simple model: y = constant + error becomes invalid.
	5. The parameter estimates become suspect and non-supportable.

##### Non-Randomness Due to Autocorrelation

One specific and common type of non-randomness is autocorrelation. Autocorrelation is the correlation between Ytand Yt-k, where k is an integer that defines the lag for the autocorrelation. That is, autocorrelation is a time dependent non-randomness. This means that the value of the current point is highly dependent on the previous point if k = 1 (or k points ago if kis not 1). Autocorrelation is typically detected via an autocorrelation plot or a lag plot.
If the data are not random due to autocorrelation, then
	1. Adjacent data values may be related.
	2. There may not be n independent snapshots of the phenomenon under study.
	3. There may be undetected "junk"-outliers.
	4. There may be undetected "information-rich"-outliers.

#### 1.2.5.2.	Consequences of Non-Fixed Location Parameter
##### Location Estimate

The usual estimate of location is the mean
	Y¯=1N∑i=1NYi
from N measurements Y1, Y2, ... , YN.

##### Consequences of Non-Fixed Location

If the run sequence plot does not support the assumption of fixed location, then
	1. The location may be drifting.
	2. The single location estimate may be meaningless (if the process is drifting).
	3. The choice of location estimator (e.g., the sample mean) may be sub-optimal.
	4. The usual formula for the uncertainty of the mean:
s(Y¯)=1N(N−1)−−−−−−−−√∑i=1N(Yi−Y¯)2−−−−−−−−−−−⎷
may be invalid and the numerical value optimistically small.
	5. The location estimate may be poor.
	6. The location estimate may be biased.

#### 1.2.5.3.	Consequences of Non-Fixed Variation Parameter
##### Variation Estimate

The usual estimate of variation is the standard deviation
	sY=1(N−1)−−−−−−−√∑i=1N(Yi−Y¯)2−−−−−−−−−−−⎷
from N measurements Y1, Y2, ... , YN.

##### Consequences of Non-Fixed Variation

If the run sequence plot does not support the assumption of fixed variation, then
	1. The variation may be drifting.
	2. The single variation estimate may be meaningless (if the process variation is drifting).
	3. The variation estimate may be poor.
	4. The variation estimate may be biased.

#### 1.2.5.4. Consequences Related to Distributional Assumptions
##### Distributional Analysis
Scientists and engineers routinely use the mean (average) to estimate the "middle" of a distribution. It is not so well known that the variability and the noisiness of the mean as a location estimator are intrinsically linked with the underlying distribution of the data. For certain distributions, the mean is a poor choice. For any given distribution, there exists an optimal choice-- that is, the estimator with minimum variability/noisiness. This optimal choice may be, for example, the median, the midrange, the midmean, the mean, or something else. The implication of this is to "estimate" the distribution first, and then--based on the distribution--choose the optimal estimator. The resulting engineering parameter estimators will have less variability than if this approach is not followed.
##### Case Studies
The airplane glass failure case study gives an example of determining an appropriate distribution and estimating the parameters of that distribution. The uniform random numberscase study gives an example of determining a more appropriate centrality parameter for a non-normal distribution.

Other consequences that flow from problems with distributional assumptions are:
##### Distribution
	1. The distribution may be changing.
	2. The single distribution estimate may be meaningless (if the process distribution is changing).
	3. The distribution may be markedly non-normal.
	4. The distribution may be unknown.
	5. The true probability distribution for the error may remain unknown.
##### Model
	1. The model may be changing.
	2. The single model estimate may be meaningless.
	3. The default model
        Y = constant + error
        may be invalid.
	4. If the default model is insufficient, information about a better model may remain undetected.
	5. A poor deterministic model may be fit.
	6. Information about an improved model may go undetected.
##### Process
	1. The process may be out-of-control.
	2. The process may be unpredictable.
	3. The process may be un-modelable.
