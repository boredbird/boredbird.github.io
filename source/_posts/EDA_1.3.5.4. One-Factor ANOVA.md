---
title: EDA_1.3.5.4. One-Factor ANOVA
date: 2018-03-12 16:58:12
categories: "statistics"
tags:
     - One-Factor ANOVA
description: EDA_1.3.5.4. One-Factor ANOVA
toc: true
---
### Purpose: Test for Equal Means Across Groups
One factor analysis of variance (Snedecor and Cochran, 1989) is a special case of analysis of variance (ANOVA), for one factor of interest, and a generalization of the two-sample t-test.

The two-sample t-test is used to decide whether two groups (levels) of a factor have the same mean. One-way analysis of variance generalizes this to levels where k, the number of levels, is greater than or equal to 2.

For example, data collected on, say, five instruments have one factor (instruments) at five levels. The ANOVA tests whether instruments have a significant effect on the results.

### Definition
The Product and Process Comparisons chapter (chapter 7) contains a more extensive discussion of one-factor ANOVA, including the details for the mathematical computations of one-way analysis of variance.

The model for the analysis of variance can be stated in two mathematically equivalent ways. In the following discussion, each level of each factor is called a cell. For the one-way case, a cell and a level are equivalent since there is only one factor. In the following, the subscripti refers to the level and the subscript j refers to the observation within a level. For example,Y23 refers to the third observation in the second level.

The first model is

    Yij=μi+Eij

This model decomposes the response into a mean for each cell and an error term. The analysis of variance provides estimates for each cell mean. These estimated cell means are the predicted values of the model and the differences between the response variable and the estimated cell means are the residuals. That is

	Yij^=μ^i
	Rij=Yij−μ^i

The second model is

	Yij=μ+αi+Eij

This model decomposes the response into an overall (grand) mean, the effect of the ith factor level, and an error term. The analysis of variance provides estimates of the grand mean and the effect of the ith factor level. The predicted values and the residuals of the model are

	Y^ij=μ^+α^i
	Rij=Yij−μ^−α^i

The distinction between these models is that the second model divides the cell mean into an overall mean and the effect of the i-th factor level. This second model makes the factor effect more explicit, so we will emphasize this approach.

### Model Validation
Note that the ANOVA model assumes that the error term, Eij, should follow the assumptions for a univariate measurement process. That is, after performing an analysis of variance, the model should be validated by analyzing the residuals.

### One-Way ANOVA Example
A one-way analysis of variance was generated for theGEAR.DAT data set. The data set contains 10 measurements of gear diameter for ten different batches for a total of 100 measurements.

                       DEGREES OF     SUM OF      MEAN
    SOURCE              FREEDOM      SQUARES     SQUARE    F STATISTIC
    ----------------   ----------   --------    --------   -----------
    BATCH                   9       0.000729    0.000081      2.2969   
    RESIDUAL               90       0.003174    0.000035
    TOTAL (CORRECTED)      99       0.003903    0.000039

    RESIDUAL STANDARD DEVIATION = 0.00594
    BATCH     N      MEAN    SD(MEAN)
    ---------------------------------
      1      10    0.99800    0.00188
      2      10    0.99910    0.00188
      3      10    0.99540    0.00188
      4      10    0.99820    0.00188
      5      10    0.99190    0.00188
      6      10    0.99880    0.00188
      7      10    1.00150    0.00188
      8      10    1.00040    0.00188
      9      10    0.99830    0.00188
     10      10    0.99480    0.00188

The ANOVA table decomposes the variance into the following component sum of squares:

	• Total sum of squares. The degrees of freedom for this entry is the number of observations minus one.
	• Sum of squares for the factor. The degrees of freedom for this entry is the number of levels minus one. The mean square is the sum of squares divided by the number of degrees of freedom.
	• Residual sum of squares. The degrees of freedom is the total degrees of freedom minus the factor degrees of freedom. The mean square is the sum of squares divided by the number of degrees of freedom.

The sums of squares summarize how much of the variance in the data (total sum of squares) is accounted for by the factor effect (batch sum of squares) and how much is random error (residual sum of squares). Ideally, we would like most of the variance to be explained by the factor effect.

The ANOVA table provides a formal F test for the factor effect. For our example, we are testing the following hypothesis.

      H0: All individual batch means are equal. 
      Ha: At least one batch mean is not equal to the others.

The F statistic is the batch mean square divided by the residual mean square. This statistic follows an Fdistribution with (k-1) and (N-k) degrees of freedom. For our example, the critical F value (upper tail) for α = 0.05, (k-1) = 9, and (N-k) = 90 is 1.9856. Since the Fstatistic, 2.2969, is greater than the critical value, we conclude that there is a significant batch effect at the 0.05 level of significance.

Once we have determined that there is a significant batch effect, we might be interested in comparing individual batch means. The batch means and the standard errors of the batch means provide some information about the individual batches. However, we may want to employ multiple comparison methods for a more formal analysis. (See Box, Hunter, and Hunter for more information.)

In addition to the quantitative ANOVA output, it is recommended that any analysis of variance be complemented with model validation. At a minimum, this should include:

	1. a run sequence plot of the residuals,
	2. a normal probability plot of the residuals, and
	3. a scatter plot of the predicted values against the residuals.

### Question
The analysis of variance can be used to answer the following question

	• Are means the same across groups in the data?

### Importance
The analysis of uncertainty depends on whether the factor significantly affects the outcome.

### Related Techniques
* Two-sample t-test
* Multi-factor analysis of variance
* Regression
* Box plot

via [http://www.itl.nist.gov/div898/handbook/eda/section3/eda354.htm](http://www.itl.nist.gov/div898/handbook/eda/section3/eda354.htm)
