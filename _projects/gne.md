---
layout: page
title: gNE 
description: Python package for geometric Neighbour Embeddings
img: assets/img/bunny.jpg
category: geometric machine learning
related_publications:
related_bibliography: gne.bib
related_repositories: https://github.com/subthaumic/gne
---

*This is work in progress, the description below will likely be subject to substantial changes.* <br>

This project introduces and explores geometric Neighbour Embeddings (gNE -- */ˈdʒ:ɪni/*, like Genie from Aladdin), a method for dimensionality reduction that aims to preserve geometric structures more faithfully than standard methods.

Similar to traditional Neighbour Embeddings like t-SNE and UMAP, gNE seeks to maintain the neighbour relationships present in high-dimensional data.
However, gNE modifies these approaches in two ways: It extends beyond pairwise affinities and instead aims to preserve geometric properties like distances, areas, and volumes of higher-order neighbour relations.
The resulting embeddings are intended to be more geometrically interpretable, such that they can facilitate downstream tasks on the low-dimensional representation, like dynamical inference.

An early implementation of these ideas is available as python package ```gNE``` [on GitHub](https://github.com/subthaumic/gne).

## 

Let $$X$$ be a finite subset of a Riemannian manifold $$(M,g_M)$$ and let $$(N,g_N)$$ be a chosen target Riemannian manifold.

We then want to find an embedding

$$
f: X \hookrightarrow (N,g_N)
$$

that tries to preserve the geometric properties of ($$k$$-nearest) neighbourhoods in $$X$$.

The higher-order neighbour relations in $$X$$ and $$Y = f(X)$$ are modeled by \textit{weighted simplicial complexes} $$(K_X, w_X)$$ and $$(K_Y, w_Y)$$.
The weight functions $$w_X$$ and $$w_Y$$ associate geometric quantities, as determined by $$g_N$$ and $$g_M$$, to each simplex.
For example distances for 1-simplices (edges), areas for 2-simplices (triangles), volumes for 3-simplices (tetrahedra).

In complete analogy to standard Neighbour Embeddings, gNE then factors through a comparison of $$(K_X, w_X)$$ and $$(K_Y, \tilde{w}_Y)$$.
The general structure of the loss function is given by a simplex-wise comparison of weights:

$$
  \mathcal{L}(K_X, K_Y) 
    = \lambda_0 \sum_{i} \mathcal{L}_0 (w_i ,\tilde w_i) 
    + \lambda_1 \sum_{i,j} \mathcal{L}_1 (w_{ij}, \tilde{w}_{ij}) 
    + \lambda_2 \sum_{i,j,k} \mathcal{L}_2 (w_{ijk}, \tilde{w}_{ijk}) 
    + \ldots
$$

Here $$\lambda_i \in \mathbb{R}$$ are hyperparameters that fix the relative importance of the simplices of various dimensionalities, $$\mathcal{L}_i$$ are loss functions (e.g. $$L^2$$), and we used abbreviations of the form $$w_{ij} = w_X({x_i,x_j})$$ and $$\tilde{w}_{ij}=w_Y({y_i,y_j})$$.


## Further Ideas

- For future purposes want to implement Hamiltonian dynamics on a given geometry. For this need tensors and differential forms.

- parametric gNE, i.e. use $$(X, d_X) \subset (M,g_M)$$ to learn a map $$f:M \to N$$ such that one can calculate $$f(x)$$ for any $$x \in M$$ that was not originally in $$X$$. As far as I understand it, this is usually done with neural nets and relies on a completely different Ansatz. Currently I do not plan to follow up on this idea.