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
