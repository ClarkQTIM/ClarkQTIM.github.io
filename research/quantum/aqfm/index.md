---
layout: project
title: Annealed Quantum Feature Maps
subtitle: Quantum dynamics as a tool for learning useful data representations
category: Quantum Computing
status: Ongoing research
---

## Overview

A feature map transforms data into a representation that may make a learning problem easier. **Annealed Quantum Feature Maps (AQFM)** investigate whether time-dependent quantum dynamics can generate useful features for classical machine-learning models. Rather than claiming a universal quantum advantage, this project asks a more targeted question: **when, and why, do these dynamical representations help?**

## A familiar example: a nonlinear problem made linear

Consider the simple two-dimensional function

$$
f(x_1,x_2)=x_1^2+x_2^2.
$$

Its graph is a bowl. If we assign each sampled point a label based on whether it lies outside a circle of radius $r$,

$$
y=\mathbf{1}\!\left\{x_1^2+x_2^2>r^2\right\},
$$

then the correct decision boundary is circular, rather than a straight line.

![Three-dimensional bowl representing x1 squared plus x2 squared]({{ '/assets/images/aqfm/aqfm_bowl.png' | relative_url }})
*The bowl $f(x_1,x_2)=x_1^2+x_2^2$; a fixed height corresponds to a circular boundary in the input plane.*

Ordinary logistic regression on the two raw inputs learns a score

$$
g(x)=\beta_0+\beta_1x_1+\beta_2x_2.
$$

Its boundary $g(x)=0$ is a **line**, which cannot reproduce the circle. But we can first construct a degree-two polynomial feature map,

$$
\phi_{\mathrm{poly}}(x)=
(x_1,x_2,x_1^2,x_1x_2,x_2^2).
$$

Logistic regression on these five features still uses a linear score in the *transformed* space,

$$
g(\phi_{\mathrm{poly}}(x))=\beta_0+\sum_{j=1}^{5}\beta_j\phi_j(x),
$$

but its boundary in the original $x_1,x_2$ plane can now be **quadratic**. The circular boundary becomes representable.

![Side-by-side linear and polynomial logistic regression decision boundaries]({{ '/assets/images/aqfm/aqfm_polynomial_example.png' | relative_url }})
*Illustrative synthetic example: a raw linear classifier cannot represent the circular decision boundary, while a degree-two expansion can. The reported training accuracies are for this generated example, not an AQFM experiment.*

**The takeaway:** a feature map can make a problem easy for a simple classifier, even when that same classifier fails on the original inputs.

## From polynomial features to quantum dynamics

AQFM follows the same basic recipe: **transform the input first, then learn from the transformed representation.** Instead of explicitly choosing polynomial terms, it uses the evolution of a quantum state under a data-dependent Hamiltonian.

A generic annealing schedule interpolates between an initial Hamiltonian and one that encodes the input $x$:

$$
H(t;x)=[1-s(t)]H_{\mathrm{init}}+s(t)H_{\mathrm{data}}(x),
\qquad 0\le t\le\tau.
$$

Starting from $|\psi_0\rangle$, the system evolves according to

$$
|\psi_x(\tau)\rangle=
\mathcal{T}\exp\!\left[-i\int_0^\tau H(t;x)\,dt\right]|\psi_0\rangle,
$$

where $\tau$ controls the anneal duration and $\mathcal{T}$ denotes time ordering (using units with $\hbar=1$).

The feature vector consists of expectation values of selected measurement observables:

$$
\phi_{\mathrm{AQFM}}(x)=
\big(\langle O_1\rangle_x,\ldots,\langle O_m\rangle_x\big),
\qquad
\langle O_j\rangle_x=
\langle\psi_x(\tau)|O_j|\psi_x(\tau)\rangle.
$$

These features can then be supplied to a conventional classifier—just as the polynomial features were in the example above.

**Data $x$ → Hamiltonian $H_{\mathrm{data}}(x)$ → annealed evolution → observables $\langle O_j\rangle_x$ → classical classifier**

## What are we investigating?

Our ongoing work studies how the structure of the quantum map affects its usefulness, focusing on three questions:

- **Anneal timescale:** when do the dynamics create informative features, and when are they too weak or effectively uninformative?
- **Measurement choice:** how does the representation change when we measure different single-qubit observables or add two-qubit correlators?
- **Representation efficiency:** for which data structures do quantum-derived features help, compared with classical representations of comparable dimension?

The emphasis is on controlled experiments and interpretable mechanisms—not simply maximizing the score on one benchmark.

## Related work

- Simen et al., [*Quenched Quantum Feature Maps*](https://arxiv.org/abs/2508.20975) (2025). A closely related approach using nonadiabatic spin-glass dynamics for feature extraction.
- Simen et al., [*Digitized Counterdiabatic Quantum Feature Extraction*](https://doi.org/10.1038/s41598-026-67564-0) (*Scientific Reports*, 2026). A related Hamiltonian-based approach using counterdiabatic techniques and higher-order feature structure.

## Ongoing work

This research is in progress. Current efforts investigate anneal-time regimes, measurement bases and pair correlators, controlled synthetic tasks, and comparisons with matched-dimensional classical feature maps. Results and technical details will be added as the study develops.
