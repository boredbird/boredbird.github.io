---
title: Sequential Minimal Optimization
date: 2017-11-29 20:26:12 
categories: "机器学习" 
tags: 
     - SVM
     - SMO
description: Sequential Minimal Optimization:A Fast Algorithm for Training Support Vector Machines
toc: true
---
### INTRODUCTION
Training a support vector machine requires the solution of a very large quadratic programming (QP) optimization problem. SMO breaks this large QP problem into a series of smallest possible QP problems. These small QP problems are solved analytically, which avoids using a time-consuming numerical QP optimization as an inner loop. The amount of memory required for SMO is linear in the training set size,which allows SMO to handle very large training sets.SMO’s computation time is dominated by SVM evaluation, hence SMO is fastest for linear SVMs and sparse data sets.Instead of previous SVM learning algorithms that use numerical quadratic programming (QP) as an inner loop, SMO uses an analytic QP step.

### Overview of Support Vector Machines
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig1.png" width="60%">
  <div class="figcaption">
  </div>
</div>

<!--more-->

### Lagrange dual form
SVM在求解过程中首先用了拉格朗日对偶，作用是将w的计算提前并消除w，使得优化函数变为拉格朗日乘子的单一参数优化问题。
对偶函数最后的优化问题：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig2.png" width="60%">
  <div class="figcaption">
  </div>
</div>

There is a one-to-one relationship between each Lagrange multiplier and each training example.Once the Lagrange multipliers are determined, the normal vector *w*
and the threshold *b* can be derived from the Lagrange multipliers:

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig3.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### linearly unseparable
Of course, not all data sets are linearly separable. There may be no hyperplane that splits the positive examples from the negative examples. In the formulation above, the non-separable case would correspond to an infinite solution. However, in 1995, Cortes & Vapnik  suggested a modification to the original optimization statement (3) which allows, but penalizes, the failure of an example to reach the correct margin. That modification is:

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig4.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### generalized to non-linear classifiers
SVMs can be even further generalized to non-linear classifiers. The output of a non-linear SVM is explicitly computed from the Lagrange multipliers:

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig5.png" width="60%">
  <div class="figcaption">
  </div>
</div>

### Karush-Kuhn-Tucker (KKT) conditions
The QP problem in equation (11), above, is the QP problem that the SMO algorithm will solve. In order to make the QP problem above be positive definite, the kernel function K must obey Mercer’s conditions.The Karush-Kuhn-Tucker (KKT) conditions are necessary and sufficient conditions for an optimal point of a positive definite QP problem. The KKT conditions for the QP problem (11) are particularly simple. The QP problem is solved when, for all i:
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig6.png" width="40%">
  <div class="figcaption">
  </div>
</div>
where *ui* is the output of the SVM for the ith training example. Notice that the KKT conditions
can be evaluated on one example at a time, which will be useful in the construction of the SMO
algorithm.

### SEQUENTIAL MINIMAL OPTIMIZATION
Sequential Minimal Optimization (SMO) is a simple algorithm that can quickly solve the SVM QP problem without any extra matrix storage and without using numerical QP optimization steps at all. SMO decomposes the overall QP problem into QP sub-problems, using Osuna’s theorem to ensure convergence.

Unlike the previous methods, SMO chooses to solve the smallest possible optimization problem at every step. For the standard SVM QP problem, the smallest possible optimization problem involves two Lagrange multipliers, because the Lagrange multipliers must obey a linear equality constraint. At every step, SMO chooses two Lagrange multipliers to jointly optimize, finds the optimal values for these multipliers, and updates the SVM to reflect the new optimal values.

The advantage of SMO lies in the fact that solving for two Lagrange multipliers can be done analytically. Thus, numerical QP optimization is avoided entirely. The inner loop of the algorithm can be expressed in a short amount of C code, rather than invoking an entire QP library routine. Even though more optimization sub-problems are solved in the course of the algorithm,each sub-problem is so fast that the overall QP problem is solved quickly.

In addition, SMO requires no extra matrix storage at all. Thus, very large SVM training problems can fit inside of the memory of an ordinary personal computer or workstation. Because no matrix algorithms are used in SMO, it is less susceptible to numerical precision problems.

There are two components to SMO: an analytic method for solving for the two Lagrange multipliers, and a heuristic for choosing which multipliers to optimize.

假设我们选取了初始值{a_1,a_2,a_3,...,a_n}满足了问题中的约束条件。接下来，{a_3,a_4,...,a_n}，这样*W*就是*a_1*和*a_2*的函数。并且*a_1*和*a_2*满足条件：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig8.png" width="40%">
  <div class="figcaption">
  </div>
</div>

由于{a_3,a_4,...,a_n}都是已知固定值，因此右边是一个具体的常数。当*y_1*和*y_2*异号时，也就是一个为1，一个为-1时，他们可以表示成一条直线，斜率为1；同理当*y_1*和*y_2*同号时，斜率为-1.

<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig7.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### Solving for Two Lagrange Multipliers
In order to solve for the two Lagrange multipliers, SMO first computes the constraints on these multipliers and then solves for the constrained minimum. For convenience, all quantities that refer to the first multiplier will have a subscript 1, while all quantities that refer to the second multiplier will have a subscript 2. Because there are only two multipliers, the constraints can be easily be displayed in two dimensions (see figure 3). The bound constraints (9) cause the Lagrange multipliers to lie within a box, while the linear equality constraint (6) causes the Lagrange multipliers to lie on a diagonal line. Thus, the constrained minimum of the objective function must lie on a diagonal line segment (as shown in figure 3). This constraint explains why two is the minimum number of Lagrange multipliers that can be optimized: if SMO optimized only one multiplier, it could not fulfill the linear equality constraint at every step.

The ends of the diagonal line segment can be expressed quite simply. Without loss of generality,
the algorithm first computes the second Lagrange multiplier *a_2* and computes the ends of the
diagonal line segment in terms of *a_2*. If the target *y_1* does not equal the target *y_2*, then the
following bounds apply to *a_2*:

L = max(0,*a_2* - *a_1*), H = min(C,C + *a_2*- *a_1*).

If the target *y_1* equals the target *y_2*, then the following bounds apply to *a_2*:

L = max(0,*a_2* + *a_1* - C), H = min(C, *a_2* + *a_1*).

然后将*a_1*用*a_2*表示：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig9.png" width="20%">
  <div class="figcaption">
  </div>
</div>

然后反代入*W*中，得：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig10.png" width="60%">
  <div class="figcaption">
  </div>
</div>

展开后*W*可以表示成*a_2*的二次函数。这样，直接求导可以得到*a_2*，然而要保证满足*L<=a_2<=H*，我们使用*new,unclipped*表示求导求出来的*a_2*，然后最后的*a_2*,要根据下面情况得到：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig11.png" width="60%">
  <div class="figcaption">
  </div>
</div>

这样得到新的*a_2*，就可以得到新的*a_1*。

#### 论文中的表达方式：
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig12.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### Heuristics for Choosing Which Multipliers To Optimize
As long as SMO always optimizes and alters two Lagrange multipliers at every step and at least one of the Lagrange multipliers violated the KKT conditions before the step, then each step will decrease the objective function according to Osuna’s theorem [16]. Convergence is thus guaranteed. In order to speed convergence, SMO uses heuristics to choose which two Lagrange multipliers to jointly optimize.

There are two separate choice heuristics: one for the first Lagrange multiplier and one for the second. The choice of the first heuristic provides the outer loop of the SMO algorithm. The outer loop first iterates over the entire training set, determining whether each example violates the KKT conditions (12). If an example violates the KKT conditions, it is then eligible for optimization. After one pass through the entire training set, the outer loop iterates over all examples whose Lagrange multipliers are neither 0 nor C (the non-bound examples). Again, each example is checked against the KKT conditions and violating examples are eligible for optimization. The outer loop makes repeated passes over the non-bound examples until all of the non-bound examples obey the KKT conditions within e. The outer loop then goes back and iterates over the entire training set. The outer loop keeps alternating between single passes over the entire training set and multiple passes over the non-bound subset until the entire training set obeys the KKT conditions within e, whereupon the algorithm terminates.

The first choice heuristic concentrates the CPU time on the examples that are most likely to violate the KKT conditions: the non-bound subset. As the SMO algorithm progresses, examples that are at the bounds are likely to stay at the bounds, while examples that are not at the bounds will move as other examples are optimized. The SMO algorithm will thus iterate over the nonbound subset until that subset is self-consistent, then SMO will scan the entire data set to search for any bound examples that have become KKT violated due to optimizing the non-bound subset.

Notice that the KKT conditions are checked to be within e of fulfillment. Typically, e is set to be 10-3. Recognition systems typically do not need to have the KKT conditions fulfilled to high accuracy: it is acceptable for examples on the positive margin to have outputs between 0.999 and 1.001. The SMO algorithm (and other SVM algorithms) will not converge as quickly if it is required to produce very high accuracy output.

Once a first Lagrange multiplier is chosen, SMO chooses the second Lagrange multiplier to
maximize the size of the step taken during joint optimization. Now, evaluating the kernel
function K is time consuming, so SMO approximates the step size by the absolute value of the numerator in equation (16): |E_1 - E_2|. SMO keeps a cached error value E for every non-bound example in the training set and then chooses an error to approximately maximize the step size. If E_1 is positive, SMO chooses an example with minimum error E2. If E1 is negative, SMO chooses
an example with maximum error E_2.

Under unusual circumstances, SMO cannot make positive progress using the second choice
heuristic described above. For example, positive progress cannot be made if the first and second training examples share identical input vectors x, which causes the objective function to become semi-definite. In this case, SMO uses a hierarchy of second choice heuristics until it finds a pair of Lagrange multipliers that can be make positive progress. Positive progress can be determined by making a non-zero step size upon joint optimization of the two Lagrange multipliers . The hierarchy of second choice heuristics consists of the following. If the above heuristic does not make positive progress, then SMO starts iterating through the non-bound examples, searching for an second example that can make positive progress. If none of the non-bound examples make positive progress, then SMO starts iterating through the entire training set until an example is found that makes positive progress. Both the iteration through the non-bound examples and the iteration through the entire training set are started at random locations, in order not to bias SMO towards the examples at the beginning of the training set. In extremely degenerate circumstances, none of the examples will make an adequate second example. When this happens, the first example is skipped and SMO continues with another chosen first example.

### Computing the Threshold
The threshold *b* is re-computed after each step, so that the KKT conditions are fulfilled for both optimized examples. The following threshold *b_1* is valid when the new *a_1* is not at the bounds,because it forces the output of the SVM to be *y_1* when the input is *x_1*:
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig13.png" width="80%">
  <div class="figcaption">
  </div>
</div>
The following threshold *b_2* is valid when the new *a_2* is not at bounds, because it forces the output of the SVM to be *y_2* when the input is *x_2*:
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig14.png" width="80%">
  <div class="figcaption">
  </div>
</div>
When both *b_1* and *b_2* are valid, they are equal. When both new Lagrange multipliers are at bound and if *L* is not equal to *H*, then the interval between *b_1* and *b_2* are all thresholds that are consistent with the KKT conditions. SMO chooses the threshold to be halfway in between *b_1* and *b_2*.

### An Optimization for Linear SVMs
To compute a linear SVM, only a single weight vector *w* needs to be stored, rather than all of the training examples that correspond to non-zero Lagrange multipliers. If the joint optimization succeeds, the stored weight vector needs to be updated to reflect the new Lagrange multiplier values. The weight vector update is easy, due to the linearity of the SVM:
<div class="fig figcenter fighighlight">
  <img src="/assets/ML/svm/SMO_fig15.png" width="80%">
  <div class="figcaption">
  </div>
</div>

### Pseudo Code Details
The pseudo-code below describes the entire SMO algorithm:
```

	target = desired output vector
	point = training point matrix
	
	procedure takeStep(i1,i2)
		if (i1 == i2) return 0
		alph1 = Lagrange multiplier for i1
		y1 = target[i1]
		E1 = SVM output on point[i1] – y1 (check in error cache)
		s = y1*y2
		Compute L, H via equations (13) and (14)
		if (L == H)
			return 0
		k11 = kernel(point[i1],point[i1])
		k12 = kernel(point[i1],point[i2])
		k22 = kernel(point[i2],point[i2])
		eta = k11+k22-2*k12
		if (eta > 0)
		{
			a2 = alph2 + y2*(E1-E2)/eta
			if (a2 < L) a2 = L
			else if (a2 > H) a2 = H
		}
		else
		{
			Lobj = objective function at a2=L
			Hobj = objective function at a2=H
			if (Lobj < Hobj-eps)
			a2 = L
			else if (Lobj > Hobj+eps)
			a2 = H
			else
			a2 = alph2
		}
		if (|a2-alph2| < eps*(a2+alph2+eps))
			return 0
		a1 = alph1+s*(alph2-a2)
		Update threshold to reflect change in Lagrange multipliers
		Update weight vector to reflect change in a1 & a2, if SVM is linear
		Update error cache using new Lagrange multipliers
		Store a1 in the alpha array
		Store a2 in the alpha array
		return 1
	endprocedure
	
	procedure examineExample(i2)
		y2 = target[i2]
		alph2 = Lagrange multiplier for i2
		E2 = SVM output on point[i2] – y2 (check in error cache)
		r2 = E2*y2
		if ((r2 < -tol && alph2 < C) || (r2 > tol && alph2 > 0))
		{
			if (number of non-zero & non-C alpha > 1)
			{
				i1 = result of second choice heuristic (section 2.2)
				if takeStep(i1,i2)
				return 1
			}
			
			loop over all non-zero and non-C alpha, starting at a random point
			{
				i1 = identity of current alpha
				if takeStep(i1,i2)
				return 1
			}
			
			loop over all possible i1, starting at a random point
			{
				i1 = loop variable
				if (takeStep(i1,i2)
				return 1
			}
		}
		return 0
	endprocedure
	
	main routine:
		numChanged = 0;
		examineAll = 1;
		while (numChanged > 0 | examineAll)
		{
			numChanged = 0;
			if (examineAll)
				loop I over all training examples
					numChanged += examineExample(I)
			else
				loop I over examples where alpha is not 0 & not C
					numChanged += examineExample(I)
			if (examineAll == 1)
				examineAll = 0
			else if (numChanged == 0)
				examineAll = 1
		}
```

via

* Sequential Minimal Optimization: A Fast Algorithm for Training Support Vector Machines;© 1998 John Platt
* [支持向量机（五）SMO算法](http://www.cnblogs.com/jerrylead/archive/2011/03/18/1988419.html)
* [【机器学习详解】SMO算法剖析](http://blog.csdn.net/luoshixian099/article/details/51227754)