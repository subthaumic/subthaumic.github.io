---
layout: page
title: Directed Spaces as Feature Representations
description: Exploring the use of directed simplicial complexes to understand feature representations in neural networks.
img: assets/img/dsc.png
related_publications: 
category: applied topology
---

Neural nets don’t just light up single neurons for single ideas, they route computation through small, reusable subcircuits.  
In this project I model those causal dependencies as **directed simplicial complexes (DSCs)** so that feature representations become geometric and causal objects.

**Core idea.**  
We can treat an MLP as a (non-stochastic) structural causal model and build DSCs from **coherent counterfactual ablations** by "gently" lowering the activation of a neuron (or a set of neurons) along valid activation trajectories and tracking which other neurons consistently respond.
A directed simplex $$(P \to q)$$ is added when the ablation of predictors $$P$$ has a statistically consistent effect on target $$q$$ across a batch.

**What I am trying to capture with this approach.**  
- *Polysemanticity*: the same neuron appears in multiple directed simplices/complexes.  
- *Polytopicity*: features spread over higher-dimensional/higher-order structures.
- *Directionality*: influence, not just co-activation.

**How I study it.**  
DSCs are built from the observed activations for a given set of inputs, and then the influence of lowering the activation of a neuron (or set of neurons) is measured by the change in activation of other neurons. This allows us to construct a directed simplicial complex that captures the causal relationships between neurons in the network, across various layers, backwards and forwards, and in different contexts.

**Toy result (quadrants).**  
A “monosemantic” network yields clean, compositional DSCs: axes detectors combine into quadrant motifs.  
A bottlenecked “polysemantic” variant shows overlapping motifs and inhibitory links that only surface under coherent ablations—exactly the kind of tangled reuse we expect.

**Why it matters.**  
This bridges interpretability, causal inference, and TDA.  
We get summaries of *which group of neurons does what, in which direction, under which context*, collecting neuron behaviour across the whole network.

**Further reading & status.**  
An informal description is available in my blog post: [The Tangled Web They Weave](https://open.substack.com/pub/subthaumic/p/the-tangled-web-they-weave).  
Preprint on [arXiv](https://arxiv.org/abs/2611.00786); code, networks and results are in [neural-dsc](https://github.com/subthaumic/neural-dsc).
As always, feedback very much welcome!