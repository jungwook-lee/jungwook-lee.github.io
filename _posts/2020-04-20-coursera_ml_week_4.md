---
layout: single
title:  "Andrew Ng's Machine Learning Course - Week 4"
date:   2020-04-20
categories: coursera machine_learning
---
# Non-linear Hypothesis

## Motivation
- Neural networks are able to learn complex non-linear hypothesis
- With large combination of features (polynomials), it is very easy to overfit
- For application such as computer vision for task i.e. classification
  - there are too many input features
  - (i.e. image size (500px x 500px = 250,000 features))
- Quadratic forms of features explode the number of features to \\(O(\frac{n^2}{2})\\)

*Neurons and the Brain*:
- Origin: "Algorithms to mimic the brain"
- Widely used 80's and early 90's, dimished late 90's
- Recent resurgence in deep learning

# Neural Networks
![](https://cdn.hswstatic.com/gif/brain-neuron-a.gif)
- Dendrites: input wire
- Axon: output wire
- Communicate using pulses of electricity
- Artificial neural network uses logistic unit

- \\(x_0\\) is the bias neuron (always 1)
- logistic/sigmoid activation function
- in Neural network literature, "weights" and "parameters" are same
- "First" layer is also known as "input" layer
- "Final" layer is also known as "output" layer
- layers in between are called "hidden" layer
- **Note**: there are extra bias terms for every layer
- Notations:
  - \\(a_i^{(j)}\\) = activation of unit \\(i\\) in layer \\(j\\)
  - \\(\Theta^{(j)}\\) = matrix of weights controlling function mapping from layer\\(j\\) to \\(j+1\\)

![](/assets/images/ann.png)

- Forward propagation: calculating \\(h_\Theta(x)\\) from input vector \\(x\\)
- **Intuition**: The middle activation output parameters are learned to map \\(x\\) to a certain non-linear function which optimize for the given task. (Inside the hidden layers)

# Applications
- Note: sigmoid(x < -4.0) is around 0.01
  - sigmoid(x > 4.0) is around 0.99
- Simple 2 input ANN with 1 hidden layer can learn gate functions (i.e. AND, OR)
- Learning XNOR classification using linear basis is not possible
- Neural networks learn more complicated function as the layers go deeper

## Multiclass Classification
- Output layer outputs values with same dimensions as the output classes \\(h_\Theta \in R^{N+1}\\)
  - The extra 1 is the negative class (i.e. in image detection background)
- Take training labels and convert them to one-hot vectors

# Learning

## Cost Function and Backprop

## Backprop in Practice

## Applications 
- Random Initialization: symmetry breaking
