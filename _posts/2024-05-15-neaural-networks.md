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