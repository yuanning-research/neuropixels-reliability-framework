# Neuropixels Cross-day Matching
This project studies cross-day neuron matching in chronic Neuropixels recordings using spike sorting outputs and independent validation analyses.

## Goal
Track putative neurons across recording sessions and evaluate the reliability of probabilistic matching outputs.

## Methods
- Quality filtering of sorted units
- Cross-session matching using UnitMatch
- Re-extraction of waveform summaries from raw recordings
- Auto-correlogram analysis from spike times
- Review of high-confidence matched pairs

## Key Results
- Identified high-confidence cross-day candidate pairs
- Observed both agreement and mismatch patterns across waveform and firing signatures
- Built a framework for future larger-scale validation

## Tools
MATLAB, Python, neural data analysis

## Repository Structure
- notebooks/: exploratory analysis or summaries
- scripts/: MATLAB / Python utilities
- figures/: selected validation outputs
