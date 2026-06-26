# Evidence-based Reliability Assessment of Predicted Biological Relationships

*A computational methods project using cross-day neuron matching as a case study.*

---

## Overview

Many computational methods predict relationships between biological entities, but evaluating whether those predictions are reliable remains difficult. Validation evidence is often incomplete, noisy, or inconsistent, making it challenging to determine how much confidence should be placed in an individual prediction.

This project investigates how multiple sources of biological evidence can be combined to assess the reliability of predicted relationships. Rather than treating predictions as simply correct or incorrect, the goal is to characterize different levels of support, identify uncertainty, and better understand where computational confidence agrees or disagrees with independent biological evidence.

Cross-day neuron matching in chronic Neuropixels recordings serves as the initial case study because it naturally provides multiple independent sources of validation.

---

## Research Question

How should predicted biological relationships be evaluated when independent evidence is incomplete, noisy, or conflicting?

More specifically:

- What types of evidence provide the strongest support for a predicted relationship?
- How should disagreement between evidence sources be interpreted?
- When does model confidence fail to reflect biological support?
- Can reliability be assessed in a systematic and reproducible way rather than relying solely on manual inspection?

---

## Current Framework

The current workflow consists of four stages.

### 1. Candidate Relationship Generation

Candidate neuron pairs are generated using UnitMatch across chronic Neuropixels recording sessions.

### 2. Independent Evidence Extraction

Each candidate pair is evaluated using evidence that is independent of the original matching procedure, including:

- waveform morphology
- autocorrelogram (ACG) structure

Additional evidence sources may be incorporated in future work.

### 3. Reliability Assessment

Candidate pairs are manually reviewed by integrating multiple evidence sources rather than relying on a single similarity metric.

Current reliability categories include:

- Strong Match
- Likely Match
- Uncertain
- Likely Mismatch
- Strong Mismatch

These labels represent the overall level of biological support rather than the original model prediction.

### 4. Reliability Analysis

The resulting annotations are used to investigate:

- agreement between prediction confidence and biological evidence
- disagreement between different evidence sources
- common sources of uncertainty
- characteristics of supported and unsupported predictions

---

## Current Progress

Current work has focused on establishing an initial validation framework.

Completed work includes:

- cross-session neuron matching using UnitMatch
- waveform reconstruction from raw spike recordings
- ACG extraction and visualization
- manual review of high-confidence candidate pairs
- construction of an evidence table for reliability assessment
- preliminary feature comparisons across reliability categories
- documentation of representative agreement, uncertainty, and mismatch cases

Detailed analyses are available in the project documentation.

---

## Preliminary Observations

Several consistent patterns have emerged during manual review.

### Prediction confidence and biological support are not always aligned.

Some neuron pairs assigned very high matching probabilities showed limited supporting biological evidence after independent review.

### Different evidence sources contribute unequally.

Waveform morphology generally provided stronger support than ACG structure, particularly when distinguishing likely matches from likely mismatches.

### Many uncertain cases reflect insufficient evidence.

Most uncertain pairs were associated with incomplete or ambiguous evidence rather than direct disagreement between evidence sources.

### Reliability assessment itself contains uncertainty.

Some candidate pairs remained difficult to classify consistently, suggesting that reliability should be viewed as a spectrum rather than a binary decision.

These observations motivate further investigation into computational approaches for reliability assessment.

---

## Future Directions

Current work focuses on manual evidence integration. Future work will explore more systematic approaches for assessing reliability.

Potential directions include:

### Evidence Integration

- incorporate additional independent validation features
- compare the contribution of different evidence sources
- investigate evidence weighting strategies

### Reliability Modeling

- develop computational approaches for reliability scoring
- compare model confidence with independently assessed reliability
- investigate whether uncertainty can be estimated directly from available evidence

### Generalization

Although this project focuses on cross-day neuron matching, the broader questions addressed here arise in many areas of computational biology where predicted biological relationships require validation under incomplete or uncertain evidence.

Future work will explore whether similar reliability assessment strategies can be applied to other biological prediction problems.

---

## Repository Structure

```text
README.md

analysis/

docs/

figures/

```

---

## Tools

- MATLAB
- Python
- UnitMatch
- Kilosort4
- Bombcell

---

## Project Status

This project is under active development.

Current efforts focus on understanding how independent biological evidence can be integrated into a reproducible framework for assessing the reliability of predicted biological relationships.
