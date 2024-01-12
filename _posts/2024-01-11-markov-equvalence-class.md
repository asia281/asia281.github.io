---
layout: post
title:  Markov equivalence class
date: 2024-01-11 00:00:00
description: Why we can't discover 
categories: causality
toc:
  sidebar: left
---

## d-separation
d-separation is a criterion for deciding, from a given a causal graph, whether a set X of variables is independent of another set Y, given a third set Z. The idea is to associate "dependence" with "connectedness" (i.e., the existence of a connecting path) and "independence" with "unconnected-ness" or "separation". The only twist on this simple idea is to define what we mean by "connecting path", given that we are dealing with a system of directed arrows in which some vertices (those residing in Z) correspond to measured variables, whose values are known precisely. To account for the orientations of the arrows we use the terms "d-separated" and "d-connected" (d connotes "directional").

We start by considering separation between two singleton variables, x and y; the extension to sets of variables is straightforward (i.e., two sets are separated if and only if each element in one set is separated from every element in the other).

### Rules:

- x and y are d-connected if there is an unblocked path between them.
- If a collider is a member of the conditioning set Z, or has a descendant in Z, then it no longer blocks any path that traces this collider.
- x and y are d-connected, conditioned on a set Z of nodes, if there is a collider-free path between x and y that traverses no member of Z. If no such path exists, we say that x and y are d-separated by Z, We also say then that every path between x and y is "blocked" by Z.


## Future reading:

- [Characterization and Greedy Learning of Interventional Markov Equivalence Classes of Directed Acyclic Graphs](https://arxiv.org/pdf/1104.2808.pdf){:target="_blank"}

