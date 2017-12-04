---
title: Statistical Inference and Estimation
date: 2017-12-04 20:26:12 
categories: "statistics" 
tags: 
     - Sampling distribution
     - Central Limit Theorem
description: Statistical Inference and Estimation
toc: true
---
# Statistical Inference, Model & Estimation

Recall, a **statistical inference** aims at learning characteristics of the population from a sample; the population characteristics are *parameters* and sample characteristics are *statistics*.

A **statistical model** is a representation of a complex phenomena that generated the data.

* It has mathematical formulations that describe relationships between random variables and parameters.
* It makes assumptions about the random variables, and sometimes parameters.
* A general form: data = model + residuals
* Model should explain most of the variation in the data
* Residuals are a representation of a lack-of-fit, that is of the portion of the data unexplained by the model.

**Estimation** represents ways or a process of learning and determining the population parameter based on the model fitted to the data.

Point estimation and interval estimation, and hypothesis testing are three main ways of learning about the population parameter from the sample statistic.

An **estimator** is particular example of a statistic, which becomes an **estimate** when the formula is replaced with actual observed sample values.

**Point estimation** = a single value that estimates the parameter. Point estimates are single values calculated from the sample

**Confidence Intervals** = gives a range of values for the parameter Interval estimates are intervals within which the parameter is expected to fall, with a certain degree of confidence.

**Hypothesis tests** = tests for a specific value(s) of the parameter.

In order to perform these inferential tasks, i.e., make inference about the unknown population parameter from the sample statistic, we need to know the likely values of the sample statistic. What would happen if we do sampling many times?

![](https://onlinecourses.science.psu.edu/stat504/sites/onlinecourses.science.psu.edu.stat504/files/lesson01/height_plot.gif)

# CLT,Central Limit Theorem
Sampling distribution of the sample mean:

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204144632.png)

For categorical data, the CLT holds for the sampling distribution of the sample proportion.

So, what is the 95% confidence interval? Based on the CLT, the 95% CI is

![](/assets/Statistics/Statistical Inference and Estimation/QQ截图20171204145320.png)
