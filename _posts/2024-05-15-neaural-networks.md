---
layout: post
title: Neural networks
date: 2024-05-15 08:15:00
description: Introduction to neural networks
tags: interview
categories: sample-posts
toc:
  sidebar: left
---

# Neural networks

Let's start with the notation. If the inputs of NN are $x_1, x_2, ..., x_d$ x, the \textit{number of inputs} (or \textit{feature dimensionality}) in the input layer is $d$. If output of the network is $o_1$, the \textit{number of outputs} in the output layer is 1. Every network has fixed \textit{number of layers} 

## Multi-layer perceptron
The simplest deep networks are called multilayer perceptrons, and they consist of multiple layers of neurons each fully connected to those in the layer below (from which they receive input) and those above. When we train high-capacity models we run the risk of overfitting. Thus, we will need to provide your first rigorous introduction to the notions of overfitting, underfitting, and model selection. To help you combat these problems, we will introduce regularization techniques such as weight decay and dropout. We will also discuss issues relating to numerical stability and parameter initialization that are key to successfully training deep networks. 

### Hidden layers and activation
By introducing more hidden layers we can overcome the monotonicity and handle more complex functions. It's also important to add activation functions to be applied after each hidden unit following the matrix multiplication. It's added in order to make MLP not collapse into linear model. It's only possible to use (at least one-hand-side) differentiable function to use gradient descent. The most commonly used activation functions are:

#### Rectified linear unit (ReLU)
Defined as:

$$ ReLU(x) = max(0, x) $$

It keeps only non-negative values of the function.

#### Sigmoid

$$sigmoid(x) = \frac{1}{1 + \exp(-x)}$$

Squashes interval $(-\inf, \inf)$ to $(0, 1)$.

#### Tanh 

$$\tanh(x) = \frac{1 - \exp(-2x)}{1 + \exp(-2x)}$$

Also squashes interval $(-\inf, \inf)$, but this time to $(-1, 1)$. Note that as the input nears $0$, the tanh function approaches a linear transformation. 

## Model Selection

When we train our models, we attempt to search for a function that fits the training data as well as possible. If the function is so flexible that it can catch on to spurious patterns just as easily as to true associations, then it might perform too well without producing a model that generalizes well to unseen data. This is precisely what we want to avoid or at least control. 

With MLPs we may wish to compare models with different numbers of hidden layers, different numbers of hidden units, and various choices of the activation functions applied to each hidden layer. In order to determine the best among our candidate models, we will typically employ a validation dataset.

### K-Fold Cross Validation
This set is taken from train dataset in order to check if our model generalise on unseen data. Sometimes we don't have enough data to split affort giving up some of its part for validation. Popular solution to this problem is splitting the original dataset into $K$ non-overlapping subsets, and then train and evaluate model $K$ times, each time on different validation subset. To get the final train and validation errors we average the results from all experiments.


### Underfitting and Overfitting
The other big consideration to bear in mind is the dataset size. Fixing our model, the fewer samples we have in the training dataset, the more likely (and more severely) we are to encounter overfitting. On the other hand if we have too simple model, we may not fit the data good enough.

Many of the techniques in deep learning are heuristics and tricks aimed at guarding against overfitting.

#### Weight decay
Weight decay (commonly called $L_2$ regularization or ridge), might be the most widely-used technique for regularizing parametric machine learning models. The technique is motivated by the basic intuition that among all functions $f$, the function $f = 0$ is in some sense the simplest, and that we can measure the complexity of a function by its distance from zero. To achieve that, we add penalizing term $\lambda ||w||^2$. 

 In probabilistic terms, we could justify this technique by arguing that we have assumed a prior belief that weights take values from a Gaussian distribution with mean zero. More intuitively, we might argue that we encouraged the model to spread out its weights among many features rather than depending too much on a small number of potentially spurious associations.

One reason to work with the $L_2$ norm is that it places an outsize penalty on large components of the weight vector. This biases our learning algorithm towards models that distribute weight evenly across a larger number of features. In practice, this might make them more robust to measurement error in a single variable. By contrast, $L_1$ penalties lead to models that concentrate weights on a small set of features by clearing the other weights to zero. This is called feature selection, which may be desirable for other reasons.

#### Dropout
In standard dropout regularization, one debiases each layer by normalizing by the fraction of nodes that were retained (not dropped out). In other words, with dropout probability p, each intermediate activation h is replaced by a $0$ with a probability $p$ and $\frac{h}{1-p}$ otherwise. Notice that expectation remains unchanged. In practice dropout means removing an existing edge between neurons with a probability $p$. 

## Vanishing and exploding gradients

we are susceptible to the same problems of numerical underflow that often crop up when multiplying together too many probabilities. When dealing with probabilities, a common trick is to switch into log-space, i.e., shifting pressure from the mantissa to the exponent of the numerical representation. Unfortunately, our problem above is more serious: initially the matrices may have a wide variety of eigenvalues. They might be small or large, and their product might be very large or very small.

 We may be facing parameter updates that are either (i) excessively large, destroying our model (the exploding gradient problem); or (ii) excessively small (the vanishing gradient problem), rendering learning impossible as parameters hardly move on each update.

 ### Issue with sigmoid
 The sigmoid’s gradient vanishes both when its inputs are large and when they are small. Moreover, when backpropagating through many layers, unless we are in the Goldilocks zone, where the inputs to many of the sigmoids are close to zero, the gradients of the overall product may vanish. Consequently, ReLUs, which are more stable (but less neurally plausible), have emerged as the default choice for practitioners.

### Initialization

These issues may decrese if we intitialize weights properly. The most common is Xavier Initialization.