---
title: EDA_1.3.6.1 What is a Probability Distribution
date: 2018-03-12 17:08:12
categories: "statistics"
tags:
     - What is a Probability Distribution
description: EDA_1.3.6.1 What is a Probability Distribution
toc: true
---
### Discrete Distributions
The mathematical definition of a discrete probability function, p(x), is a function that satisfies the following properties.

	1. The probability that x can take a specific value is p(x). That is
    P[X=x]=p(x)=px
	2. p(x) is non-negative for all real x.
	3. The sum of p(x) over all possible values of x is 1, that is
    ∑jpj=1
    where j represents all possible values that x can have and pj is the probability at xj.
    One consequence of properties 2 and 3 is that 0 <= p(x) <= 1.

What does this actually mean? A discrete probability function is a function that can take a discrete number of values (not necessarily finite). This is most often the non-negative integers or some subset of the non-negative integers. There is no mathematical restriction that discrete probability functions only be defined at integers, but in practice this is usually what makes sense. For example, if you toss a coin 6 times, you can get 2 heads or 3 heads but not 2 1/2 heads. Each of the discrete values has a certain probability of occurrence that is between zero and one. That is, a discrete function that allows negative values or values greater than one is not a probability function. The condition that the probabilities sum to one means that at least one of the values has to occur.

### Continuous Distributions
The mathematical definition of a continuous probability function, f(x), is a function that satisfies the following properties.

	1. The probability that x is between two points a and b is
    p[a≤x≤b]=∫baf(x)dx
	2. It is non-negative for all real x.
	3. The integral of the probability function is one, that is
    ∫∞−∞f(x)dx=1

What does this actually mean? Since continuous probability functions are defined for an infinite number of points over a continuous interval, the probability at a single point is always zero. Probabilities are measured over intervals, not single points. That is, the area under the curve between two distinct points defines the probability for that interval. This means that the height of the probability function can in fact be greater than one. The property that the integral must equal one is equivalent to the property for discrete distributions that the sum of all the probabilities must equal one.

### Probability Mass Functions Versus Probability Density Functions
Discrete probability functions are referred to as probability mass functions and continuous probability functions are referred to as probability density functions. The term probability functions covers both discrete and continuous distributions.

There are a few occasions in the e-Handbook when we use the term probability density function in a generic sense where it may apply to either probability density or probability mass functions. It should be clear from the context whether we are referring only to continuous distributions or to either continuous or discrete distributions.
