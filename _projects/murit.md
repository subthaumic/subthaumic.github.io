---
layout: page
title: MuRiT
description: Ripser add-on for pathwise exploration of multi-persistence in filtered clique complexes
img: assets/img/paths.gif
related_publications: Neumann2022
related_repositories: https://github.com/tdalife/murit
category: applied topology
---

MuRiT (Multiparameter-Rips Transform) computes **pathwise persistent homology** for a multifiltered clique complex.
It implements the pathwise Vietoris–Rips transformations of {% cite Neumann2022 %}, letting you probe multi-parameter persistence with the speed and memory footprint of Ripser.

## What it does
- **Multi-parameter input** – describe a clique complex via a CSV listing 1-simplices with their generator antichains in $$\mathbb{R}^k$$; incomparable generators per edge are supported and automatically pruned to a minimal antichain.
- **Pathwise persistence** – specify a coordinatewise non-decreasing path through $$\mathbb{R}^k$$; MuRiT reduces the multifiltration to a one-dimensional auxiliary matrix and feeds it to Ripser, translating interval endpoints back to filtration vectors.
- **Multi-path orchestration** – pass a `.paths` file to process many paths in one run; outputs are written per path (`*_pathNN.aux`, `*_pathNN.ripser`).
- **Ripser integration** – `--ripser` uses `ripser` from `PATH`; `--ripser <path>` uses an explicit binary.
- **Parallel execution** – auxiliary matrix generation is fully multithreaded with deterministic output order.

## Typical workflow
```bash
murit \
  --complex examples/figure8.csv \
  --path examples/figure8.paths \
  --ripser --dim 1
```

`figure8.csv` specifies the complex:
```text
N,k
9,2
0,1,"[[0,0]]"
1,2,"[[0,0]]"
...
```

`figure8.paths` lists one JSON path literal per line:
```text
[[0,0],[1,0],[1,1]]
[[0,0],[0,1],[1,1]]
```

MuRiT writes `figure8_path01.ripser`, `figure8_path02.ripser`, … with Ripser output translated back to filtration vectors.

## When to use it
- Exploring multi-parameter filtrations by sweeping many paths before committing to heavier multi-persistence computations.
- Benchmarking time-varying or multi-modal datasets where several parameters interact.
- Automating feature-stability studies across many paths through the same complex.

## Learn more and cite
- Source code & releases: [github.com/tdalife/murit](https://github.com/tdalife/murit)
- Preprint: Maximilian Neumann *et al.* "MuRiT: Efficient Computation of Pathwise Persistence Barcodes in Multi-Filtered Flag Complexes via Vietoris-Rips Transformations," arXiv:2207.03394.
