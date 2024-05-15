---
layout: post
title:  Causal interference
date: 2024-01-01 00:00:00
description: Causal interference
categories: causality
toc:
  sidebar: left
---

## Sources

If you want to start your adventure with causality, I recommend watching the videos from [Causal Inference Course](https://www.bradyneal.com/causal-inference-course){:target="_blank"}. They honestly have the best explanations of causal theory I've ever seen.

## Basic terms

### Faithfulness

The statistical dependencies inferred from observational data accurately reflect the underlying causal relationships among variables.

## How to allow identifiability? (computing from purely statistical quantities)


### Ignorability 
$$(Y(1), Y(0)) \perp T$$. 
Intuition: we ignore all missing data and compute statistics based on the data we have.

$$E(Y(1)) - E(Y(0)) = E(Y(1)|T = 1) - E(Y(0) | T = 0) = E(Y|T = 1) - E(Y|T = 0)$$

Confounding disappears after adding ignorability.

### Exchangeability:

We can swap the groups and get the same expected value. We can write it as:

$$E(Y(1) | T = 1) = E(Y(1) | T = 0)= E(Y(1))$$

Potential outcome Y is independent of treatment.

## Randomized control trial (RCT)

Forcing people in groups to change their trial type to make the group random. It removes confounders. Graphical interpretation: removing an edge. It makes a graph satisfy the backdoor criterion. Some 

If we have covariate balance ($P(X | T = 0) = P(X | T = 1)$), then assosiation is causation ($P(X | do(T)) = P (X | T)$).

## Backdoor 

### Criterion

To establish a causal relationship between X and Y, you need to collectively block (condition on) all backdoor paths that could introduce confounding. 
The backdoor criterion states that a variable set $Z$ satisfies the criterion if and only if:
1. $Z$ blocks all backdoor paths from $X$ to $Y$.
2. There are no colliders on the backdoor paths in the set $Z$.

We can illustrate if as follows:
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

### Adjustment


## Frontdoor 

### Criterion

Like the backdoor criterion, the front door criterion identifies and estimates causal relationships between variables. It is applicable when an unobserved or latent variable M acts as an intermediate step between the X and the Y. 

A set of variables $$M$$ satisfies the frontdoor criterion relative to $$T$$ and $$Y$$ if the following are true:
1. $$M$$ completely mediates the effect of $$T$$ on $$Y$$ (i.e., all causal paths from T to Y go through M).
2. There is no unblocked backdoor path from T to M.
3. All backdoor paths from M to Y are blocked by T.


### Adjustment
If $$Y, M, T$$ satisfy the criterion and we have positivity, then:
$$ P(y|do(t)) = \sum_m P(m|t) \sum _{t'} P(y|m, t')P(t') $$


# Other criterions

**Necessary criterion:** For each backdoor path from $$T$$ to any child $$M$$ of $$T$$ that is an ancestor of $$Y$$, we must block the path. It's not a sufficient criterion.

**Unconfounded children criterion**: All backdoor paths from the treatment variable T to all of its children that are ancestors of Y with a single conditioning set must be blocked. Sufficient when T is a single variable. 

![Backdoor-example](/assets/img/unconfounded_child.png)

# Currently, we usually try to solve one of the following problems:

1. **Causal inference**: How much would some specific variables (features or the label) change if we manipulate the value of another particular variable? 

2. **Causal discovery**: By modifying the value of which variables, could we change the value of another variable?

# Propensity score 

$$e(w) = P(T=1 | W)$$

e is only 1-dimensional

Given positivity:

$$(Y(0), Y(1)) \perp T | W \arrow (Y(0), Y(1)) \perp T | e(W)$$