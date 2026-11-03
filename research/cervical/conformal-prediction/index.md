---
layout: project
title: Conformal Prediction for Cervical Cancer Screening
subtitle: Understanding uncertainty in automated visual evaluation.
category: Cervical & Gynecologic AI
status: Published Research
parent: /research/cervical/
---

## Overview

This project investigates uncertainty quantification for
deep-learning-based cervical cancer screening.

We compare conformal prediction with Monte Carlo (MC)
dropout to better understand predictive uncertainty,
misclassifications, and the challenges of distinguishing
Normal, Gray Zone, and Precancer+ cervical images.

## Motivation

Automated cervical cancer screening systems may help extend
screening access in low-resource settings.

However, clinical deployment requires more than accurate
predictions. We must also understand when a model is
uncertain, particularly when misclassification could
affect clinical decisions.

## Methodology

We evaluated two conformal prediction methods:

- **Least Ambiguous Set-Valued Classifier (LAC)**
- **Adaptive Prediction Sets (APS)**

We compared their prediction-set lengths with uncertainty
estimated using repeated Monte Carlo dropout inference.

We also investigated uncertainty across the three
diagnostic categories and compared two-class and
three-class screening models.

## Key Findings

- Conformal prediction sets were generally larger for
  incorrect predictions than for correct predictions.
- LAC showed a stronger relationship with MC-dropout
  uncertainty than APS.
- Gray Zone images exhibited elevated uncertainty,
  highlighting ambiguity in diagnostic categorization.
- Conformal prediction offered a computationally
  inexpensive alternative to repeated stochastic inference,
  subject to careful calibration.

## Figures and Visualizations

*Figures will be added as the project page develops.*

## Publications

**Conformal Prediction and Monte Carlo Inference for
Addressing Uncertainty in Cervical Cancer Screening**

Clark C, Kinder S, Egemen D, et al.  
UNSURE 2024, Lecture Notes in Computer Science, 2025.

[View publication on Springer](https://doi.org/10.1007/978-3-031-73158-7_19)

## Presentations and Posters

*To be added.*

## Code and Resources

*To be added.*
