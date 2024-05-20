---
layout: post
title: Linear regression
date: 2024-05-15 08:10:00
description: Introduction of linear regression
tags: interview
categories: sample-posts
toc:
  sidebar: left
---

# Softmax regression

Softmax because soft approximation of max. This sort of generalizes sigmoid regression. But in sigmoid regression we only train one regression, and not two!

Sometimes we want to classify the the object rather that regress. In ML we often do soft assignments, i.e., to assess the probability that each category applies.

## One-hot encoding
Let's consider the example. Consider features (at this point treat them as a black-box) based on which you want to classify is the pet is a cat, dog, or chicken, indicate them as a classes: 0, 1, 2.  
General classification problems do not come with natural orderings among the classes. Fortunately, statisticians long ago invented a simple way to represent categorical data: the one-hot encoding. A one-hot encoding is a vector with as many components as we have categories. The component corresponding to particular instance’s category is set to 1 and all other components are set to 0. In our case, a label $y$ would be a three-dimensional vector, with $(1, 0, 0)$ corresponding to “cat”, $(0, 1, 0)$ to dog, and $(0, 0, 1)$ to chicken. Assume that later on all labels will be one-hot-encoded.

## Intro 

In order to estimate the conditional probabilities associated with all the possible classes, we need a model with multiple outputs, one per class. To address classification with linear models, we will need as many affine functions as we have outputs. Each output will correspond to its own affine function. In our case, since we have 4 features and 3 possible output categories, we will need 12 scalars to represent the weights $w$, and 3 scalars to represent the biases $b$. You can write a classification problem as:

$$o_0 = x_0 w_{0, 0} + x_1 w_{0, 1} + x_2 w_{0, 2} + x_3 w_{0, 3} + b_0$$
$$o_1 = x_1 w_{1, 0} + x_1 w_{1, 1} + x_2 w_{1, 2} + x_3 w_{1, 3} + b_1$$
$$o_2 = x_2 w_{2, 0} + x_1 w_{2, 1} + x_2 w_{2, 2} + x_3 w_{2, 3} + b_2$$

We can also put all the weights in a matrix $W$ with a shape $3 \times 4$, biases, inputs and outputs into vectors $B$, $X$ and $O$ with a shape $3 \times 1$. The equation will look the following:

$$ O = X W + B $$

The neural network looks as follows:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/nn_softmax.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

## Softmax operation
The main approach that we are going to take here is to interpret the outputs of our model as probabilities. We will optimize our parameters to produce probabilities that maximize the likelihood of the observed data. Then, to generate predictions, we will choose the label with the maximum predicted probabilities.


Logits are the outputs of a neural network before the activation function is applied. We can't use them as probabilities, as they can sum up to not 1 or be negative. We must guarantee then that logits will be nonnegative, sum up to 1 and be "proportional" to the logits. That's why we use softmax:

$$ softmax(o)_i = \frac{\exp(o_i)}{\sum_{j} \exp(o_j)}  $$

Notice that $ \underset{i}{\operatorname{argmax}} o_i = \underset{i}{\operatorname{argmax}} softmax(o)_i$.


# Log-likelihood
We need a loss function to measure the quality of our predicted probabilities. We will rely on maximum likelihood estimation.
The softmax function gives us a vector $\hat{y}$ which we can interpret as estimated conditional probabilities of each class given any input. 


## Cross-entropy loss
We can compare the reality with the estimates maximising likelihood estimation, by minimising the negative log-likelihood:

$$ -\log P(Y | X) = \sum_{i=1}^n -\log P(y^{(i)} | x^{(i)}) = -\sum_{i=1}^n y_j\log \hat{y_j} = -\sum_{i=1}^n y_j\log  \frac{\exp(o_i)}{\sum_{j} \exp(o_j)} $$

Since $y$ is a one-encoded vector, the sum is nonzero for one term.  It is the expected value of the loss for a distribution over labels.



## Softmax vs derivatives