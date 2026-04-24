# Project Summary
This document summarizes the current stable workflow for an ongoing project on cross-day neuron matching and validation in chronic Neuropixels recordings.

Initial exploratory and learning steps are omitted. The focus here is the reusable analysis pipeline and current stage of progress.

---

# Step 0

# PIPELINE OVERVIEW
Kilosort  
→ Bombcell (unit quality control)  
→ UnitMatch (cross-day neuron matching)  
→ Validation and visualization

- Raw waveform extraction  
- Waveform-based SST construction  
- Spike-time ACG augmentation  
- High-confidence pair visualization

---

# PROJECT GOAL
A central challenge in chronic Neuropixels recordings is determining whether units detected across different recording sessions correspond to the same underlying neuron.

This project focuses on:

- Cross-session matching of putative neurons  
- Independent validation of matching outputs  
- Identifying uncertainty, agreement, and mismatch patterns  
- Building a scalable workflow for future larger datasets

---

# CURRENT DATA FLOW

## Inputs
- Standard Kilosort outputs  
- Raw electrophysiology recordings  
- Session metadata

## Outputs
- Cross-day candidate match tables  
- Per-session waveform summaries  
- Spike-time autocorrelograms  
- Visualization reports for manual review

---

# Step 1

# Bombcell Quality Control
Bombcell is run independently on each recording session to compute unit-level quality metrics from Kilosort outputs.

Bombcell is used for:

- Quality assessment  
- Unit labeling  
- Filtering low-quality units for downstream analysis

Bombcell does **not** modify spike times or waveforms.

## Notes
All datasets in this project were processed with Kilosort 4, so parameters were kept consistent across sessions.

---

# Step 2

# UnitMatch Cross-day Matching
UnitMatch is used to identify putative neuron correspondences across recording sessions.

It integrates multiple features, including:

- Waveform similarity  
- Spatial consistency  
- Amplitude and decay features  
- Trajectory stability across channels

## Outputs
- Pairwise matching scores  
- Match probabilities  
- Diagnostic summaries

## Notes
During development, one issue encountered was reuse of previous parameter structures, where session fields could silently retain outdated values.

Re-initializing parameters for each run resolved this issue and improved robustness.

---

# Step 3A

# Raw Waveform Extraction
Per-unit raw spike waveforms are extracted from the original recordings for each session.

These waveforms are generated once and reused across downstream steps.

Benefits:

- Avoid repeated access to large raw files  
- Faster downstream analysis  
- Consistent waveform inputs for validation

---

# Step 3B

# Spike-time ACG Augmentation
Per-session SST files are augmented with:

- Spike times  
- Auto-correlograms (ACGs)

ACGs are computed directly from Kilosort outputs.

This provides a validation signal independent of waveform features.

---

# Step 3C

# Waveform-based SST Construction
Per-session SST structures are built using real raw waveforms from high-quality units.

For each unit:

- Mean waveform is computed  
- Standard deviation waveform is computed  
- Signals are aligned around peak channel and peak time

Default representation:

- 8 channels × 65 samples

These files serve as the waveform backbone for downstream validation.

---

# Step 3D

# High-confidence Pair Visualization
High-confidence cross-day matches are selected from the UnitMatch MatchTable.

Current threshold used:

- MatchProb ≥ 0.95

For selected pairs, the workflow plots:

- Normalized mean waveforms  
- Auto-correlograms

This supports manual inspection of candidate matches.

## Current Observation
Some high-probability pairs show strong agreement across waveform and ACG structure.

Others show partial disagreement or mismatch, suggesting that probabilistic matching scores should be interpreted with caution.

---

# CURRENT FINDINGS
- High-confidence candidate pairs can be identified across sessions  
- Waveform and firing-pattern agreement is common but not universal  
- Some matches likely reflect ambiguity rather than true identity continuity  
- Independent validation adds useful structure beyond match scores alone

---

# LIMITATIONS
- No ground-truth neuron identity across days  
- Current review still includes manual inspection  
- No strict one-to-one constraint in the current matching stage  
- Larger multi-session datasets are still being processed

---

# NEXT STEPS
- Apply pipeline to larger datasets  
- Develop automated validation metrics  
- Add one-to-one matching constraints where appropriate  
- Extend tracking across more sessions  
- Quantify agreement between match probability and validation signals

---

# STATUS
This is an active and ongoing project. The repository will be updated as analysis progresses.
