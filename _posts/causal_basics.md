---
layout: post
title:  Causal interference
date: 2023-12-12 00:00:00
description: Causal interference
tags: formatting diagrams
categories: sample-posts
---
What is the primary question of causal interference?

# Why is association not causation?

## How to allow identifiability? (computing from purely statistical quantities)

Ignorability: (Y(1), Y(0)) independent T. Intuition: we ignore all missing data and compute statistics based on data we have.

$$E(Y(1)) - E(Y(0)) = E(Y(1)|T = 1) - E(Y(0) | T = 0) = E(Y|T = 1) - E(Y|T = 0)$$

Confounding disappears after adding ignorability.

# Exchangeability:

We can swap the groups and we'll get the same expected value. We can write it as:

$$E(Y(1) | T = 1) = E(Y(1) | T = 0)= E(Y(1))$$

Potential outcome Y is independent from treatment.

## Ranomized control trial (RCT)

Forcing people in groups to change their trial type in order to make group random. It removes confounder. Graphical interpretation: removing an edge.

## Backdoor criterion