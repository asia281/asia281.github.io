---
layout: post
title:  Causal interference
date: 2024-01-01 00:00:00
description: Causal interference
tags: formatting diagrams
categories: sample-posts
toc:
  sidebar: left
---

### Sources

If you want to start your adventure with causality, I recommend to watch the videos from [Causal Inference Course](https://www.bradyneal.com/causal-inference-course){:target="_blank"}. They honestly have the best explanations of causal theory I've ever seen.

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

Forcing people in groups to change their trial type in order to make group random. It removes confounders. Graphical interpretation: removing an edge. It makes a graph satisfy backdoor criterion. Some 

If we have covariate balance ($P(X | T = 0) = P(X | T = 1)$), then assosiation is causation ($P(X | do(T)) = P (X | T)$).

## Backdoor 

# Criterion

To establish a causal relationship between X and Y, you need to collectively block (condition on) all backdoor paths that could introduce confounding. 
The backdoor criterion states that a variable set $Z$ satisfies the criterion if and only if:
1. $Z$ blocks all backdoor paths from $X$ to $Y$.
2. There are no colliders on the backdoor paths that are in the set $Z$.

We can ilustrate if as follows:
![Backdoor](/assets/img/openbackdoor.svg)

Let's do some examples. Let's consider the following graph:
![Backdoor-example](/assets/img/biasexamples.svg)

1. $X \perp T$
Y is a collider that hasn't been conditioned on.
2. $X \nperp T | Y$
Y is a collider that has been conditioned on
3. $X \nperp T | W$
W has been conditioned on, it is a descendant of a collider 
4. $Y \perp G$
5. $Y \nperp G | U$
U is a collider that has been conditioned on
6. $Y \perp G | U, T$
T is a confounder that has been conditioned on

# Adjustment


## Frontdoor criterion

Like the backdoor criterion, the front door criterion is used to identify and estimate causal relationships between variables. It is applicable when there is an unobserved or latent variable M that acts as an intermediate step between the X and the Y. 

A set of variables $M$ satisfies the frontdoor criterion relative to $T$ and $Y$ if the following are true:
1. $M$ completely mediates the effectof $T$ on $Y$ (i.e. all causal paths from T to Y go through M).
2. There is no unblocked backdoor path from T to M.
3. All backdoor paths from M to Y are blocked by T.


# Adjustment
If $Y, M, T$ satisfy criterion and we have positivity, then:
$$ P(y|do(t)) = \sum_m P(m|t) \sum _{t'} P(y|m, t')P(t') $$

