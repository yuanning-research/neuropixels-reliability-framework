## Preliminary Reliability Assessment

Reviewed 83 high-confidence UnitMatch candidate pairs (MatchProb > 0.95).

Independent validation was performed using:

- waveform morphology
- autocorrelogram structure

Pairs were categorized into:

- Strong Match
- Likely Match
- Uncertain
- Likely Mismatch
- Strong Mismatch

### Results

| Category | Count |
|-----------|-------|
| Strong Match | 21 |
| Likely Match | 25 |
| Uncertain | 21 |
| Likely Mismatch | 12 |
| Strong Mismatch | 4 |

Combined outcomes:

| Outcome | Count | Percent |
|----------|-------|---------|
| Match (Strong + Likely) | 46 | 55.4% |
| Uncertain | 21 | 25.3% |
| Mismatch (Strong + Likely) | 16 | 19.3% |

### Key Observations

- High MatchProb did not always correspond to strong manual support.
- A large fraction of pairs remained uncertain despite high matching confidence.
- Waveform evidence was generally more informative than ACG evidence.

### Sources of Uncertainty

Among the 21 uncertain pairs:

| WF | ACG | Count |
|------|------|------|
| Ambiguous | Ambiguous | 18 |
| Against | Support | 2 |
| Ambiguous | Support | 1 |

Most uncertainty arose from insufficient evidence rather than direct disagreement between waveform and ACG assessments.

### Sources of Mismatch

Among the 16 mismatch pairs:

| WF | ACG | Count |
|------|------|------|
| Against | Against | 4 |
| Against | Ambiguous | 10 |
| Ambiguous | Against | 2 |

Most mismatch decisions were associated with waveform disagreement, even when ACG evidence remained inconclusive.

### Evidence Patterns

Common patterns observed during manual review:

| Outcome | Typical Evidence Pattern |
|----------|----------|
| Strong Match | WF Support + ACG Support |
| Uncertain | WF Ambiguous + ACG Ambiguous |
| Mismatch | WF Against + ACG Ambiguous |

These patterns suggest that waveform evidence often carried greater weight than ACG evidence during reliability assessment.

### Metric Observations

Average MatchProb remained high across all categories:

| Category | Mean MatchProb |
|-----------|---------------|
| Strong Match | 0.992 |
| Uncertain | 0.995 |
| Strong Mismatch | 0.971 |

This suggests that MatchProb alone may not distinguish strongly supported matches from uncertain cases and highlights the value of independent validation.

### Representative Strong Match: S1 Unit 112 ↔ S2 Unit 138

This pair was classified as a Strong Match because both waveform and ACG evidence strongly supported the match.

The waveform morphology was highly consistent across sessions. The trough timing, waveform width, channel spread, and overall shape were nearly identical. The ACG profiles also showed a closely matched refractory dip and recovery pattern.

This pair also appeared relatively isolated among nearby candidate pairs. Neighboring pairs had somewhat similar ACG structure, but their waveforms showed clearer differences, suggesting that this pair had the strongest combined evidence.

Overall, this case represents a high-confidence match supported by both morphology and firing-pattern evidence.

### Representative Uncertain Case: S1 Unit 221 ↔ S2 Unit 266

This pair was classified as Uncertain because neither evidence source provided a confident validation signal.

The waveform showed partial similarity, but one side contained an abrupt flat segment, suggesting possible truncation, padding, or waveform extraction artifact rather than a clean biological waveform difference. The ACG was also sparse and did not provide a clear refractory/recovery structure.

This case represents an uncertainty pattern driven mainly by insufficient or unreliable evidence, rather than direct disagreement between waveform and ACG.

### Representative Likely Mismatch: S1 Unit 214 ↔ S2 Unit 236

This pair was classified as a Likely Mismatch despite a high MatchProb (0.997).

The waveform similarity metric remained relatively high (WavformSim = 0.875), but visual inspection suggested notable differences in waveform morphology. The overall waveform shapes appeared broader and more asymmetric across sessions, making it difficult to interpret them as a convincing continuation of the same unit.

The waveform was also affected by an abrupt truncation pattern similar to that observed in some uncertain cases. However, unlike the uncertain example, the underlying waveform structure still appeared meaningfully different after accounting for this artifact.

The ACG provided limited evidence and was largely uninformative due to sparse spike counts. As a result, the classification was driven primarily by waveform disagreement rather than firing-pattern evidence.

This case illustrates that relatively high similarity scores do not always correspond to convincing biological matches and highlights the importance of visual inspection when evaluating high-confidence candidate pairs.

### Preliminary Interpretation

Several themes emerged from manual review.

First, waveform morphology consistently provided the most informative validation signal. Most mismatch decisions were associated with waveform disagreement even when ACG evidence remained ambiguous.

Second, many uncertain cases were driven by insufficient evidence rather than direct conflict between evidence sources. Sparse ACGs and incomplete waveform profiles frequently limited confident interpretation.

Third, manual review itself introduced uncertainty. Some pairs were difficult to classify consistently across multiple review passes, suggesting that reliability assessment should be viewed as a probabilistic process rather than a source of absolute ground truth.

Together, these observations suggest that high UnitMatch confidence scores alone may not fully capture match reliability and that independent evidence remains important for interpreting candidate neuron matches.

#### 也许UnitMatch 太标准化，不能处理真实数据中的异常情况？

### Preliminary Feature Exploration

Several UnitMatch features were compared across manually assigned reliability categories using boxplots.

Initial observations:

- MatchProb remained high across all categories, including uncertain and mismatch cases.
- Strongly supported matches tended to show higher values for some spatial and waveform-related features.
- Uncertain cases did not consistently fall between matches and mismatches, suggesting that uncertainty may reflect insufficient evidence rather than intermediate reliability.
- Some feature distributions showed substantial overlap across categories, indicating that individual UnitMatch metrics alone may not fully explain manual confidence assessments.

These results suggest that manual validation captures information beyond MatchProb alone and motivate further investigation into how different evidence sources contribute to reliability assessment.

One emerging observation is that uncertain cases may represent a distinct class driven by limited or ambiguous evidence, rather than simply occupying a midpoint between supported and unsupported matches.

Manual review was treated as an evidence-based assessment process rather than absolute ground truth.
