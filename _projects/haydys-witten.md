---
layout: page
title: Haydys-Witten Instantons
description: PhD project
category: geometric analysis
related_publications: Bleher2023a, Bleher2023b, Bleher2023c
---

Haydys-Witten instantons play a crucial role in Witten's gauge theoretic approach to Khovanov homology, which provides an intriguing example of the general connection between geometric analysis and topological invariants of manifolds and knots.

Starting from a Wilson line along a knot $$K$$ in Chern-Simons theory and using a series of dualities between equivalent realizations of the same physical system, Witten arrives at the Hilbert space of BPS states $$\mathcal{H}_{\mathrm{BPS}}(K)$$ in five-dimensional $$\mathcal{N}=2$$ supersymmetric Yang-Mills (SYM) theory on the manifold with boundary $$\mathbb{R}_s \times S^3 \times \mathbb{R}^+_y$$.
Witten proposed that $$\mathcal{H}_{\mathrm{BPS}}(K)$$ is a homological knot invariant and that it coincides with Khovanov homology.

To calculate $$\mathcal{H}_{\mathrm{BPS}}(K)$$, start with the vector space $$CF^{\bullet,\bullet}(S^3, K)$$ spanned by all supersymmetric *classical* ground states of the theory.
The latter are given by $$\mathbb{R}_s$$-invariant solutions of the equations of motion, a set of partial differential equations known as Kapustin-Witten equations.
BPS states (supersymmetric *quantum* ground states) are obtained from the classical ones by taking into account quantum-mechanical instanton corrections.
Instanton corrections in this context arise from solutions of the Haydys-Witten equations on $$\mathbb{R}_s\times S^3 \times \mathbb{R}^+_y$$ that interpolate between two Kapustin-Witten solutions at $$s\to\pm\infty$$.
Counting Haydys-Witten instantons defines a differential $$Q$$ on $$CF^{\bullet,\bullet}$$, such that the space of BPS states is given by an infinite-dimensional version of Morse theory

$$\mathcal{H}_{\mathrm{BPS}}^{\bullet,\bullet}(K) = HF^{\bullet,\bullet}(K) := H^\bullet( CF^{\bullet,\bullet}(K), Q)\ .$$

In short: Physics tells us that there is a Floer theory of Haydys-Witten instantons on five-manifolds (instead of anti-self dual connections on four-manifolds), that yields interesting topological invariants of four-manifolds with boundaries and corners.

Gaiotto and Witten laid out a program to calculate Khovanov homology directly from the partial differential equations in gauge theory.
One of the key ideas is to construct solutions of the four-dimensional Kapustin-Witten equations on $$\mathbb{R}_t \times \Sigma \times \mathbb{R}^+_y$$, where $$\Sigma$$ is a Riemann surface, by adiabatically braiding solutions of the three-dimensional specialization known as extended Bogomolny equations (EBE) along a braid representation of $$K$$ extended in the direction of $$\mathbb{R}_t$$.

In my thesis I report on new advances in that direction.
Chapter 2 sets the scene, elaborating on the construction of Haydys-Witten Floer theory and, in doing so, also provides some previously unreported results.
The key insights of Chapters 3 and 4 take the form of vanishing results for the Kapustin-Witten and Haydys-Witten equations and might be of independent interest.
In Chapter 5 these insights are combined with Gaiotto and Witten's approach of adiabatically braiding solutions of the extended Bogomolny equations.
This leads to a conjectural relation between Haydys-Witten Floer theory and a version of symplectic Khovanov homology.
The arguments of Chapter 5 are ultimately based on physical intuition, and while a proof along these lines currently seems out of reach, the results presented in this work lay out a new strategy to confirm that Witten's gauge theoretic categorification of the Jones polynomial produces Khovanov homology.