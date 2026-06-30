# Evidence Patterns

Waveform and ACG evidence were not distributed independently (chi-square test, p = 0.0008), suggesting that the two evidence sources often provided consistent assessments of the same neuron pair.

Several recurring evidence patterns emerged during manual review:

| Waveform Evidence | ACG Evidence | Typical Outcome |
|------------------|--------------|----------------|
| Support | Support | Strong Match |
| Support | Ambiguous | Likely Match |
| Ambiguous | Ambiguous | Uncertain |
| Against | Ambiguous | Likely Mismatch |
| Against | Against | Strong Mismatch |

Most evidence combinations mapped consistently to a single reliability category. All pairs with Support + Support evidence were classified as Strong Matches, whereas all pairs with Ambiguous + Ambiguous evidence were classified as Uncertain.

ACG assessments were frequently classified as ambiguous (60.2%), making them less informative than waveform evidence in many cases. However, when clear ACG support or contradiction was present, it generally agreed with waveform-based assessments and contributed to confident classifications. Waveform disagreement frequently led to mismatch classifications even when ACG evidence was inconclusive.

Together, these observations suggest that uncertainty arose from two situations: insufficient evidence (Ambiguous + Ambiguous) and conflicting evidence (Against + Support). Reliability judgments appeared to emerge from the combination of multiple evidence sources rather than any individual metric alone.

## Feature Behavior Under Direction and Resolution Assessments

To better understand how manual review decisions were formed, feature distributions were examined under two simplified review dimensions: direction assessment (Match vs Mismatch) and resolution status (Resolved vs Uncertain). For each feature, median values, Mann–Whitney U statistics, and rank-biserial correlations (RBC) were calculated.

### Direction Assessment

The direction-based comparison revealed clearer feature separation than the earlier reliability-category analysis. Several UnitMatch features showed moderate to strong associations with manual match-versus-mismatch decisions. The strongest effects were observed for TotalScore (RBC = 0.56) and MatchProb (RBC = 0.51), followed by WavformSim (RBC = 0.36), spatialdecaySim (RBC = 0.35), and CentroidOverlord (RBC = 0.34).

These results suggest that the similarity features used by UnitMatch capture information that is broadly consistent with biological match judgments. Notably, even mismatch cases often retained high MatchProb values (median = 0.978), indicating that algorithmic confidence alone is not sufficient to guarantee a biologically convincing match.

### Resolution Assessment

Feature behavior differed when comparing resolved and uncertain cases. Distance-related features showed the strongest associations with uncertainty, with EucledianDistance (RBC = -0.33) and CentroidDist (RBC = 0.33) exhibiting larger effects than other features.

In contrast, MatchProb (RBC = -0.24) and TotalScore (RBC = -0.16) showed substantially weaker effects than in the direction analysis. Uncertain cases often retained extremely high MatchProb values (median = 0.9995), despite lacking sufficient evidence for a confident decision.

These observations suggest that uncertainty does not necessarily arise from weak feature values. Instead, uncertainty often reflects situations in which available evidence is incomplete, ambiguous, or difficult to reconcile.

### Interpretation

Together, these results indicate that match direction and evidential confidence represent distinct aspects of the cross-day matching problem. Features that help distinguish matches from mismatches do not necessarily explain why some candidate pairs remain difficult to interpret.

UnitMatch features appear to be more informative for determining match direction than for establishing confidence in a match decision. Cases with high algorithmic similarity can still require manual interpretation when supporting evidence is incomplete, conflicting, or difficult to reconcile.

This distinction motivates the separation between direction assessment and reliability assessment within the proposed evidence-based review framework.

## Sources of Uncertainty Among High-Confidence Pairs

To further investigate why some candidate pairs remained difficult to classify despite receiving extremely high UnitMatch scores, all uncertain pairs with MatchProb > 0.99 were examined individually. Sixteen of the twenty-one uncertain pairs (76.2%) exceeded this threshold, including fourteen pairs (66.7%) with MatchProb > 0.999.

These observations suggest that uncertainty is not simply a consequence of low MatchProb or weak feature values. Instead, several recurring sources of uncertainty were identified during manual review.

### Representative Sources of Uncertainty

| Source of uncertainty | Representative observations |
|---|---|
| Spatial inconsistency | High MatchProb and waveform similarity despite large EucledianDistance and reduced CentroidDist |
| Waveform extraction artifacts | Sharp truncation, flat segments, or incomplete waveform structure limiting interpretation |
| Weak supporting evidence | Sparse or uninformative ACG patterns providing little independent validation |
| Conflicting evidence | Waveform morphology and ACG patterns suggesting different conclusions |
| Potential local candidate ambiguity | Multiple nearby candidate pairs exhibiting similarly high similarity scores |

These observations are not mutually exclusive, and individual uncertain pairs often exhibited multiple sources of uncertainty simultaneously.

### Interpretation

Many high-confidence uncertain pairs combined strong similarity metrics with weak or conflicting biological evidence. A large subset showed waveform truncation or flat waveform segments that were likely related to extraction or preprocessing limitations rather than clear biological differences. In these cases, ACG patterns were often sparse or uninformative, providing little additional evidence to support or reject the match.

Distance-related inconsistencies were also common. Several pairs retained near-perfect MatchProb values and highly similar waveform shapes despite exhibiting substantial spatial separation between sessions. This observation is consistent with the feature analysis, where EucledianDistance and CentroidDist showed the strongest associations with resolution status while contributing relatively little to match-versus-mismatch direction.

A smaller subset of uncertain pairs showed disagreement between evidence sources. Examples included cases where waveform morphology differed despite similar ACG patterns, or where specific waveform components were present in one session but absent in the other. These cases illustrate situations in which no single feature provides a decisive answer and manual interpretation requires weighing multiple partially conflicting sources of evidence.

Some uncertain cases also appeared within local groups of highly similar candidate units. Although not systematically analyzed, these observations suggest that uncertainty may sometimes arise from ambiguity among multiple plausible candidates rather than from a single clearly incorrect match.

Taken together, these observations indicate that high-confidence uncertain pairs are not simply low-quality matches. Rather, they represent situations in which algorithmic similarity remains high while the available biological evidence is incomplete, inconsistent, or difficult to reconcile.

These findings further support the distinction between algorithmic confidence and evidential confidence. While UnitMatch scores can provide useful information for identifying candidate matches, they do not fully capture the quality, consistency, or interpretability of the evidence available for manual validation.
