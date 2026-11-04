---
layout: project
title: "Quantum Search with Learned Oracles"
subtitle: "Exploring Grover search and Dürr–Høyer optimization for feature subset selection"
category: Quantum Computing
status: Ongoing research
parent: /research/quantum/
---

## Overview

Choosing which variables to include in a predictive model is a deceptively difficult optimization problem. With \(d\) candidate features, there are \(2^d\) possible subsets. Exhaustively fitting and evaluating a model for every subset can quickly become impractical. A learned *surrogate* can estimate a subset's predictive value without retraining the underlying model each time—but exhaustively searching that surrogate over every subset still takes \(2^d\) evaluations.

This project explores a different possibility: **can a learned surrogate be implemented as a coherent quantum oracle, allowing quantum search algorithms to identify promising feature subsets with fewer oracle queries?**

## Feature subsets as a search problem

Let \(z\in\{0,1\}^d\) specify which features are selected and let \(F(z)\) measure the resulting model's held-out performance (for example, AUROC). Our ideal objective is

$$
z^* = \operatorname*{arg\,max}_{z\in\{0,1\}^d} F(z).
$$

We can instead learn a relatively inexpensive approximation \(\widehat F(z)\approx F(z)\). This avoids retraining for every *evaluation*, but does not, on its own, eliminate the combinatorial search problem. Classical heuristic searches can already avoid exhaustive enumeration; here, we investigate the theoretical opportunities and practical costs of **quantum oracle-based search**.

## Grover's algorithm: marking, then diffusion

Grover's algorithm searches an unstructured set of \(N\) candidates using an oracle that recognizes a valid answer. Starting from an equal superposition

$$
|s\rangle = \frac{1}{\sqrt N}\sum_{z=0}^{N-1}|z\rangle,
$$

one Grover iteration consists of **two reflections**:

**1. Oracle marking.** A phase oracle flips the sign of states satisfying a criterion \(m(z)\in\{0,1\}\):

$$
O_m|z\rangle=(-1)^{m(z)}|z\rangle.
$$

**2. Diffusion.** A reflection about the initial superposition converts these relative phase differences into amplitude amplification:

$$
D=2|s\rangle\langle s|-I,
\qquad G=DO_m.
$$

![Geometric illustration of one Grover iteration, showing the oracle reflection and the subsequent diffusion reflection.]({{ '/assets/images/quantum/grover-iteration.png' | relative_url }})

*One Grover iteration in the two-dimensional subspace of marked and unmarked states. The oracle flips the marked amplitude, then diffusion reflects the result about the starting state, rotating the vector toward the marked subspace.*

If \(M\) of the \(N\) candidates are marked, define \(\sin\alpha=\sqrt{M/N}\). Writing \(|g\rangle\) and \(|b\rangle\) for the normalized superpositions of marked and unmarked candidates, respectively,

$$
|s\rangle=\sin\alpha\,|g\rangle+\cos\alpha\,|b\rangle,
$$

and after \(k\) Grover iterations,

$$
G^k|s\rangle=\sin((2k+1)\alpha)|g\rangle
+\cos((2k+1)\alpha)|b\rangle.
$$

Thus the probability of obtaining a marked result is \(\sin^2((2k+1)\alpha)\). With an appropriate number of iterations, search requires \(O(\sqrt{N/M})\) oracle queries, rather than \(O(N/M)\) queries for naive random search. Too many iterations can rotate the state *past* the target, so the iteration count matters.

## From Grover search to Dürr–Høyer optimization

Grover search answers a threshold question: **does this candidate meet the criterion?** Dürr–Høyer minimum finding uses related quantum-search procedures to repeatedly improve a current candidate. For maximizing subset utility, an oracle can mark subsets whose estimated score exceeds a threshold \(T\):

$$
m_T(z)=\mathbf{1}\{\widehat F(z)>T\}.
$$

In the ideal oracle-query model, optimization over \(N=2^d\) candidates can require \(O(\sqrt N)=O(2^{d/2})\) queries, compared with \(O(N)\) exhaustive evaluations.

## Our research direction: learned quantum oracles

The proposed workflow is straightforward at a conceptual level:

**Feature subset** \(z\) → **surrogate estimate** \(\widehat F(z)\) → **coherent threshold oracle** → **Grover / Dürr–Høyer search** → **candidate subset for classical validation**.

The difficult part lies between the surrogate and the search. A classical predictor is not automatically a usable Grover oracle: the estimated score must be evaluated **coherently**, compared with a threshold, and converted into a reversible phase-marking operation. Circuit depth, ancillary qubits, approximation error, and the cost of building and querying the oracle may offset the theoretical reduction in query count. And optimizing \(\widehat F\) does not guarantee finding the maximizer of the true performance function \(F\).

Our aim is therefore **not to claim quantum advantage**, but to understand when a learned oracle makes quantum search a meaningful option for feature selection—and what its implementation would actually cost.

## Foundational reading

- Grover, L. K. (1996). [A fast quantum mechanical algorithm for database search](https://doi.org/10.1145/237814.237866). *Proceedings of STOC '96*, 212–219.
- Dürr, C., and Høyer, P. (1996). [A quantum algorithm for finding the minimum](https://arxiv.org/abs/quant-ph/9607014). *arXiv:quant-ph/9607014*.

## Ongoing Work

This is active research. Current questions concern surrogate fidelity, coherent oracle construction, and how approximation and hardware-resource costs affect any prospective quantum-search benefit. Implementation details and experimental findings are reserved for the manuscript.
