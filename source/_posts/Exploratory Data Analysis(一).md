---
title: Exploratory Data Analysis(一)
date: 2018-03-02 10:26:12
categories: "statistics"
tags:
     - Comparative  
     - Screening
     - Optimization
     - Regression
     - Time Series
     - Multivariate

description: Exploratory Data Analysis(一)
toc: true
---
# 1. Exploratory Data Analysis
This chapter presents the assumptions, principles, and techniques necessary to gain insight into data via EDA--exploratory data analysis.
## 1.1. EDA Introduction
What is exploratory data analysis? How did it begin? How and where did it originate? How is it differentiated from other data analysis approaches, such as classical and Bayesian? Is EDA the same as statistical graphics? What role does statistical graphics play in EDA? Is statistical graphics identical to EDA?
These questions and related questions are dealt with in this section. This section answers these questions and provides the necessary frame of reference for EDA assumptions, principles, and techniques.
### 1.1.1. What is EDA?
#### Approach
Exploratory Data Analysis (EDA) is an approach/philosophy for data analysis that employs a variety of techniques (mostly graphical) to
>1. maximize insight into a data set;
2. uncover underlying structure;
3. extract important variables;
4. detect outliers and anomalies;
5. test underlying assumptions;
6. develop parsimonious models; and
7. determine optimal factor settings.

#### Focus
The EDA approach is precisely that--an approach--not a set of techniques, but an attitude/philosophy about how a data analysis should be carried out.
#### Philosophy
EDA is not identical to statistical graphics although the two terms are used almost interchangeably. Statistical graphics is a collection of techniques--all graphically based and all focusing on one data characterization aspect. EDA encompasses a larger venue; EDA is an approach to data analysis that postpones the usual assumptions about what kind of model the data follow with the more direct approach of allowing the data itself to reveal its underlying structure and model. EDA is not a mere collection of techniques; EDA is a philosophy as to how we dissect a data set; what we look for; how we look; and how we interpret. It is true that EDA heavily uses the collection of techniques that we call "statistical graphics", but it is not identical to statistical graphics per se.
#### History
The seminal work in EDA is Exploratory Data Analysis, Tukey, (1977). Over the years it has benefitted from other noteworthy publications such as Data Analysis and Regression, Mosteller and Tukey (1977), Interactive Data Analysis, Hoaglin (1977), The ABC's of EDA, Velleman and Hoaglin (1981) and has gained a large following as "the" way to analyze a data set.
#### Techniques
Most EDA techniques are graphical in nature with a few quantitative techniques. The reason for the heavy reliance on graphics is that by its very nature the main role of EDA is to open-mindedly explore, and graphics gives the analysts unparalleled power to do so, enticing the data to reveal its structural secrets, and being always ready to gain some new, often unsuspected, insight into the data. In combination with the natural pattern-recognition capabilities that we all possess, graphics provides, of course, unparalleled power to carry this out.
The particular graphical techniques employed in EDA are often quite simple, consisting of various techniques of:
> 1. Plotting the raw data (such as data traces,histograms, bihistograms, probability plots,lag plots, block plots, and Youden plots.
2. Plotting simple statistics such as mean plots, standard deviation plots, box plots, and main effects plots of the raw data.
3. Positioning such plots so as to maximize our natural pattern-recognition abilities, such as using multiple plots per page.

### 1.1.2. How Does Exploratory Data Analysis differ from Classical Data Analysis?
#### Data Analysis Approaches
EDA is a data analysis approach. What other data analysis approaches exist and how does EDA differ from these other approaches?

Three popular data analysis approaches are:
> 1. Classical
2. Exploratory (EDA)
3. Bayesian

#### Paradigms for Analysis Techniques
These three approaches are similar in that they all start with a general science/engineering problem and all yield science/engineering conclusions. The difference is the sequence and focus of the intermediate steps.
* For classical analysis, the sequence is
        Problem => Data => Model => Analysis => Conclusions
* For EDA, the sequence is
        Problem => Data => Analysis => Model => Conclusions
* For Bayesian, the sequence is
        Problem => Data => Model => Prior Distribution => Analysis => Conclusions

#### Method of dealing with underlying model for the data distinguishes the 3 approaches
Thus for classical analysis, the data collection is followed by the imposition of a model (normality, linearity, etc.) and the analysis, estimation, and testing that follows are focused on the parameters of that model.

For EDA, the data collection is not followed by a model imposition; rather it is followed immediately by analysis with a goal of inferring what model would be appropriate.

Finally, for a Bayesian analysis, the analyst attempts to incorporate scientific/engineering knowledge/expertise into the analysis by imposing a data-independent distribution on the parameters of the selected model; the analysis thus consists of formally combining both the prior distribution on the parameters and the collected data to jointly make inferences and/or test assumptions about the model parameters.

In the real world, data analysts freely mix elements of all of the above three approaches (and other approaches). The above distinctions were made to emphasize the major differences among the three approaches.

Further discussion of the distinction between the classical and EDA approaches	Focusing on EDA versus classical, these two approaches differ as follows:
>1. Models
2. Focus
3. Techniques
4. Rigor
5. Data Treatment
6. Assumptions

### 1.1.3 How Does Exploratory Data Analysis Differ from Summary Analysis?
#### Summary
A summary analysis is simply a numeric reduction of a historical data set. It is quite passive. Its focus is in the past. Quite commonly, its purpose is to simply arrive at a few key statistics (for example, mean and standard deviation) which may then either replace the data set or be added to the data set in the form of a summary table.
#### Exploratory
In contrast, EDA has as its broadest goal the desire to gain insight into the engineering/scientific process behind the data. Whereas summary statistics are passive and historical, EDA is active and futuristic. In an attempt to "understand" the process and improve it in the future, EDA uses the data as a "window" to peer into the heart of the process that generated the data. There is an archival role in the research and manufacturing world for summary statistics, but there is an enormously larger role for the EDA approach.

### 1.1.4. What are the EDA Goals?
#### Primary and Secondary Goals
The primary goal of EDA is to maximize the analyst's insight into a data set and into the underlying structure of a data set, while providing all of the specific items that an analyst would want to extract from a data set, such as:

    1. a good-fitting, parsimonious model
    2. a list of outliers
    3. a sense of robustness of conclusions
    4. estimates for parameters
    5. uncertainties for those estimates
    6. a ranked list of important factors
    7. conclusions as to whether individual factors are statistically significant
    8. optimal settings

#### Insight into the Data
Insight implies detecting and uncovering underlying structure in the data. Such underlying structure may not be encapsulated in the list of items above; such items serve as the specific targets of an analysis, but the real insight and "feel" for a data set comes as the analyst judiciously probes and explores the various subtleties of the data. The "feel" for the data comes almost exclusively from the application of various graphical techniques, the collection of which serves as the window into the essence of the data. Graphics are irreplaceable--there are no quantitative analogues that will give the same insight as well-chosen graphics.

To get a "feel" for the data, it is not enough for the analyst to know what is in the data; the analyst also must know what is not in the data, and the only way to do that is to draw on our own human pattern-recognition and comparative abilities in the context of a series of judicious graphical techniques applied to the data.

### 1.1.5.The Role of Graphics
#### Graphical
Statistics and data analysis procedures can broadly be split into two parts:
 1. quantitative
 2. graphical

#### Quantitative
Quantitative techniques are the set of statistical procedures that yield numeric or tabular output. Examples of quantitative techniques include:

1. hypothesis testing
2. analysis of variance
3. point estimates and confidence intervals
4. least squares regression

These and similar techniques are all valuable and are mainstream in terms of classical analysis.
#### Graphical
On the other hand, there is a large collection of statistical tools that we generally refer to as graphical techniques. These include:
* scatter plots
* histograms
* probability plots
* residual plots
* box plots
* block plots

#### EDA Approach Relies Heavily on Graphical Techniques
The EDA approach relies heavily on these and similar graphical techniques. Graphical procedures are not just tools that we could use in an EDA context, they are tools that we must use. Such graphical tools are the shortest path to gaining insight into a data set in terms of
* testing assumptions
* model selection
* model validation
* estimator selection
* relationship identification
* factor effect determination
* outlier detection

If one is not using statistical graphics, then one is forfeiting insight into one or more aspects of the underlying structure of the data.

### 1.1.6. An EDA/Graphics Example
#### Anscombe Example
A simple, classic (Anscombe) example of the central role that graphics play in terms of providing insight into a data set starts with the following data set:

`Data`

X|Y
-----|-------------
10.00|           8.04
 8.00|           6.95
13.00|          7.58
 9.00|           8.81
11.00|           8.33
14.00|           9.96
 6.00|          7.24
 4.00|           4.26
12.00|          10.84
 7.00|           4.82
 5.00|           5.68
#### Summary Statistics
If the goal of the analysis is to compute summary statistics plus determine the best linear fit for Y as a function of X, the results might be given as:

    N = 11
    Mean of X = 9.0
    Mean of Y = 7.5
    Intercept = 3
    Slope = 0.5
    Residual standard deviation = 1.237
    Correlation = 0.816

The above quantitative analysis, although valuable, gives us only limited insight into the data.
#### Scatter Plot
In contrast, the following simple scatter plotof the data

![](assets/EDA/anscomb1.gif)

suggests the following:

* 1. The data set "behaves like" a linear curve with some scatter;
* 2. there is no justification for a more complicated model (e.g., quadratic);
* 3. there are no outliers;
* 4. the vertical spread of the data appears to be of equal height irrespective of the X-value; this indicates that the data are equally-precise throughout and so a "regular" (that is, equi-weighted) fit is appropriate.

#### Three Additional Data Sets
This kind of characterization for the data serves as the core for getting insight/feel for the data. Such insight/feel does not come from the quantitative statistics; on the contrary, calculations of quantitative statistics such as intercept and slope should be subsequent to the characterization and will make sense only if the characterization is true. To illustrate the loss of information that results when the graphics insight step is skipped, consider the following three data sets [Anscombe data sets 2, 3, and 4]:

X2|Y2|X3|Y3|X4|Y4
-----|----|-----|-----|-----|-----
10.00|9.14|10.00| 7.46| 8.00| 6.58
 8.00|8.14| 8.00| 6.77| 8.00| 5.76
13.00|8.74|13.00|12.74| 8.00| 7.71
 9.00|8.77| 9.00| 7.11| 8.00| 8.84
11.00|9.26|11.00| 7.81| 8.00| 8.47
14.00|8.10|14.00| 8.84| 8.00| 7.04
 6.00|6.13| 6.00| 6.08| 8.00| 5.25
 4.00|3.10| 4.00| 5.39|19.00|12.50
12.00|9.13|12.00| 8.15| 8.00| 5.56
 7.00|7.26| 7.00| 6.42| 8.00| 7.91
 5.00|4.74| 5.00| 5.73| 8.00| 6.89
##### Quantitative Statistics for Data Set 2
 A quantitative analysis on data set 2 yields

 	N = 11
 	Mean of X = 9.0
 	Mean of Y = 7.5
 	Intercept = 3
 	Slope = 0.5
 	Residual standard deviation = 1.237
 	Correlation = 0.816

 which is identical to the analysis for data set 1. One might naively assume that the two data sets are "equivalent" since that is what the statistics tell us; but what do the statistics not tell us?

##### Quantitative Statistics for Data Sets 3 and 4
 Remarkably, a quantitative analysis on data sets 3 and 4 also yields

 	N = 11
 	Mean of X = 9.0
 	Mean of Y = 7.5
 	Intercept = 3
 	Slope = 0.5
 	Residual standard deviation = 1.236
 	Correlation = 0.816 (0.817 for data set 4)

 which implies that in some quantitative sense, all four of the data sets are "equivalent". In fact, the four data sets are far from "equivalent" and a scatter plot of each data set, which would be step 1 of any EDA approach, would tell us that immediately.

##### Scatter Plots
![](assets/EDA/anscomb4.gif)
###### Interpretation of Scatter Plots
Conclusions from the scatter plots are:

> 1. data set 1 is clearly linear with some scatter.
2. data set 2 is clearly quadratic.
3. data set 3 clearly has an outlier.
4. data set 4 is obviously the victim of a poor experimental design with a single point far removed from the bulk of the data "wagging the dog".

###### Importance of Exploratory Analysis
These points are exactly the substance that provide and define "insight" and "feel" for a data set. They are the goals and the fruits of an open exploratory data analysis (EDA) approach to the data.

 Quantitative statistics are not wrong per se, but they are incomplete. They are incomplete because they are numericsummaries which in the summarization operation do a good job of focusing on a particular aspect of the data (e.g., location, intercept, slope, degree of relatedness, etc.) by judiciously reducing the data to a few numbers. Doing so also filters the data, necessarily omitting and screening out other sometimes crucial information in the focusing operation. Quantitative statistics focus but also filter; and filtering is exactly what makes the quantitative approach incomplete at best and misleading at worst.

The estimated intercepts (= 3) and slopes (= 0.5) for data sets 2, 3, and 4 are misleading because the estimation is done in the context of an assumed linear model and that linearity assumption is the fatal flaw in this analysis.

The EDA approach of deliberately postponing the model selection until further along in the analysis has many rewards, not the least of which is the ultimate convergence to a much-improved model and the formulation of valid and supportable scientific and engineering conclusions.

### 1.1.7.General Problem Categories
#### Problem Classification
The following table is a convenient way to classify EDA problems.
##### Univariate and Control
###### UNIVARIATE
    Data:
    	A single column of numbers, Y.
    Model:
    	y = constant + error
    Output:
    	1. A number (the estimated constant in the model).
    	2. An estimate of uncertainty for the constant.
    	3. An estimate of the distribution for the error.
    Techniques:
    	• 4-Plot
    	• Probability Plot
    	• PPCC Plot
###### CONTROL
    Data:
    	A single column of numbers, Y.
    Model:
    	y = constant + error
    Output:
    	A "yes" or "no" to the question "Is the system out of control?".
    Techniques:
    	• Control Charts

#### Comparative and Screening
##### COMPARATIVE
    Data:
    	A single response variable and k independent variables (Y, X1, X2, ... , Xk), primary focus is onone (the primary factor) of these independent variables.
    Model:
    	y = f(x1, x2, ..., xk) + error
    Output:
    	A "yes" or "no" to the question "Is the primary factor significant?".
    Techniques:
    	• Block Plot
    	• Scatter Plot
    	• Box Plot
##### SCREENING
    Data:
    	A single response variable and k independent variables (Y, X1, X2, ... , Xk).
    Model:
    	y = f(x1, x2, ..., xk) + error
    Output:
    	1. A ranked list (from most important to least important) of factors.
    	2. Best settings for the factors.
    	3. A good model/prediction equation relating Y to the factors.
    Techniques:
    	• Block Plot
    	• Probability Plot
    	• Bihistogram
#### Optimization and Regression
##### OPTIMIZATION
    Data:
    	A single response variable and k independent variables (Y, X1, X2, ... , Xk).
    Model:
    	y = f(x1, x2, ..., xk) + error
    Output:
    	Best settings for the factor variables.
    Techniques:
    	• Block Plot
    	• Least Squares Fitting
        • Contour Plot
##### REGRESSION
    Data:
    	A single response variable and k independent variables (Y, X1, X2, ... , Xk). The independent variables can be continuous.
    Model:
    	y = f(x1, x2, ..., xk) + error
    Output:
    	A good model/prediction equation relating Y to the factors.
    Techniques:
    	• Least Squares Fitting
    	• Scatter Plot
    	• 6-Plot
#### Time Series and Multivariate
##### TIME SERIES
    Data:
    	A column of time dependent numbers, Y. In addition, time is an indpendent variable. The time variable can be either explicit or implied. If the data are not equi-spaced, the time variable should be explicitly provided.
    Model:
    	yt = f(t) + error 
    	The model can be either a time domain based or frequency domain based.
    Output:
    	A good model/prediction equation relating Y to previous values of Y.
    Techniques:
    	• Autocorrelation Plot
    	• Spectrum
    	• Complex Demodulation Amplitude Plot
    	• Complex Demodulation Phase Plot
    	• ARIMA Models
##### MULTIVARIATE
    Data:
    	k factor variables (X1, X2, ... , Xk).
    Model:
    	The model is not explicit.
    Output:
    	Identify underlying correlation structure in the data.
    Techniques:
    	• Star Plot
    	• Scatter Plot Matrix
    	• Conditioning Plot
    	• Profile Plot
    	• Principal Components
    	• Clustering
    	• Discrimination/Classification
    Note that multivarate analysis is only covered lightly in this Handbook.
