---
layout: post
title:  Causal discovery
date: 2024-01-15 00:00:00
tags: git
categories: sample-posts
toc:
  sidebar: left
---

# PC-algorithm

1. The PC algorithm starts with a complete graph. In the first step all node pairs are tested for conditional independence with conditional independence tests, suspect to a certain threshold. If those tests suggest conditional independence between pairs of nodes the edges are deleted from the complete graph. 
2. Based on the results of the conditional independence tests, orient the edges in the undirected graph. If two variables A and B are found to be conditionally independent given a set C, then the edge between A and B is removed or not oriented. If no conditional independence is found, the edge is oriented from A to B or from B to A.
3. orientation rules to correctly orient edges around colliders to avoid inducing spurious relationships.


# Causal discovery
Discovering the graph G from samples of a joint distribution P is a fundamental problem in causality. While observational data alone is in general not sufficient to identify the DAG, interventional data can improve identifiability up to finding the exact graph. Finding the right DAG is challenging as the solution space grows super-exponentially with the number of variables. Commonly, methods that recover graphs from joint observational and interventional data are grouped into constraint-based and score-based approaches.

## Constraint-based 
These methods use conditional independence tests to identify causal relations.

## Score-based 
On the other hand, these methods search through the space of all possible causal structures with the goal of optimizing a specified metric. This metric, also referred to as score function, is usually a combination of how well the structure fits the data, for instance in terms of log-likelihood, as well as regularizers for encouraging sparsity. Since the search space of DAGs is super-exponential in the number of nodes, many methods rely on a greedy search, yet returning graphs in the true equivalence class

## Gradient-based discovery methods
are score-based methods that avoid the combinatorial greedy search over DAGs by using gradient-based methods. Thereby, the adjacency matrix is parameterized by weights that represent linear factors or probabilities of having an edge between a pair of nodes. The main challenge of such methods is how to limit the search space to acyclic graphs. One common approach is to view the search as a constrained optimization problem and deploy an augmented Lagrangian procedure to solve it (Zheng et al., 2018; 2020; Yu et al., 2019; Brouillard et al., 2020), including NOTEARS (Zheng et al., 2018) and DCDI (Brouillard et al., 2020). Alternatively, Ke et al. (2019) propose to use a regularization term penalizing cyclic graphs while allowing unconstrained optimization. However, the regularizer must be designed and weighted such that the correct, acyclic causal graph is the global optimum of the score function.


## ENCO [github](https://github.com/phlippe/ENCO){:target="_blank"}

In ENCO, the structural parameters for an edge (i,j) are represented by two parameters ρi,j = [θi,j , γi,j ]. Intuitively, γi,j corresponds the existence of the edge, while θi,j = −θj,i is associated with the direction of the edge

## DCDI [github](https://github.com/slachapelle/dcdi){:target="_blank"}

It combines constraint and score-based approaches. Among these, IGSP is a method that optimizes a score based on conditional independence tests. Contrary to GIES, this method has been shown to be consistent under the faithfulness assumption.

## DECI

## DiBS

## SDI