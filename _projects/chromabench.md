---
layout: page
title: chromabench
description: A minimal validation benchmark for chromatic topological data analysis
category: applied topology
related_repositories: https://github.com/subthaumic/chromabench
---

`chromabench` is the simplest check that a topological method meant to read both the *shape* and the *colour distribution* of a point cloud actually does.

It is a 2x2 family of two-colour point clouds: two spatial distributions, *uniform* or *cluster*, each with the two colours either *mixed* or *separated*.
The mixed and separated versions are sampled from the **same** distribution, so only the colour distribution tells them apart.

## The task

The four classes factor as **spatial distribution** $$\times$$ **colour distribution**:

$$
\{\texttt{uniform}, \texttt{cluster}\} \times \{\texttt{mixed}, \texttt{separated}\}.
$$

Given a labelled point cloud -- coordinates *and* colours -- a method predicts its class. Scoring is balanced accuracy under stratified 10-fold cross-validation (chance $$= 0.25$$ for the four balanced classes).

## The colour-blind baseline

Ordinary persistent homology of the pooled points (colours discarded) depends only on the spatial layout. Since the mixed and separated members of a class share the same point positions, they are *topologically identical* to PH.
Alpha-complex PH in dimensions 0 and 1, vectorized by persistence-images, with a multinomial logistic regression perfectly resolves `uniform` vs `cluster` but has to guess on `mixed` vs `separated`. Beating it requires actually using colour.

## Usage sketch

```python
from chromabench import load_dataset, evaluate, run_baseline

ds = load_dataset()                          # 4 classes x 100 two-colour point clouds, seed 42
print(run_baseline(ds)["score"])             # colour-blind PH reference (~0.47)
print(evaluate(MyChromaticMethod(), ds)["score"])   # your colour-aware method
```

A method is any object with `fit(samples, y)` and `predict(samples)`.

## Learn more
- Source code & issue tracker: [github.com/subthaumic/chromabench](https://github.com/subthaumic/chromabench)
