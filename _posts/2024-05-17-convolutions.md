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

Convolutional neural networks (CNNs) are specifically designed to deal with this problem. 

## Why convolution is called convolution?

