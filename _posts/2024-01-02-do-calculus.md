---
layout: post
title:  Causal interference
date: 2024-01-02 00:00:00
description: Causal interference
tags: formatting diagrams
categories: sample-posts
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