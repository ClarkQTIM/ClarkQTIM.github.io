---
layout: project
title: Uncertainty-Aware Training for Ophthalmic Segmentation
subtitle: Incorporating predictive uncertainty directly into the learning objective.
category: Ophthalmology
status: Published Research
parent: /research/ophthalmology/
---

## Overview

Deep learning models are commonly trained by minimizing
the difference between their predictions and ground truth.

However, predictive uncertainty contains additional
information about where a model struggles.

**Uncertainty-Aware Training (UAT)** incorporates
pixel-level uncertainty directly into the loss function,
encouraging segmentation models to concentrate on
ambiguous regions during optimization.

We investigate this approach using the Medical Segment
Anything Model (MedSAM) on three ophthalmic
segmentation tasks.

## Motivation

Uncertainty quantification is often treated as a
post-training diagnostic tool.

This project instead asks:

**Can model uncertainty improve the learning process itself?**

By emphasizing uncertain pixels during optimization,
we aim to improve segmentation performance without
substantially modifying the underlying model architecture.

## Methodology

### Model

We fine-tuned MedSAM for three ophthalmic
segmentation tasks:

- **Geographic atrophy (GA)** in fundus autofluorescence images.
- **Optic cup (OC)** segmentation in fundus photographs.
- **Foveal avascular zone (FAZ)** segmentation in OCT angiography.

### Uncertainty estimation

We evaluated three uncertainty-aware training strategies:

1. **Entropy:** Pixel-wise predictive entropy.
2. **Conformal prediction:** Uncertainty derived from
   Least Ambiguous Set-Valued Classifier (LAC) prediction sets.
3. **Model variance:** Variation across MedSAM's multiple
   segmentation outputs.

### Uncertainty-weighted loss

We introduced a pixel-wise weighting scheme:

\[
W_i = 1 + \gamma U_i, \qquad \gamma \geq 0
\]

where \(U_i\) denotes pixel-level uncertainty and
\(\gamma\) controls the strength of uncertainty weighting.

The resulting weighted binary cross-entropy loss is

\[
\mathcal{L}_{UAT}
=
-\frac{1}{N}
\sum_{i=1}^{N}
W_i
\left[
y_i \log(\hat{y}_i)
+
(1-y_i)\log(1-\hat{y}_i)
\right].
\]

When \(\gamma=0\), the loss reduces to ordinary
binary cross-entropy.

### Experimental evaluation

Each configuration was evaluated over ten runs.
We compared segmentation performance, training
stability, and convergence behavior against the
standard fine-tuning baseline.

## Key Results

### Segmentation performance

**Entropy-based UAT significantly improved Dice
scores across all three ophthalmic segmentation tasks.**

LAC conformal-based training also improved performance
for geographic atrophy and optic cup segmentation.

### Training stability

Several UAT configurations reduced variability in
model performance, although the reported stability
improvements did not reach statistical significance.

### Training convergence

Performance gains did not consistently translate
into faster convergence.

### Interpretability

Uncertainty maps provided insight into how the
model's uncertainty evolved during training.

Entropy-based uncertainty frequently remained
concentrated around segmentation boundaries,
highlighting ambiguous anatomical regions.

## Limitations and Future Work

The effectiveness of uncertainty weighting depends
on the uncertainty method, task complexity, and
hyperparameter selection.

Future work includes:

- Alternative segmentation losses, including Dice
  and Tversky variants.
- Multi-class segmentation.
- Additional uncertainty estimation methods.
- Evaluation across further imaging datasets.

## Figures and Visualizations

*To be added: uncertainty maps, segmentation examples,
training dynamics, and Dice score comparisons.*

## Publication

Clark CW, Kinder S, Nebbia G, Veturi YA, McNamara S,
Manoharan N, Forest T, Kahook M, Mandava N, Singh P,
Kalpathy-Cramer J. Uncertainty-aware training for
ophthalmic segmentation using MedSAM.
Transl Vis Sci Technol. 2026 Feb;15(2):19.
doi:10.1167/tvst.15.2.19.

[View published article](https://doi.org/10.1167/tvst.15.2.19)

## Presentations and Posters

*To be added.*

## Code and Resources

*To be added.*
