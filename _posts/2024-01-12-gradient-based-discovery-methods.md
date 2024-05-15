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

1. The PC algorithm starts with a complete graph. In the first step, all node pairs are tested for conditional independence with conditional independence tests suspected to a certain threshold. If those tests suggest conditional independence between pairs of nodes, the edges are deleted from the complete graph. 
2. Based on the results of the conditional independence tests, orient the edges in the undirected graph. If two variables, $$A$$ and $$B$$, are found to be conditionally independent given a set C, then the edge between A and B is removed or not oriented. If no conditional independence is found, the edge is oriented from A to B or B to A.
3. orientation rules to correctly orient edges around colliders to avoid inducing spurious relationships.


# Causal discovery
Discovering the graph G from samples of a joint distribution P is a fundamental problem in causality. While observational data alone is insufficient to identify the DAG, interventional data can improve identifiability up to finding the exact graph. Finding the right DAG is challenging as the solution space grows super-exponentially with the number of variables. Methods that recover graphs from joint observational and interventional data are commonly grouped into constraint-based and score-based approaches.

## Constraint-based 
These methods use conditional independence tests to identify causal relations.

## Score-based 
On the other hand, these methods search through the space of all possible causal structures to optimize a specified metric. This metric, also referred to as score function, is usually a combination of how well the structure fits the data, for instance, in terms of log-likelihood and regularizers for encouraging sparsity. Since the search space of DAGs is super-exponential in the number of nodes, many methods rely on a greedy search yet return graphs in the true equivalence class.

## Gradient-based discovery methods
are score-based methods that avoid the combinatorial greedy search over DAGs using gradient-based methods. The adjacency matrix is parameterized by weights representing linear factors or probabilities of having an edge between a pair of nodes. The main challenge of such methods is limiting the search space to acyclic graphs. One common approach is to view the search as a constrained optimization problem and deploy an augmented Lagrangian procedure to solve it (Zheng et al., 2018; 2020; Yu et al., 2019; Brouillard et al., 2020), including NOTEARS (Zheng et al., 2018) and DCDI (Brouillard et al., 2020). Alternatively, Ke et al. (2019) propose using a regularization term to penalize cyclic graphs while allowing unconstrained optimization. However, the regularizer must be designed and weighted such that the correct, acyclic causal graph is the global optimum of the score function.
# Classical discovery methods

## PC

## FCI


# Gradient-based discovery methods

## ENCO [github](https://github.com/phlippe/ENCO){:target="_blank" rel="noopener noreferrer"}

In ENCO, the structural parameters for an edge $$(i,j)$$ are represented by two parameters $$\rho _{i,j} = [θi,j , \gammai,j ]$$. Intuitively, $$\gamma_{i,j}$$ corresponds to the existence of the edge, while $$θi,j = −θj,i$$ $ is associated with the edge's direction. It has 2 steps:

1. **Distribution fitting** trains a neural network fφi per variable $$X_i$$ parameterized by φi to model its observational, conditional data distribution $$p(X_i|...)$$. The input to the network is all other variables, $$X_{-i}$$. For simplicity, we want this neural network to model the conditional of the variable $$X_i$$ concerning any possible set of parent variables. We, therefore, apply a dropout-like scheme to the input to simulate different sets of parents. In that case, during training, we randomly set an input variable Xj to zero based on the probability of its corresponding edge $$X_j \arrow X_i$$, and minimize
$$min E_X E_M [−logfφi(Xi;M−i ⊙X−i)]$$ 

where $$M_j ∼ Ber(p(X_j \arrow X_i))$$


2. **Graph fitting** uses the learned networks to score and compare different graphs on interventional data. For parameterizing the edge probabilities, we use two sets of parameters: $$\gamma \in R^{N \times N}$$ represents the existence of edges in a graph, and $$θ \in R^{N \times N}$$ the orientation of the edges. The likelihood of an edge is determined by $$p(X_i \arrow Xj ) = \sigma(\gamma_{ij} ) · σ(θij )$$

3. **Prediction**: Alternating between the distribution and graph fitting stages allows us to fine-tune the neural networks to the most probable parent sets along the training. After training, we obtain a graph prediction by selecting the edges for which σ(γij ) and σ(θij ) are greater than 0.5. The orientation parameters prevent loops between any two variables since σ(θij) can only be greater than 0.5 in one direction.

## NOTEARS [github](https://github.com/xunzheng/notears){:target="_blank"}

The basic DAG learning problem is formulated as follows: Let X ∈ Rn×d be a data matrix consisting of n i.i.d. observations of the random vector $$X = (X_1, . . . , X_d)$$ and let D denote the (discrete) space of DAGs $$G = (V, E)$$ on d nodes. Given X, we seek to learn a DAG G ∈ D (also called a Bayesian network) for the joint distribution $$P(X)$$. We model X via a structural equation model (SEM) defined by a weighted adjacency matrix W ∈ Rd×d. Thus, instead of operating on the discrete space D, we will operate on Rd×d, the continuous space of d × d real matrices.

Any W ∈ Rd×d defines a graph on d nodes in the following way: Let A(W) ∈ {0,1}d×d be the binary matrix such that [A(W )]ij = 1 ⇐⇒ wij ̸= 0 and zero otherwise. Let's treat W as if it were a (weighted) graph. G(W) but also W =[w1|···|wd] defines a linear SEM by $$X_j =w_j^T X+z_j$$,whereX = (X1, . . . , Xd) is a random vector and z = (z1, . . . , zd) is a random noise vector. We do not assume that z is Gaussian. More generally,we can modelXj via a generalized linear model(GLM) $$E(X_j|X_{pa(X_j)})=f(w_j^T X)$$. For example, if $$X_j$$ binary, we can model the conditional distribution of $$X_j$$ given its parents via logistic regression.

Since we are interested in learning a sparse DAG, we add l1-regularization:

$$F(W) = 1/2n - ||X−XW||^2_F +\lambda ||W||_1$$


Theorem 1. A matrix W ∈ Rd×d is a DAG if and only if
$$h(W ) = tr(exp(W \times W)) − d = 0 $$
where $$\times$$ is the Hadamard product and $$e^A$$ is the matrix exponential of $$A$$. Moreover, $$h(W)$$ has a simple gradient
$$\nabla h(W) = (exp(W\times W)) ^T \ties 2W$$

There were some statements that [NOTEARS isn't suitable for CGP](https://arxiv.org/pdf/2104.05441.pdf){:target="_blank"}, for which they demonstrated a lack of scale-invariance. 

## DCDI [github](https://github.com/slachapelle/dcdi){:target="_blank"}

It combines constraint and score-based approaches. Among these, IGSP is a method that optimizes a score based on conditional independence tests. Contrary to GIES, this method is consistent under the faithfulness assumption.



## DECI

## DiBS

## SDI

