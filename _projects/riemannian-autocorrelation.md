---
layout: page
title: Riemannian Autocorrelation
description: Extending autocorrelation functions to Riemannian manifolds with applications to non-local isoperimetric energies.
img: assets/img/autocorrelation.png
category: geometric analysis
---

Let $$(M^n,g)$$ be a compact Riemannian manifold and $$\Omega \subset M$$ a measurable subset. We study non-local isoperimetric energies of the form

$$E_{\gamma,\varepsilon}(\Omega) = \mathrm{Per}(\Omega) - \frac{\gamma}{\varepsilon} \int_{M \times M} K_\varepsilon(x,y) \, |\mathbf{1}_\Omega(x) - \mathbf{1}_\Omega(y)| \, dx \, dy,$$

where $$K_\varepsilon$$ is an interaction kernel.
The two terms compete: the perimeter acts like surface tension—it penalizes boundary and prefers large connected regions.
The non-local term, with its minus sign, favors configurations with more interface, acting as a repulsive or spreading force (think screened electrostatic repulsion between charged membrane domains).
This competition is the classic setup for pattern formation.
Such energies have been studied in flat domains, but many phenomena occur on curved surfaces.

In the Euclidean case, the non-local term can be reformulated using the *autocorrelation function*, which measures the average overlap between $$\Omega$$ and its translates at distance $$r$$.
Our key insight is that translations can be replaced by the geodesic flow: we define the **Riemannian autocorrelation function** as

$$c_\Omega(r) = \frac{1}{\sigma_{n-1}} \int_M \int_{\|w\|=1} \mathbf{1}_\Omega(x) \, \mathbf{1}_\Omega(\exp_x(rw)) \, dw \, dx,$$

which generalizes (a radially symmetric version of) Matheron's covariogram to curved spaces.
I expect this function to be of independent interest in geometric analysis, as it encodes geometric information about $$\Omega$$, e.g. one could ask which sets the autocorrelation function uniquely determines (cf. [covariogram problem](https://people.dimai.unifi.it/bianchi/lavori/covariogram_survey14.pdf)).

Our first main result characterizes finite perimeter via the autocorrelation function: $$\Omega$$ has finite perimeter if and only if $$c_\Omega$$ is Lipschitz continuous.
In that case, the derivative at $$r=0$$ satisfies $$c'_\Omega(0) = -\frac{k_n}{2} \mathrm{Per}(\Omega)$$.

As an application, we specialize to the round sphere $$M = S^n$$ with Helmholtz kernel $$K_\varepsilon$$.
In the short-range regime $$\varepsilon \to 0$$, we prove that $$E_{\gamma,\varepsilon}$$ Γ-converges to $$(1 - \gamma/\gamma_{\mathrm{crit}}) \mathrm{Per}(\Omega)$$ for subcritical $$\gamma < \gamma_{\mathrm{crit}} = 1$$.
In this regime, minimizers are geodesic balls—no fine-scale patterns form.