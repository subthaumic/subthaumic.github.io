---
layout: page
title: markovmodus
description: Markov-modulated simulator for single-cell RNA velocity benchmarks
category: geometric machine learning
related_repositories: https://github.com/subthaumic/markovmodus
---

`markovmodus` generates synthetic single-cell RNA sequencing snapshots where a hidden continuous-time Markov process controls transcriptional kinetics.
It provides the ground-truth lineage graphs that trajectory- and velocity-inference methods try to reconstruct, making it a practical sandbox for stress-testing those pipelines.

## The model

Each cell carries a hidden state $$z \in \{z_1, z_2, \ldots\}$$ that evolves as a continuous-time Markov chain on a state graph,

$$
\frac{d}{dt} p_z(t) = \sum_{z'} H_{zz'}\, p_{z'}(t),
$$

with asymmetric rates $$H_{zz'} \neq H_{z'z}$$ encoding the directionality of state transitions.

The current state $$z(t)$$ determines the transcription rate $$\alpha_{z, g}$$ for each gene $$g$$, which drives a transcription–splicing–degradation process for its unspliced and spliced counts $$u_g, s_g$$:

$$
\begin{aligned}
\frac{d u_g}{dt} &= \alpha_{z(t), g} - \beta\, u_g, \\
\frac{d s_g}{dt} &= \beta\, u_g - \gamma\, s_g,
\end{aligned}
$$

where $$\beta$$ is the splicing rate and $$\gamma$$ the degradation rate.

## Highlights
- **Explicit state graphs** – branching, cyclic, or linear lineage topologies, with asymmetric rates to encode directionality.
- **Dynamic transitions** – transition rates can be static or time- and state-dependent for non-stationary dynamics.
- **Cell proliferation** – cells can divide during the simulation, with lineage bookkeeping for each daughter.
- **Tunable kinetics and noise** – per-state expression targets with global splicing/decay, plus optional negative-binomial count noise.
- **Ready-to-use outputs** – AnnData for Scanpy, pandas DataFrames, or `.csv` / `.h5ad` files.

## Usage sketch
```python
from markovmodus import SimulationParameters, simulate_dataset

params = SimulationParameters(
    num_states=5,
    num_genes=300,
    num_cells=2000,
    t_final=30.0,
    dt=1.0,
    markers_per_state=120,
    rng_seed=42,
)

adata = simulate_dataset(params)              # AnnData with spliced / unspliced layers
df = simulate_dataset(params, output="dataframe")  # or pandas DataFrame
```

## Learn more
- Documentation: [subthaumic.github.io/markovmodus](https://subthaumic.github.io/markovmodus/)
- PyPI package: [pypi.org/project/markovmodus](https://pypi.org/project/markovmodus/)
- Source code & issue tracker: [github.com/subthaumic/markovmodus](https://github.com/subthaumic/markovmodus)
