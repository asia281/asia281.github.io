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

# Convolutions
Until now simply discarded each image’s spatial structure by flattening them into one-dimensional vectors, feeding them through a fully-connected MLP. Because these networks are invariant to the order of the features, we could get similar results regardless of whether we preserve an order corresponding to the spatial structure of the pixels or if we permute the columns of our design matrix before fitting the MLP’s parameters.

Convolutional neural networks (CNNs) are specifically designed to deal with this problem.  The convolutional layer picks windows of a given size and weighs intensities according to the filter $V$. Usually the image is represented by $3$ channels 

## Why convolution is called convolution?
Convolution between two functions is:

$$ (f \cdot g)(x) = \int f(x) g(z - x) dx $$

Doing convolution measures the overlap between $f$ and $g$, when one function is shifted by $x$.

## Padding and stride
Assuming that the input shape is $(n_h, n_w)$ and the convolution kernel shape is $(k_h, k_w)$, then the output shape will be $(n_h - k_h + 1, n_w - k_w + 1)$. 

If we start with a $(240 \times 240)$ pixel image, $10$ layers of $(5 \times 5)$ convolutions reduce the image to $(200 \times 200)$ pixels, slicing off $30%$ of the image and with it obliterating any interesting information on the boundaries of the original image. Padding is the most popular tool for handling this issue.

Padding is basically adding empty pixels to the boundaries of images. 

Sometimes we want to reduce dimentionaly radically, then we use stride. It's the amount of cells we want to move the window. 

## Pooling
Usually average or max pooling. Consist of a fixed-shape window that is slid over all regions in the input according to its stride, computing a single output for each location traversed by the fixed-shape window (sometimes known as the pooling window).

## Batch Normalization

Batch Norm helps with convergence. Formally, for minibatch $B$:

$$BN(x) = \gamma \frac{x - \mi_B}{\simga_B} + \beta$$

Usage for fully-connected layers and convolutional layers is slightly different. For FF it's:

$$ h = activation(BN(Wx + b)) $$

When the convolution has multiple output channels, we need to carry out batch normalization for each of the outputs of these channels, and each channel has its own scale and shift parameters, both of which are scalars. Assume that our minibatches contain $m$ examples and that for each channel, the output of the convolution has height $p$ and width $q$. For convolutional layers, we carry out each batch normalization over the $mpq$ elements per output channel simultaneously. Thus, we collect the values over all spatial locations when computing the mean and variance and consequently apply the same mean and variance within a given channel to normalize the value at each spatial location.

# Modern models


## Alexnet

AlexNet won Image contest in 2012. AlexNet is much deeper than the comparatively small LeNet5. AlexNet consists of eight layers: five convolutional layers, two fully-connected hidden layers, and one fully-connected output layer. Second, AlexNet used the ReLU instead of the sigmoid as its activation function. Let us delve into the details belo

## VGG
The basic building block of classic CNNs is a sequence of the following: (i) a convolutional layer with padding to maintain the resolution, (ii) a nonlinearity such as a ReLU, (iii) a pooling layer such as a maximum pooling layer. One VGG block consists of a sequence of convolutional layers, followed by a maximum pooling layer for spatial downsampling. 

## ResNet
The idea is to add the connection ommiting the block, ie identity function from the input to be added before activation. 

# Reccurent Neural Networks

In short, while CNNs can efficiently process spatial information, recurrent neural networks (RNNs) are designed to better handle sequential information. RNNs introduce state variables to store past information, together with the current inputs, to determine the current outputs.