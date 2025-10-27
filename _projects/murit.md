---
layout: page
title: MuRiT
description: Ripser add-on for pathwise exploration of multi-persistence in filtered metric spaces
img: assets/img/paths.gif
related_publications: Neumann2022
related_repositories: https://github.com/tdalife/murit
category: applied topology
---

MuRiT (Multiparameter-Rips Transform) is a standalone Go program that converts interval paths in multi-filtered metric spaces into one-dimensional filtrations that classical tools can digest.
It implements the pathwise Vietoris–Rips transformations of {% cite Neumann2022 %}, letting you probe multi-parameter persistence with the speed and memory footprint of Ripser.

## What it does
- **Pathwise multi-persistence** – sample any totally ordered path through an \(n\)-parameter Vietoris–Rips filtration and obtain the auxiliary distance matrix for that slice.
- **Ripser integration** – forward the matrix straight to a local Ripser instance (`--ripser`) and get barcodes mapped back to the chosen filtration coordinates.
- **Optimised execution** – fully parallel, streaming computations keep memory predictable; prebuilt binaries are available for Linux, macOS, and Windows.
- **Open-source workflow** – written in Go with a minimal CLI, ready for scripting, bundling, or extension.

## Typical workflow
```bash
murit \
  --dist examples/diamond.dist \
  --minima examples/diamond.minima \
  --path "[0,0,0]--[1,0,0]--[1,1.2,0]--[1,1.6,1]--[1,2,1]" \
  --ripser --dim 2
```
1. Provide a lower-triangular distance matrix and an annotation file listing the pointwise minima of the multi-filtration (e.g. time of arrival, sensor thresholds).
2. Specify the path in filtration space—MuRiT constructs the auxiliary matrix that encodes that subfiltration.
3. Add `--ripser` to launch Ripser automatically; any extra Ripser flags (dimension, threshold, modulus) are forwarded unchanged.

MuRiT prints the transformed distance matrix or, when Ripser is invoked, the persistent homology intervals referenced to the original filtration parameters.

## When to use it
- Benchmarking time-varying or multi-modal datasets where several parameters interact.
- Probing multi-parameter filtrations for interesting slices before running heavier multi-persistence computations.
- Automating sweeps over many paths through the same dataset to study feature stability.

## Learn more and cite
- Source code & releases: [github.com/tdalife/murit](https://github.com/tdalife/murit)
- Preprint: Maximilian Neumann *et al.* “MuRiT: Efficient Computation of Pathwise Persistence Barcodes in Multi-Filtered Flag Complexes via Vietoris-Rips Transformations,” arXiv:2207.03394.
