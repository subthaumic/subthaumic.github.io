---
layout: page
title: Directed Spaces as Feature Representations
description: Exploring the use of directed simplicial complexes to understand feature representations in neural networks.
img: assets/img/dsc.png
related_publications: 
category: applied topology
---

Neural nets don’t just light up single neurons for single ideas—they route computation through small, reusable subcircuits.  
In this project I model those subcircuits as **directed simplicial complexes (DSCs)** so that feature representations become geometric and causal objects rather than blurry heatmaps.

**Core idea.**  
We can treat an MLP as a (non-stochastic) structural causal model and build DSCs from **coherent counterfactual ablations**: gently lowering the activation of a neuron (or a set of neurons) along valid activation trajectories and tracking which other neurons consistently respond.
A directed simplex $$(P \to q)$$ is added when the ablation of predictors $$P$$ has a statistically consistent effect on target $$q$$ across a batch (Wilcoxon signed-rank on pre/post activation deltas).

**What this captures.**  
- *Polysemanticity*: the same neuron appears in multiple directed simplices/complexes.  
- *Polytopicity*: features spread over higher-dimensional directed motifs (not single units).  
- *Directionality*: we encode influence, not just co-activation.

**How I study it.**  
Small, controlled testbeds (quadrant classifiers; MNIST MLPs).  
I enumerate DSCs from activations + gradients, then compare **simplicial dimension, connectivity, recurrence, and symmetry**, and probe **causal directionality** via ablations/interventions. Filtration values (e.g. time-to-significance) let the complex “grow” so we can watch motifs assemble.

**Toy result (quadrants).**  
A “monosemantic” network yields clean, compositional DSCs: axes detectors combine into quadrant motifs.  
A bottlenecked “polysemantic” variant shows overlapping motifs and inhibitory links that only surface under coherent ablations—exactly the kind of tangled reuse we expect.

**Why it matters.**  
This bridges interpretability, causal inference, and TDA.  
We get compact, comparable summaries of *which group of neurons does what, in which direction, under which context*.

**Further reading & status.**  
Longer story and motivation in my blog post: [*The Tangled Web They Weave*](https://open.substack.com/pub/subthaumic/p/the-tangled-web-they-weave).  
A manuscript is in preparation; I’m happy to share a draft, just reach out.
As always, feedback and collaboration welcome!