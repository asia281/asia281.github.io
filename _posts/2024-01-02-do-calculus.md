---
layout: post
title:  Causal interference
date: 2024-01-02 00:00:00
description: Causal interference
categories: causality
toc:
  sidebar: left
---

## Rules

1. $$P(y | do(t),z,w) = P(y | do(t),w) if Y \perp _{G_T} Z | T,W$$

It's a generalization of d-separation to interventional distributions.

$$ P(y|z,w)=P(y|w) if Y \perp _G Z|W $$

2. $$P(y | do(t),do(z),w) = P(y | do(t),z,w) if Y ?GT,Z Z | T,W$$

It's a generalization of backdoor adjustment/criterion

P(y|do(z),w)=P(y|z,w) if Y ?GZ Z|W 

3. $$ P(y | do(t),do(z),w) = P(y | do(t),w) if Y \perp GT,Z(W) Z | T,W $$

where $Z(W)$ denotes the set of nodes of $Z$ that aren't ancestors of any node of $W$ in $G_T$.

$$ P(y|do(z),w)=P(y|w) if Y ?GZ(W) Z|W $$

## Examples
$$P_G(y|do(x)) = p(y)$$ if $Y$ is a non-descendant of $X$.

If $Y$ is not a parent of $X$ then
$$P_G (y | do(X = \hat{x})) = \sum_{pa_X} P(y | \hat{x}, pa_X ) p(pa_X )$$ 

Whenever we can compute the marginalized intervention distribution p(y | do(X = xˆ)) by a summation 􏰈z p(y | xˆ, z) p(z) as in (2), we call the set Z a valid adjustment set for the intervention $Y | do(X)$. We see that $Z = PA^G_X$ is a valid adjustment set for Y | do(X) (for any Y ). 