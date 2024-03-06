---
layout: page
title: gNE 
description: Python package for geometric Neighbour Embeddings
img: assets/img/bunny.jpg
category: geometric machine learning
---


Let $$X$$ be a finite subset of a Riemannian manifold $$(M,g_M)$$ and let $$(N,g_N)$$ be a chosen target Riemannian manifold. Denote by $$\phi, \psi: \mathbb{R}_{\geq 0} \to [0,1]$$ two proximity functions, i.e. functions that map distances $$d_M(x_i,x_j)$$ and $$d_N(y_i,y_j)$$ to proximities/similarities.[^1]

gNE (*/ˈdʒ:ɪni/*, like Genie from Aladdin) then finds an embedding

$$
f: X \hookrightarrow (N,g_N)
$$

that tries to preserve neighbour proximities: $$\phi( d_M(x_i, x_j) ) \simeq \psi(d_N(y_i,y_j))$$ by minimizing a specified Loss function $$\mathcal{L}(\phi(X), \psi(Y))$$, where $$Y=f(X)$$. By default this is cross entropy (or equivalently Kullback-Leibler divergence, since $$\phi(d_M(x_i,x_j))$$ is constant)

$$
\mathcal L_{\mathrm{KL}}(X,Y) = - \sum_{i,j} \phi(d_M(x_i,x_j)) \log \psi(d_N(y_i,y_j))
$$

$$(X,\phi)$$ can be viewed as a complete weighted graph. Instead, as is typical in neighbourhood embeddings, gNE by default considers only the kNN-Graph weighted by the proximities determined by $$\phi$$.[^2]

## Features

- Model geometries (Euclidean, Hyperbolic, Sphere, SPD, and their products)
- Custom geometries via specification of Riemannian metric $$g_M$$, specified in some high dimensional $$\mathbb{R}^n$$. Get geodesic distances from this.
  (available: Sasakian metric on tangent bundle)
- Finite metric spaces $$(X,d_X)$$
- Weighted graphs $$(G,w_G)$$
- Standard maps from finite metric space$$(X,d_X)$$  to e.g. weighted kNN-Graph, VR-Graph, ...
- Loss functions for graphs and complexes (available: Cross Entropy, Kullback-Leibler, their symmetrization, ...)

- Choice of proximity function $$\phi$$ (available: Gaussian, Laplace, t-distribution, ...)
- Offers choice of point on attraction-repulsion spectrum (available : t-SNE, UMAP-like choices on attraction-repulsion spectrum

## Standard pipeline of gNE

model(source geometry, target geometry)
model(X)

## Further Ideas

- provide an implementation for weighted complexes! In the loss function can e.g. use generalization from sum over edges $$\sum_{i,j} = \sum_{e}$$ to a sum over all simplices. In that case minimizing the loss function should not only keep pairwise proximities similar, but also keep n-ary proximities.
  Note that in analogy of loss function for edges, one can ask about geometric properties of higher simplices, e.g. area or volume of the simplex in target space. 
  Needs implementation of
	- Weighted complexes $$(C,w_C)$$
	- Standard maps to produce kNN-Complex, VR-Complex, ... from $$(X,d_X)$$
	- Loss function for weighted complexes


- For future purposes want to implement Hamiltonian dynamics on a given geometry. For this need tensors and differential forms.

- parametric gNE, i.e. use $$(X, d_X) \subset (M,g_M)$$ to learn a map $$f:M \to N$$ such that one can calculate $$f(x)$$ for any $$x \in M$$ that was not originally in $$X$$.



---

[^1]:  According to %Bohm2022 the choice doesn't really matter, so could probably hard-code it to be the Cauchy similarity kernel

$$
\phi(d(x_i,x_j)) = \frac{1}{1+a d(x_i, x_j)^{2b}}
$$

[^2]: Again, the choice of proximity kernel seems to be ultimately irrelevant. Typically one either uses a Gaussian kernel or binary adjacencies (in either case normalized such as to obtain a probability distribution).