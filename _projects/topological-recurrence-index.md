---
layout: page
title: Topological Recurrence Index
description: Persistent-homology pipeline that flags emerging adaptive mutations in viral genomes
category: applied topology
related_publications: Bleher2021
---

The **topological Recurrence Index (tRI)** ranks SARS-CoV-2 mutations by how frequently they appear across independent, phylogenetically distant lineages. 
It leverages persistent homology to spot convergent evolutionary signals that classic tree-based pipelines struggle to surface quickly.

{% cite Bleher2021 %}

## Why topology helps
- **Phylogeny-free convergence detection** – Vietoris–Rips filtrations on genomic Hamming graphs capture reticulate patterns that point to repeated selective advantages.
- **Inherently confined to genetic background** – tRI scores are always located within the context of specific genetic backgrounds, reducing noise from unrelated mutations.
- **Actionable priorities** – mutations with high tRI values align with variants of concern and experimentally validated fitness gains.

## Workflow at a glance
1. Construct Hamming graphs of viral genomes sampled over time windows.
2. Compute Vietoris–Rips persistence in dimension one to identify loops corresponding to parallel mutational paths.
3. Aggregate loop membership to score individual mutations (the tRI) and track trajectories over time.
4. Cross-reference high-tRI mutations with structural data and epidemiological trends.

## Highlights
- Early warning signals for spike mutations later dominant in Alpha, Beta, Gamma and Delta variants.
- Open-source implementation alongside interactive dashboards for public-health partners.
- Scales to millions of sequences using distributed ripser-based calculations.

## Learn more
- Preprint: {% cite Bleher2021 %}
- Contact: reach out if you are interested in applying tRI to other pathogens or longitudinal omics datasets.
