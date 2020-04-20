---
layout: single
title:  "Coursera Machine Learning - Week 3"
date:   2020-04-19
categories: coursera machine_learning
toc: true
---
# Classification

## Classification and Representation
- \\(y \in \\{0, 1\\} \\) where 0 = "negative class", 1 = "positive class"
- multiclass, if there are more than 1 class + negative
- simple classficiation:
  - Threshold the classfier output \\(h_\theta (x)\\)
- Problem with linear regression for classification:
  - output from \\(h_\theta \in \mathbb{R}\\), where \\(y \in \\{0,1\\} \\)
  - classification itself is not a linear function!
    - remember that it is a boundary (i.e. step function in 2D)
- Use logistic regression to deal with discrete output variable

## Hypothesis Representation
- We define the logistic function (sigmoid) as:
<p>
\[ g(z) = \frac{1}{1+e^{-z}}\]
\[ h_\theta (x) = g(\theta^T x) = \frac{1}{1+e^{-\theta^{T} x}} \]
</p>

- Example of a sigmoid function:

<img src="https://i.stack.imgur.com/KcX81.png" alt="drawing" align="middle" width="500"/>

- Logistic regression:
  - Want to find parameters \\( \theta \\) that shapes the sigmoid function.
  - In this case \\(h_\theta (x)\\) outputs a estimated probability that \\(y = 1\\) with input \\(x\\)
  - In probabilistic form:
\\( h_\theta (x) = P(y=1|x;\theta) \\)

## Decision Boundary
- Note that for sigmoid function:
  - if \\(h_\theta (x) = z \geq 0\\) then \\(g(z) \geq 0.5 \\)
  - if \\(h_\theta (x) = z < 0 \\) then \\( g(z) < 0.5 \\)
  - it means that the sign of the hypothesis function determines the probability \\( g(h_\theta) \\)
- By plotting \\(x_1\\) against \\(x_2\\), it can be seen that the conditions \\( h_\theta(x) \geq 0 \\) creates a linear boundary over the input sample space.
- On decision boundaries:
  - Having a linear basis function, creates linear boundaries
  - For example, using \\(h_\theta(x) = \theta_0 + \theta_1x_1 + \theta_2x_2 + \theta_3x^2_1 + \theta_4x^2_2\\) creates a circular decision boundary
  - High degree polynomial functions can create ellipses, and other complex decision boundaries

# Logistic Regression Model
## Cost Function
- **Idea**: Using MSE over sigmoid hypothesis function creates a non-linear cost function.
<p>
\begin{align*}
  J(\theta)&  = \cfrac{1}{m} \sum^m_{i=1}\text{cost}(h_\theta(x^{(i)}, y^{(i)})) \\
           & \text{where}~\text{cost}(h_\theta(x), y) = \frac{1}{2}(h_\theta(x)-y)^2 \\
  \end{align*}
</p>
- if we use the logistic function as hypothesis, the optimization becomes non-convex
  - non-convex: not guaranteed to converge to global minimum
- Define a new cost function for logistic regression:
<p>$$
\text{cost}(h_\theta(x), y) =
\begin{cases}
~~~~~- \log(h_\theta(x)) & \text{if $y$ = 1} \\
- \log(1-h_\theta(x)) & \text{if $y$ = 0} \\
\end{cases}
$$</p>
- **Intuition**:
  - Note that the above function is a log function mirrored in x-axis
  - Note that the function is positive only in range \\((0, 1]\\)
  - \\( \text{As}~h_\theta(x) \rightarrow 0,~ \text{cost} \rightarrow \infty~\text{when}~y = 1\\)
    - Thus, penalize with a large cost, when classification is wrong
  - \\( \text{As}~h_\theta(x) \rightarrow 1,~ \text{cost} \rightarrow 0~\text{when}~y = 1\\)
    - Don't penalize when the classification is right
  - It is simliar intuition but flipped for the case when \\(y=0\\)

## Simplified cost function and gradient descent
**Idea**: simplify the cost function:
\\[\text{cost}(h_\theta(x), y) = -y\log(h_\theta(x)) - (1-y)\log(1-h_\theta(x)) \\]

**Idea**: derive the logistic regression cost function:
\\[J(\theta) = -\frac{1}{m}\Biggl(\sum^m_{i=1} y^{(i)}\log(h_\theta(x^{(i)})) + (1-y^{(i)})\log(1-h_\theta(x^{(i)}))\Biggr)\\]
- In statistics, this can be derived by Maximum Liklihood Estimation (MLE).
  - Has nice property for optimization (convex)

**Exercise**: derive the gradient for the above cost function.
  - hint: derivative of \\(\frac{\partial}{\partial x}\sigma (x) = \sigma(x)(1-\sigma(x))\\)

Thus, the gradient descent algorithm is:
<p>
\begin{align}
& \text{repeat until convergence} \\
& ~~~~~~~\theta_j := \theta_j - \alpha \frac{1}{m} \sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{(i)})x_j^{(i)} \\
& \text{simultaneously update $\theta_j$ for $j = 0,1,...,n$}
\end{align}
</p>

## Advanced Optimization
- **Idea** Other optimization algorithms than gradient descent:
  - conjugate gradient
  - BFGS
  - L-BFGS
  - No need to pick \\(\alpha\\), uses line search
  - Often faster, at the cost of being more complex

# Multiclass Classification
## One-vs-all
**Idea**: train a logistic regression classifier \\(h_\theta^{i}(x)\\) for each class \\(i\\) to predict the probability
that \\(y=i\\).

# Overfitting
## Problem of Overfitting
- If a given model is failing to generalize due to a strong preconception/bias: underfitting, "High bias"
  - model is too simple
  - not enough data
- If a given model is fitting all the data points but failing to generalize: overfitting, "High variance"
  - model is too complex
  - too many parameters/features
  - not enough regularization

Options:
1. Reduce number of features.
   - Manually select which features to keep
   - Model selection algorithm
2. Regularization
   - Keep all the features, but reduce magnitude/values of parameter \\(\theta_j\\)
   - Works well when we have a lot of features, each contribute a bit to predict \\(y\\)

## Regularization
- **Idea**: penalize some paramters by attributing them to higher cost, to drive down the magnitude (thus effectively reducing their contribution)
  - "Simpler" Hypothesis
  - Less prone to overfitting
  - Optimization becomes a balance act of fitting the training set and reducing magnitude of parameters

  <p>\[ J(\theta) = \frac{1}{2m}\Biggr(\sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{i})^2 + \lambda\sum^{n}_{j=1}\theta_j^2\Biggr) \]</p>

## Regularized Linear Regression
- **Idea**: Apply the regularization term for linear regression
<p>\[ J(\theta) = \frac{1}{2m}\Biggr(\sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{i})^2 + \lambda\sum^{n}_{j=1}\theta_j^2\Biggr) \]</p>

<p>
\begin{align}
& \text{repeat until convergence} \\
& ~~~~~~~\theta_0 := \theta_0 - \alpha \frac{1}{m} \sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{(i)})x_0^{(i)} \\
& ~~~~~~~\theta_j := \theta_j - \alpha \Biggr( \frac{1}{m} \sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{(i)})x_j^{(i)} + \frac{\lambda}{m}\theta_j \Biggr) \\
& \text{simultaneously update $\theta_j$ for $j = 1,...,n$}
\end{align}
</p>

**Note**:
- The update above treats the 0th term separately.
- The above form is \\(\frac{\partial}{\partial\theta_j}J(\theta)\\) with regularization for linear regression
- If we isolate \\(\theta_j\\) terms, a constant of \\(1 - \frac{\lambda}{m}\\) appears, which helps drive down the weights/parameters

- **Idea**: Apply regularization to [normal form of linear regression](/coursera/machine_learning/coursera_ml_week_2/#normal-equations)
<p>\[
\theta = \Biggr(X^T X + \lambda \\
\begin{bmatrix}
   0 & & & \\
   & 1 & & \\
   & & \ddots & \\
   & & & 1
\end{bmatrix}
\Biggr)^{-1}X^T y
\]</p>
- The regularization helps in making the inner matrix singular/invertible, when \\((m < n)\\)

## Regularized Logistic Regression
- **Idea**: Apply the regularization term for logistic regression cost function
\\[J(\theta) = -\Biggl(\frac{1}{m}\sum^m_{i=1} y^{(i)}\log(h_\theta(x^{(i)})) + (1-y^{(i)})\log(1-h_\theta(x^{(i)})) - \frac{\lambda}{m}\sum^{n}_{j=1}\theta_j^2 \Biggr) \\]
- The overall gradient descent for regularized linear regression is same as [Regularized Linear Regression](/coursera/machine_learning/coursera_ml_week_3/#regularized-linear-regression)
- Take note here that the sigmoid function is used in the hypothesis term.
