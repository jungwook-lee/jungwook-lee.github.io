---
layout: single
title:  "Coursera Machine Learning - Week 1"
date:   2020-03-16
categories: coursera machine_learning
toc: true
---

## Introduction

Machine learning definition by Tom Mitchell:

> Program learns from E (experience) with respect to T(task) and P(measure), if its performance of task T, measured by P, improves with E

Supervised Learning:
- Regression:
  - map input variables to continuous function
- Classification
  - map input variables to discrete functions/categories

Unsupervised Learning:
- clustering
- market segementation
- learning the structure of data/relationship among variables

## Model and Cost Function

- Training Set -> Learning Algorithm -> Hypothesis
- Hypothesis: functions that maps input to output

\\[h : X \rightarrow Y \\]

- Following is a linear regression with one variable (\\(x\\)) (univariate linear regression).

\\[h_\theta = \theta_0 + \theta_1 x\\]

- Cost function \\(J(\theta_0, \theta_1)\\) measures the accuracy of our hypothesis

<p>\[ J(\theta_0, \theta_1) = \frac{1}{2m}\sum_{i=1}^{m}(\hat{y}i - y_i)^2 = \frac{1}{2m}\sum_{i=1}(h_\theta(x_i) - y_i)^2 \]</p>

- The following form is "squared error function"/"mean squared error"
  - mean is halved for computation of gradient descent (derivative of cost function cancels 1/2)

\\[\min_{\theta_0, \theta_1} J(\theta_0, \theta_1)\\]

- Cost function intuition:
  - The cost function outputs error given the parameter of the model
  - The goal is to find parameters that provide minimal cost output
  - The minimum can be found via optimization
  - More than often the optimization will not be linear!
- Cost functions with 2 parameters can be visualized with a contour plot
- The shape becomes a bowl with a minimum at the bottom

## Parameter Learing
- How should we find the parameter that minimizes the cost function?
- **Gradient descent**:
  - Start at an arbitrary point
  - keep changing the paramter to reduce the cost until minimum can be found
- With more than 1 global optima, gradient descent will likely be stuck at local optimal points

> repeat until convergence
\\[\theta_j := \theta_j - \alpha \frac{\partial}{\partial\theta_j}J(\theta_0, \theta_1) (for\ j=0\ and\ j=1)\\]

- Note that \\(:=\\) symbol means assignment
- \\(\alpha\\) is learning rate (always positive)
  - higher learning rate means higher change per update
  - if too small, will take a long time to converge
  - if too large, diverge or fail to converge
- Can we converge with a constant learning rate?
  - Yes! since we are expecting that the gradient is getting smaller when it approaches local minima
- Note that the parameter needs simultaneous update until new assignment
- **Exercise**: Calculate the partial derivative for the mean squared error! (hint: chain rule)
- Convex functions always have a or multiple global optimum
  - squared function are convex
- **Batch** Gradient Descent: each step uses all training examples

## Linear Algebra Review
- Matrix multiplication: not commutative but associative
- Identity: 1's on diagonals, rest 0's
- Matrix inverse:
  - Not all numbers have inverse (i.e. 0 and \\(0^{-1}\\) is undefined)
  - 2 conditions: square matrix, determinant is not zero (non-singular)

> If A is an m x m matrix, and if it has and inverse,
\\[ AA^{-1} = A^{-1}A = I \\]
