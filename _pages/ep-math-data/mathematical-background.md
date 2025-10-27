---
layout: "page"
title: "Mathematical Background"
permalink: "/projects/ep-math-data/mathematical-background/"
archived: true
archive_source: "STRUCTURES Wiki"
archive_captured: "Oct 2025"
primary_editor: "Dspitz"
primary_edit_count: "29"
total_edits: "50"
first_editor: "Bleher"
first_edit: "2019-05-05T09:05:39Z"
last_editor: "Dspitz"
last_edit: "2019-10-26T09:08:28Z"
---
> This article was originally written by Daniel Spitz for the STRUCTURES Wiki (captured October 2025).


Topological data analysis (TDA) techniques are fundamentally built on ideas and results of algebraic topology. The persistent homology toolbox includes rigorous mathematical theorems from general and algebraic topology, justifying the constructions undertaken. As motivated below, there are three fundamental results that make the classical theory of persistent homology sensible. In addition to these, we introduce relevant mathematical objects, mainly following  Carlsson 2009.

## Introduction
### Topological Data Analysis, abstractly
Data of interest is given by means of point clouds, that is, finite subsets  X\subset \mathbb{R}^n . In order to associate topological notions to [math]X[/math] it is necessary to first translate the data into topological spaces. This step usually requires the notion of a distance, that is, a metric on  \mathbb{R}^n , which is tailored to the nature of the data. This way, geometry enters the stage: The distance of points in \mathbb{R}^n is a notion that is usually not inherent to the data. Additionally, on different length scales different information may be encoded, which is why a priori there exists no distinguished value of a distance. Instead, unifying features that persist over a broad range of length scales may be dominant, while others may be subdominant, generically. The persistence of topological features is precisely what TDA techniques are capable to capture via the structure of persistent homology groups.

To this end, the applications of topological ideas to data analysis can almost always be divided into the following two steps
$$
\text{Data} \stackrel{geometry}{\longrightarrow} \text{simplicial complex} \stackrel{algebraic\;topology}{\longrightarrow} \text{invariants inherent to the data set} 
$$

### The Need for Theorems
Let us assume that our initial point cloud data [math]D=\{p_i \in \mathbb{R}^n\}[/math] arises as a finite subset of a paracompact topological space [math]X[/math] embedded in [math]\mathbb{R}^n[/math]. TDA techniques have the purpose to determine characteristic properties of the topological space [math]X[/math] from the point cloud [math]D[/math].

For any value of [math]r[/math] the open balls centered at the points are a good open cover [math]\mathcal{U}_r = \{B_r(p_i)\}[/math] of the compact space [math]Y_r=\bigcup B_r(p_i)[/math]. Recall that the Čech complex [math]\check{\mathcal C}(D)[/math] is the filtered complex of the [nerves]({{ '/projects/ep-math-data/mathematical-background/#the-nerve-theorem' | relative_url }}) [math]\check{\mathcal C}_r(D) = \{ N(\mathcal U_r), r\in [0,\infty) \}[/math]. Thus, by the [nerve theorem]({{ '/projects/ep-math-data/mathematical-background/#the-nerve-theorem' | relative_url }}) there exists a homotopy equivalence [math]\check{\mathcal C}_r(D) \simeq Y_r[/math] for each [math]r[/math].

For a moment assume that there exists a value [math]r[/math], such that [math]X\cap\mathcal U_r[/math] is a good open cover of [math]X[/math]. Then, at this value of [math]r[/math] the Čech complex is actually homotopy equivalent to [math]X[/math] due to the [nerve theorem]({{ '/projects/ep-math-data/mathematical-background/#the-nerve-theorem' | relative_url }}). This motivates the standard approach to topological data analysis, in which we assume that - generically - we are in a situation with the above assumptions holding.

However, it is not clear at which value of [math]r[/math] this situation occurs, which means that we need to consider the radius-dependent, 1-parameter family of Čech complex of [math]D[/math] as a whole. Then, the topological invariants of this filtered complex will contain characteristic properties of [math]X[/math] - encoded in their radius-dependence. The homology groups of a 1-parameter family of filtered simplicial complexes actually have the structure of a [persistence module]({{ '/projects/ep-math-data/mathematical-background/#persistence-modules' | relative_url }}). According to the [structure theorem]({{ '/projects/ep-math-data/mathematical-background/#the-structure-theorem' | relative_url }}), we can completely classify persistence modules by means of all birth and death parameters of homology classes, providing us with a useful and efficient structural description of multi-scale topological information.

Unfortunately, the situation described so far does not occur in data analysis scenarios, typically. The hypotheses of [math]X[/math] being embedded and there being a radius [math]r[/math] that admits a good open cover of the embedding of [math]X[/math] by balls with this radius are problematic. Furthermore, measurements are always endowed with uncertainties, such that the points of [math]D[/math] do not necessarily lie on the image of [math]X[/math] in [math]\mathbb{R}^n[/math].

This is where the [stability theorem]({{ '/projects/ep-math-data/mathematical-background/#stability-theorem' | relative_url }}) enters, which makes precise the following statement: a small variation of the metric results in only a small variation of the associated persistence module. Although this result does not fully invalidate the objections of the previous paragraph, it is crucial for inferring topological information of [math]X[/math] from [math]D[/math].

## The Nerve Theorem
Often it is desirable to construct simplicial complexes which compute the homology of an underlying space [math]X[/math] or are strongly related to it. To rigorously guarantee for this one may look for a homotopy equivalence from [math]X[/math] to the simplicial complex. Numerous simplicial complexes exist that may be associated to [math]X[/math]. A particularly simple and in our setting useful variant will be the nerve of a covering of a topological space.

Given the nerve theorem below, which provides to us such a homotopy equivalence, the need for methods to generate coverings remains. This directly leads to the construction of different complexes such as the Čech complex or the Alpha complex. This way, the nerve theorem is a cornerstone in describing the homotopy type of a topological space via a finite point cloud sampled from it and associated simplicial complexes.

### The Nerve of a Covering
Let [math]X[/math] be a topological space, and let [math]\mathcal U=\{U_i\}[/math] be any covering of [math]X[/math]. The _nerve_ of [math]\mathcal U[/math], denoted by [math]N\mathcal U[/math], is defined as the abstract simplicial complex with vertex set [math]A[/math], and where a family [math]\{i_0,\dots, i_k\}[/math] spans a [math]k[/math]-simplex if and only if [math]U_{i_0}\cap \dots \cap U_{i_k}\neq \emptyset[/math].

### The Nerve Theorem
Let [math]X[/math] be a paracompact space and [math]\mathcal U=\{U_i\}[/math] a good open cover, that is every nonempty intersection of finitely many sets in [math]\mathcal U[/math] is contractible.

Then the nerve [math]N\mathcal U[/math] is _homotopy equivalent_ to [math]X[/math].

## The Structure Theorem
Given a 1-parameter family of filtered simplicial complexes, say depending on a length scale [math]r[/math], its persistent homology groups form a persistence module. Additional information enters the stage through the parameter [math]r[/math], the description of which is elegantly captured by the structure theorem . Accordingly, the structure of a barcode, that is, a multiset of possibly infinitely long intervals, may be used to describe persistent homology groups of a 1-parameter family of simplicial complexes.

### Persistence Modules
Following Otter et al 2017 , a pair [math](\{M_i\}_{i\in I}, \{\Phi_{i,j}: M_i\to M_j\}_{i\leq j})[/math], where [math](I, \leq )[/math] is a totally ordered set, such that for each [math]i[/math], we have that [math]M_i[/math] is a vector space and the maps [math]\Phi_{i,j}[/math] are linear maps satisfying the functoriality property [math]\Phi_{k,j}\circ \Phi_{i,k} = \Phi_{i,j}[/math] for all [math]i\leq k \leq j[/math], is called a _persistence module_.

### Persistent Homology Groups
Let [math]C_1\subset C_2\subset \dots \subset C_l=C[/math] be a filtered simplicial complex. The [math]p[/math]_th persistent homology of_ [math]C[/math] is the pair $$(\{H_p(C_i)\}_{1\leq i \leq l} , \{f_{i,j}\}_{1\leq i\leq j \leq l}\}),
$$
where for all [math]i,j\in \{1,\dots, l\}[/math] with [math]i\leq j[/math], the linear maps [math]f_{i,j}: H_p(C_i)\to H_p(C_j)[/math] are the maps induced by the inclusion maps [math]C_i\to C_j[/math].

### The Structure Theorem
Let [math]C_1\subset C_2\subset \dots \subset C_l=C[/math] be a filtered simplicial complex, for example the 1-parameter family of Čech complexes, [math]\check{\mathcal C}(D)[/math], D being as before a finite subset of X. Then the [math]p[/math]th persistence module of homology classes of [math]C[/math] with coefficients in a field k decomposes isomorphically as follows,$$H_p( C,k) \simeq \bigoplus_{i=1}^{r} I_{[b_i,d_i]}
$$
where the I_{[b_i,d_i]} denote the indecomposable persistence modules
$$
I_{[b_i,d_i]} = \left\{ \begin{matrix} k & t\in[b_i,d_i] \\ 0 & \text{else } \end{matrix} \right.
$$
and \{[b_i,d_i], 1\leq i \leq r\} is a finite collection of intervals, for the example of [math]\check{\mathcal C}(D)[/math] with r\leq|D|.

## The Stability Theorem
Stability theorems for persistence diagrams exist in multiple different fashions . We focus here on the first such stability result obtained by Cohen-Steiner, Edelsbrunner and Harer in 2007 .

### Stability Theorem
Let [math]X[/math] be a triangulable space with continuous tame functions [math]f,g:X\to \mathbb{R}[/math]. Then the persistence diagrams satisfy $$d_B(D(f),D(g))\leq ||f-g||_{\infty}.$$ Here, [math]D(f), D(g)[/math] specify the persistence diagrams of the filtration of sublevel sets of the functions [math]f,g[/math], respectively, [math]d_B[/math] denotes the Bottleneck distance between two persistence diagrams and [math]||f-g||_{\infty}[/math] is the supremum of [math]f-g[/math].

In words, persistence diagrams are stable under possibly irregular perturbations of small amplitude.