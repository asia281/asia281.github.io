---
layout: post
title: Linear regression
date: 2024-05-15 08:00:00
description: Introduction of linear regression
tags: interview
categories: sample-posts
toc:
  sidebar: left
---

# Linear regression

We assume that the relationship between the independent variables $x$ and the dependent variable $y$ is linear, i.e., that $y$ can be expressed as a weighted sum of the elements in $x$, given some noise on the observations. Second, we assume that any noise is well-behaved (following a Gaussian distribution).

Given a dataset, our goal is to choose the weights $w$ and the bias $b$ such that on average, the predictions made according to our model best fit the true prices observed in the data. 

$$ \hat{y} = w_1x_1 + ... + w_dx_d + b $$

$$ \hat{y} = w^T x + b $$

### Loss function

Before we start thinking about how to fit data with our model, we need to determine a measure of fitness. The loss function quantifies the distance between the real and predicted value of the target. The loss will usually be a non-negative number where smaller values are better and perfect predictions incur a loss of 0. The most popular loss function in regression problems is the MSE:

$$ L(w, b) = \frac{\hat{y} - y}{2n} = \frac{w^T x + b - y}{n} $$

When training the model, we want to find parameters $(w^*, b^*)$ that minimize the total loss across all training examples:

$$ w^*, b^* = \text{argmin}_{w, b} L(w, b) $$

### Analytic solution

To start, we can subsume the bias $b$ into the parameter $w$
by appending a column to the design matrix consisting of all ones. Then our prediction problem is to minimize $||y - w^Tx||$. There is just one critical point on the loss surface and it corresponds to the minimum of the loss over the entire domain. Taking the derivative of the loss with respect to $w$ and setting it equal to zero yields the analytic (closed-form) solution:

$$ w^* = (X^TX)^{-1} X^T y $$

While simple problems like linear regression may admit analytic solutions, you should not get used to such good fortune. Although analytic solutions allow for nice mathematical analysis, the requirement of an analytic solution is so restrictive that it would exclude all of deep learning.

### Minibatch stochastic gradient descent

The key technique for optimizing nearly any deep learning model, and which we will call upon throughout this book, consists of iteratively reducing the error by updating the parameters in the direction that incrementally lowers the loss function. This algorithm is called gradient descent. 
The most naive application of gradient descent consists of taking the derivative of the loss function, which is an average of the losses computed on every single example in the dataset. In practice, this can be extremely slow: we must pass over the entire dataset before making a single update. Thus, we will often settle for sampling a random minibatch of examples every time we need to compute the update, a variant called minibatch stochastic gradient descent.

In each iteration, we first randomly sample a minibatch $B$ and compute:

$$ (w, b) \leftarrow (w-b) - \frac{\alpha}{|B|} \sum_{i \in B} \nabla_{w, b} L^{(i)} (w, b) $$

For quadratic loss we can write:

$$ w \leftarrow w - \frac{\alpha}{|B|} \sum_{i \in B} x^{(i)} (w^T x^{(i)} + b - y^{(i)}) $$
$$ b \leftarrow b - \frac{\alpha}{|B|} \sum_{i \in B} (w^T x^{(i)} + b - y^{(i)}) $$

Linear regression happens to be a learning problem where there is only one minimum over the entire domain. However, for more complicated models, like deep networks, the loss surfaces contain many minima. Fortunately, for reasons that are not yet fully understood, deep learning practitioners seldom struggle to find parameters that minimize the loss on training sets. The more formidable task is to find parameters that will achieve low loss on data that we have not seen before, a challenge called generalization. 

### Gaussian distribution

One way to motivate linear regression with the mean squared error loss function (or simply squared loss) is to formally assume that observations arise from noisy observations, where the noise is normally distributed as follows:

$$ y = w^T x + b + \epsilon $$

where $\epsilon$ is sampled from normal distribution with mean $0$ and standard deviation $\sigma^2$.
Thus, we can now write out the likelihood of seeing a particular $y$ for a given $x$ via

$$ P(y | x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp(-\frac{1}{2\sigma^2}) (y - w^Tx - b)^2 $$

Now, according to the principle of maximum likelihood, the best values of parameters $w$ and $b$ are those that maximize the likelihood of the entire dataset:

$$ P(y|X) = \prod_{i=1}^n p(y^{(i)} | x^{(i)}) $$

Estimators chosen according to the principle of maximum likelihood are called maximum likelihood estimators. While, maximizing the product of many exponential functions might look difficult, we can simplify things significantly, without changing the objective, by maximizing the log of the likelihood instead. For historical reasons, optimizations are more often expressed as minimization rather than maximization. So, without changing anything we can minimize the negative log-likelihood $-\log P(y|X)$ by:

$$ -\log P(y|X) = \sum_{i = 1}^n \frac{1}{2} \log(2\pi\sigma^2) + \frac{1}{2\sigma^2} (y - w^Tx - b)^2$$

It follows that minimizing the mean squared error is equivalent to maximum likelihood estimation of a linear model under the assumption of additive Gaussian noise.
