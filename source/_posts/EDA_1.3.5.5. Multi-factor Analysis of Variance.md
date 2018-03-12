---
title: EDA_1.3.5.5. Multi-factor Analysis of Variance
date: 2018-03-12 16:58:12
categories: "statistics"
tags:
     - Multi-factor Analysis of Variance
description: EDA_1.3.5.5. Multi-factor Analysis of Variance
toc: true
---
### Purpose: Detect significant factors
The analysis of variance (ANOVA) (Neter, Wasserman, and Kutner, 1990) is used to detect significant factors in a multi-factor model. In the multi-factor model, there is a response (dependent) variable and one or more factor (independent) variables. This is a common model in designed experiments where the experimenter sets the values for each of the factor variables and then measures the response variable.

Each factor can take on a certain number of values. These are referred to as the levels of a factor. The number of levels can vary betweeen factors. For designed experiments, the number of levels for a given factor tends to be small. Each factor and level combination is a cell. Balanced designs are those in which the cells have an equal number of observations and unbalanced designs are those in which the number of observations varies among cells. It is customary to use balanced designs in designed experiments.

### Definition
The Product and Process Comparisons chapter (chapter 7) contains a more extensive discussion of two-factor ANOVA, including the details for the mathematical computations.

The model for the analysis of variance can be stated in two mathematically equivalent ways. We explain the model for a two-way ANOVA (the concepts are the same for additional factors). In the following discussion, each combination of factors and levels is called a cell. In the following, the subscript i refers to the level of factor 1, j refers to the level of factor 2, and the subscript k refers to thekth observation within the (i,j)th cell. For example, Y235refers to the fifth observation in the second level of factor 1 and the third level of factor 2.

The first model is

	Yijk=μij+Eijk

This model decomposes the response into a mean for each cell and an error term. The analysis of variance provides estimates for each cell mean. These cell means are the predicted values of the model and the differences between the response variable and the estimated cell means are the residuals. That is

	Y^ijk=μ^ij
	Rijk=Yijk−μ^ij

The second model is

	Yijk=μ+αi+βj+Eijk

This model decomposes the response into an overall (grand) mean, factor effects (α^i and β^j represent the effects of the i-th level of the first factor and the j-th level of the second factor, respectively), and an error term. The analysis of variance provides estimates of the grand mean and the factor effects. The predicted values and the residuals of the model are

	Y^ijk=μ^+α^i+β^j
	Rijk=Yijk−μ^−α^i−β^j

The distinction between these models is that the second model divides the cell mean into an overall mean and factor effects. This second model makes the factor effect more explicit, so we will emphasize this approach.

### Model Validation
Note that the ANOVA model assumes that the error term,Eijk, should follow the assumptions for a univariate measurement process. That is, after performing an analysis of variance, the model should be validated by analyzing the residuals.

### Multi-Factor ANOVA Example
An analysis of variance was performed for the JAHANMI2.DATdata set. The data contains four, two-level factors: table speed, down feed rate, wheel grit size, and batch. There are 30 measurements of ceramic strength for each factor combination for a total of 480 measurements.

     SOURCE              DF SUM OF SQUARES    MEAN SQUARE   F STATISTIC
     ------------------------------------------------------------------
     TABLE SPEED          1   26672.726562   26672.726562        6.7080
     DOWN FEED RATE       1   11524.053711   11524.053711        2.8982
     WHEEL GRIT SIZE      1   14380.633789   14380.633789        3.6166
     BATCH                1  727143.125000  727143.125000      182.8703
     RESIDUAL           475 1888731.500000    3976.276855
     TOTAL (CORRECTED)  479 2668446.000000    5570.868652

     RESIDUAL STANDARD DEVIATION = 63.05772781

     FACTOR          LEVEL   N      MEAN     SD(MEAN)
     ------------------------------------------------
     TABLE SPEED      -1    240  657.53168    2.87818
                       1    240  642.62286    2.87818
     DOWN FEED RATE   -1    240  645.17755    2.87818
                       1    240  654.97723    2.87818
     WHEEL GRIT SIZE  -1    240  655.55084    2.87818
                       1    240  644.60376    2.87818
     BATCH             1    240  688.99890    2.87818
                       2    240  611.15594    2.87818

The ANOVA decomposes the variance into the following component sum of squares:

	• Total sum of squares. The degrees of freedom for this entry is the number of observations minus one.
	• Sum of squares for each of the factors. The degrees of freedom for these entries are the number of levels for the factor minus one. The mean square is the sum of squares divided by the number of degrees of freedom.
	• Residual sum of squares. The degrees of freedom is the total degrees of freedom minus the sum of the factor degrees of freedom. The mean square is the sum of squares divided by the number of degrees of freedom.

The analysis of variance summarizes how much of the variance in the data (total sum of squares) is accounted for by the factor effects (factor sum of squares) and how much is due to random error (residual sum of squares). Ideally, we would like most of the variance to be explained by the factor effects. The ANOVA table provides a formal Ftest for the factor effects. To test the overall batch effect in our example we use the following hypotheses.

      H0: All individual batch means are equal. 
      Ha: At least one batch mean is not equal to the others.

The F statistic is the mean square for the factor divided by the residual mean square. This statistic follows an Fdistribution with (k-1) and (N-k) degrees of freedom wherek is the number of levels for the given factor. Here, we see that the size of the "direction" effect dominates the size of the other effects. For our example, the critical Fvalue (upper tail) for α = 0.05, (k-1) = 1, and (N-k) = 475 is 3.86111. Thus, "table speed" and "batch" are significant at the 5 % level while "down feed rate" and "wheel grit size" are not significant at the 5 % level.
In addition to the quantitative ANOVA output, it is recommended that any analysis of variance be complemented with model validation. At a minimum, this should include

	1. A run sequence plot of the residuals.
	2. A normal probability plot of the residuals.
	3. A scatter plot of the predicted values against the residuals.

### Questions
The analysis of variance can be used to answer the following questions:

	1. Do any of the factors have a significant effect?
	2. Which is the most important factor?
	3. Can we account for most of the variability in the data?

### Related Techniques
* One-factor analysis of variance
* Two-sample t-test
* Box plot
* Block plot
* DOE mean plot

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda355.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda355.htm)
