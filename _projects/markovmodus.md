---
layout: page
title: markovmodus
description: Markov-modulated simulator for single-cell RNA velocity benchmarks
category: geometric machine learning
related_repositories: https://github.com/subthaumic/markovmodus
---

`markovmodus` generates synthetic single-cell RNA sequencing snapshots where a hidden continuous-time Markov process controls transcriptional kinetics. 
It provides the ground-truth lineage graphs that trajectory- and velocity-inference methods try to reconstruct, making it a practical sandbox for stress-testing those pipelines.

The simulator samples cell state paths on a user-defined support (from fully connected graphs to bespoke transition matrices) and assigns each state its own steady-state expression targets.
Within every state, transcripts follow a linear splicing model, optionally perturbed by negative-binomial noise to match the over-dispersion seen in real data.

## Highlights
- **Explicit state graphs** – build branching, cyclic, or linear topologies by supplying an adjacency mask or transition matrix; asymmetric rates let you encode directionality without extra coding.
- **Customisable kinetics** – control gene-level marker assignments and reuse caps so neighbouring states share only the transcriptional programs you intend.
- **Snapshot realism** – globally consistent splicing (`beta`) and decay (`gamma`) parameters pair with per-state production targets; dispersion tuning adds count noise when desired.
- **Friendly outputs** – return AnnData objects for Scanpy workflows, pandas DataFrames for scripting, or persist directly to `.csv` and `.h5ad`.

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
    default_transition_rate=0.08,
    rng_seed=42,
)

adata = simulate_dataset(params)              # AnnData with spliced / unspliced layers
df = simulate_dataset(params, output="dataframe")  # or pandas DataFrame
```

## Learn more
- Documentation: [subthaumic.github.io/markovmodus](https://subthaumic.github.io/markovmodus/)
- PyPI package: [pypi.org/project/markovmodus](https://pypi.org/project/markovmodus/)
- Source code & issue tracker: [github.com/subthaumic/markovmodus](https://github.com/subthaumic/markovmodus)
