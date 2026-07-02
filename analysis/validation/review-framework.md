# Manual Review Framework

To independently evaluate high-confidence UnitMatch predictions, each candidate pair was reviewed using two evidence sources:

- waveform morphology
- autocorrelogram (ACG) structure

UnitMatch predictions and MatchProb values were not considered during evidence assessment. The goal was to determine whether independent biological evidence supported the predicted relationship.

## Waveform Assessment

Waveform evidence was assigned to one of three categories.

| Label | Description |
|---------|---------|
| Support | Overall waveform morphology was consistent across sessions, including waveform shape, trough/peak timing, waveform width, relative channel amplitudes, and spatial propagation pattern. Minor amplitude differences were allowed if the overall morphology remained stable. |
| Ambiguous | Waveform quality or interpretability was insufficient for a confident judgment due to low signal-to-noise ratio, extraction artifacts, waveform truncation, baseline instability, or partial similarity. |
| Against | Clear differences were observed in waveform morphology, channel profile, or spatial propagation pattern that were unlikely to be explained by recording variability alone. |

## ACG Assessment

Autocorrelograms were evaluated as an independent measure of firing behavior.

| Label | Description |
|---------|---------|
| Support | Similar refractory period, recovery profile, central dip, and overall firing pattern across sessions. |
| Ambiguous | Sparse spikes, noisy autocorrelograms, poorly defined refractory periods, or insufficient structure for reliable interpretation. |
| Against | Clear differences in refractory structure, recovery profile, or overall firing pattern. |

## Reliability Categories

Waveform and ACG evidence were combined to assign each candidate pair to one of five review categories.

| Category | Typical Evidence Pattern |
|---------|---------|
| Strong Match | Waveform Support + ACG Support |
| Likely Match | Waveform Support + ACG Ambiguous |
| Uncertain | Ambiguous evidence, insufficient evidence, or conflicting evidence |
| Likely Mismatch | Waveform Against + ACG Ambiguous, or Waveform Ambiguous + ACG Against |
| Strong Mismatch | Waveform Against + ACG Against |

## Direction and Resolution Assessments

To facilitate later analyses, reliability categories were further summarized into two orthogonal review dimensions.

### Direction Assessment

| Direction | Categories |
|------------|------------|
| Match | Strong Match, Likely Match |
| Mismatch | Strong Mismatch, Likely Mismatch |
| Unknown | Uncertain |

Direction assessment reflects the biological interpretation of whether two recordings likely originated from the same neuron.

### Resolution Assessment

| Resolution | Categories |
|------------|------------|
| Resolved | Strong Match, Likely Match, Likely Mismatch, Strong Mismatch |
| Uncertain | Uncertain |

Resolution assessment reflects whether the available evidence was sufficient to support a confident conclusion, regardless of whether the final conclusion was match or mismatch.

This distinction separates biological direction from evidential confidence. For example, Strong Match and Strong Mismatch represent opposite biological conclusions but both correspond to highly resolved assessments.

## Review Philosophy

Manual review was treated as an evidence-based assessment process rather than absolute ground truth.

The objective was not to determine whether a prediction was definitively correct, but rather to evaluate the degree to which independent biological evidence supported, contradicted, or failed to resolve the predicted relationship. Uncertainty was therefore retained as an explicit outcome whenever available evidence was insufficient for a confident judgment.

