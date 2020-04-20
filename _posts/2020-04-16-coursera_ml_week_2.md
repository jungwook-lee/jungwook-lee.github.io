---
layout: single
title:  "Coursera Machine Learning - Week 2"
date:   2020-04-16 21:29:19 -0400
categories: coursera machine_learning
toc: true
---
# Multivariate Linear Regression

## Multiple Features
- Note on notation \\(x_{n}^{(i)}\\)
  - lowercase \\(n\\) is the feature index
  - superscrit \\(i\\) is training instance index

Previously for univariate hypothesis:
\\[h_\theta (x) = \theta_0 + \theta_1 x\\]
With multiple features:
\\[h_\theta (x) = \theta_0 + \theta_1 x + \theta_2 x + \theta_3 x ...\\]

For convenience of notation, define \\(x_0 = 1\\). Thus,

<!-- matrix -->
<p>\[
x =
\begin{bmatrix}
  1 \\
  x_1 \\
  x_2 \\
  x_3 \\
  \vdots \\
\end{bmatrix}
\in \mathbb{R}^{n+1}
\hspace{20pt}
\theta =
\begin{bmatrix}
  \theta_0 \\
  \theta_1 \\
  \theta_2 \\
  \theta_3 \\
  \vdots \\
\end{bmatrix}
\in \mathbb{R}^{n+1}
\]</p>

And simply:
\\[h_\theta(x) = \theta^{T}x\\]

> From here on, \\(x \in \mathbb{R}^{n+1}\\) and \\(\theta \in \mathbb{R}^{n+1}\\) vectors

## Gradient Descent for Multiple Variables
The cost function in multivariate form is similar:

<p>\[ J(\theta) = \frac{1}{2m}\sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{i})^2 \]</p>

To update the gradient descent for multivariable form:

> repeat until convergence
<p>\[
\theta_j := \theta_j - \alpha \frac{1}{m} \sum_{i=1}^{m}(h_\theta (x^{(i)}) - y^{(i)})x_j^{(i)}
\]</p>
> simultaneously update \\(\theta_j\\) for j = 0,1,...,n

## Feature Scaling

**Idea**: Make sure features are on a similar scale.
- Having a single variable that is larger in scale can single handedly affect the contour/hills of the error function.
- Having a elongated or lopsided hills may make it harder to converge to global minimum.

**Techniques**:
- Feature scaling: make the features to \\(-1 \leq x_i \leq 1\\)
- Mean Normalization: make the features have approximately zero mean
  - Don't apply to bias term. \\(x_0 = 1\\)
  - i.e. \\(x_i := (x_i - \mu_i) / \sigma_i\\) where \\(\sigma_i\\) is standard deviation

## Learning Rate
**Idea**: How to "debug" correct learning rate \\(\alpha\\)
- Plot the cost \\(J_\theta\\) vs. # of Iterations
  - The cost value should decrease after every iteration
  - Should look like the positive section of rational function
- Automatic convergence test:
  - Finish when cost decrease less than a certain threshold
  - Not so easy to find the threshold
- If the cost ever increase, increase the learning rate
- If the values are not converging fast, then increase learning rate
- Practically, try a bunch of value by power of 10
  - 0.001, 0.01, 0.1, 1

## Features and Polynomial Regression
- Features can be added by using existing features (i.e. length, height to calculate area)
- You can easily turn linear regression to polynomial regression
  - Substitue each feature term with squared, cubic ... versions of the feature
\\[h_\theta (x) = \theta_0 + \theta_1 (x) + \theta_2 (x^2) + \theta_3 (x^3) ...\\]
  - Be careful about the the ranges of the polynomial features values!
  - Instead of polynomials, you can also use square root function
\\[h_\theta (x) = \theta_0 + \theta_1 (x) + \theta_2\sqrt{x}\\]
  - Note that different functions output different ranges, so feature scaling is important.

# Computing Parameters Analytically
## Normal equations
**Idea**: Derive the optimal solution directly, instead of iterative approach.
- The basic approach is that to take a derivative and find the x in which derivative is 0.
- This is akin to finding the local minima of a function.
- The normal analytical form is the following:
\\[\theta = (X^T X)^{-1}X^T y\\]
where,
<p>\[
X =
\begin{bmatrix}
  (x^{(1)})^T \\
  (x^{(2)})^T \\
  (x^{(3)})^T \\
  \vdots \\
  (x^{(m)})^T \\
\end{bmatrix}
\in \mathbb{R}^{m \times (n+1)}
\hspace{20pt}
y =
\begin{bmatrix}
  (y^{(1)})^T \\
  (y^{(2)})^T \\
  (y^{(3)})^T \\
  \vdots \\
  (y^{(m)})^T \\
\end{bmatrix}
\in \mathbb{R}^{m}
\]</p>
- In octave: `pinv(X'*X)*X'*y`
- For normal equation, feature scaling is not necessary.
- **Pros**:
  - No need to hyperparameter tuning
  - Fast for small matrices n = ~100 to 1000
- **Cons**:
  - For large matrices, inverting matrices take a long time i.e. \\((X^T X)^{-1}\\)
  - Around 100 ~ 1000 is fine. Around ~10,000 is probably starting to get slow.
  - Runtime of inverting is \\(O(n^3)\\)
  - So, when the number of features are large \\(n\\), use gradient descent

## Normal equation non-invertability
**Idea**: what if \\(X^T X\\) is singular (non-invertible/degenerate)?
- Pseudo inversing allows computation of inverse of singular matrices. `pinv` in octave
- If \\(X^T X\\) is non-invertible:
  - linearly dependent features (redundant, reducible rows)
    - having 2 separate features that are scaled i.e. (feets and meters of same measurement)
  - too many features compared to number of input examples (e.g. \\(m \leq n\\))
    - delete, or use regularization
