---
layout: project
title: Automated Detection of Acetowhite Lesions
subtitle: Learning the temporal behavior of cervical tissue to identify regions of expert agreement.
category: Cervical & Gynecologic AI
status: Published Research
parent: /research/cervical/
---

## Overview

During colposcopy, dilute acetic acid is applied to the cervix,
causing abnormal tissue to undergo transient visual changes
known as **acetowhitening**.

Although acetowhitening is an important cue for identifying
potential lesions, its interpretation varies substantially
between clinicians.

This project investigates whether machine learning can
analyze the temporal behavior of cervical regions and
automatically identify areas that expert colposcopists
would annotate as acetowhite lesions.

## Motivation

Traditional colposcopic assessment depends heavily on
clinician experience and visual interpretation.

By learning from temporal changes rather than relying
only on a single image, we aim to develop objective
tools that could support lesion identification and
biopsy site selection.

## Methodology

### Data

We analyzed time-series images from **238 colposcopy
examinations**, each containing 17 sequential cervical
images captured before and after application of acetic acid.

Five expert colposcopists provided annotations indicating
areas exhibiting acetowhitening.

### Image preprocessing

The pipeline included:

1. Spatial registration across the image sequence.
2. Cervix localization using an object detection model.
3. Image cropping and segmentation into 5×5 superpixels.
4. Extraction of temporal intensity trajectories.
5. Normalization, smoothing, and artifact filtering.

Each superpixel produced a temporal sequence of 17
intensity values.

### Temporal feature extraction

We extracted statistical features describing the
acetowhitening response, including:

- Area under the temporal curve
- Mean intensity change
- Maximum intensity change
- Time to peak response
- Standard deviation

K-means clustering was used to identify characteristic
temporal response patterns, with distances to cluster
centers serving as additional predictive features.

### Classification

An **XGBoost classifier** was trained to predict four
levels of expert agreement:

- No agreement
- Low agreement
- Medium agreement
- High agreement

Predicted agreement maps were reconstructed from
superpixel classifications.

## Key Results

The best-performing feature combinations achieved an
**overall ROC-AUC of 0.825** across the four
agreement categories.

Cluster-distance features contributed important
predictive information beyond summary statistics alone.

Model-generated maps reproduced regions of expert
agreement, particularly where multiple clinicians
identified the same acetowhite lesions.

### Exploratory histological comparison

Predictions were also compared with localized biopsy
histology from 24 patients, comprising 44 biopsy areas.

Of 16 areas with CIN2+ histology, 10 were assigned
medium or high predicted agreement.

This preliminary comparison supports further study,
but does not establish clinical diagnostic performance.

## Limitations and Future Work

The model learns patterns in expert annotations rather
than directly predicting histologically confirmed disease.

Additional validation on larger datasets with localized
histology is required.

Other directions include improving registration,
reducing clustering costs, and integrating these maps
into downstream cervical screening models.

## Figures and Visualizations

*To be added: cervical image sequences, temporal
feature extraction pipeline, synthetic lesion maps,
and comparisons with localized histology.*

## Publication

Clark C, Aquilina A, Perkins RB, Papagiannakis E,
Kalpathy-Cramer J. Automating the detection of acetowhite
lesions by classifying the temporal behavior of cervical
regions. J Low Genit Tract Dis.
2026 Jan 1;30(1):31-38.
doi:10.1097/LGT.0000000000000927.

[View published article](https://doi.org/10.1097/LGT.0000000000000927)

## Presentations and Posters

*To be added.*

## Code and Resources

*To be added.*
