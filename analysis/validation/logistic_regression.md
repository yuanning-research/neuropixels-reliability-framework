## Feature Correlation Analysis

Before fitting logistic regression models, correlations among candidate predictors were examined to identify redundant features and reduce coefficient instability.

The initial feature set included MatchProb, TotalScore, EucledianDistance, CentroidDist, WavformSim, CentroidOverlord, and spatialdecaySim. Correlation analysis showed that EucledianDistance and CentroidDist were perfectly anti-correlated (r = -1.00), indicating that they represented the same spatial information in opposite directions. To avoid redundant predictors, CentroidDist was excluded from the logistic regression models.

After removing CentroidDist, the final feature set included:

- MatchProb
- TotalScore
- EucledianDistance
- WavformSim
- CentroidOverlord
- spatialdecaySim

The remaining features showed moderate correlations but no perfect or near-perfect redundancy. The strongest remaining correlation was between MatchProb and CentroidOverlord (r = 0.66), followed by WavformSim and CentroidOverlord (r = 0.55), MatchProb and WavformSim (r = 0.54), MatchProb and TotalScore (r = 0.54), TotalScore and EucledianDistance (r = -0.55), and TotalScore and spatialdecaySim (r = 0.52).

These results support the use of a reduced six-feature set for subsequent interpretable logistic regression analyses.

## Logistic Regression Analysis

To further examine which features contributed to manual review decisions, logistic regression models were fitted using the six selected features. Two complementary outcomes were analyzed:

- Direction (Match vs. Mismatch)
- Resolution (Resolved vs. Uncertain)

All predictor variables were standardized prior to model fitting to allow direct comparison of coefficient magnitudes.

### Direction Analysis

For Direction labels, univariate logistic regression showed that several similarity-related features were significantly associated with Match/Mismatch decisions, including MatchProb, TotalScore, CentroidOverlord, and spatialdecaySim. WavformSim showed a similar trend, while EucledianDistance was not significantly associated with Direction.

In the multivariate model, most individual features lost significance after accounting for shared information among predictors. TotalScore retained the strongest association with Direction decisions, suggesting that manual Match/Mismatch judgments are driven by the combined evidence captured by multiple similarity metrics rather than by any single feature alone.

### Resolution Analysis

For Resolution labels, a different pattern emerged. Univariate logistic regression identified EucledianDistance as the strongest predictor of whether a candidate pair could be confidently resolved. Larger distances were associated with a higher likelihood of uncertainty. MatchProb showed a weaker but similar trend.

Unlike Direction decisions, waveform-related and overlap-related features contributed relatively little to Resolution. This suggests that the ability to confidently resolve a candidate pair depends more strongly on spatial consistency than on overall similarity.

### Summary

Together, these analyses indicate that Direction and Resolution capture distinct aspects of the cross-day matching problem.

- Direction decisions are primarily associated with similarity-related evidence.
- Resolution decisions are more strongly influenced by spatial consistency and confidence of the available evidence.

These findings support the distinction between algorithmic confidence and evidential confidence observed during manual review and reinforce the conclusion that Match/Mismatch classification and uncertainty assessment should be considered separately.

## Generalization Beyond Neuron Matching

This project treats cross-day neuron matching as a case study for a broader problem in computational biology: how to evaluate predicted relationships between biological entities when model confidence and independent evidence do not fully agree.

In this setting, a candidate neuron pair can be viewed as a predicted biological relationship. UnitMatch provides an algorithmic confidence score, while waveform morphology and ACG structure provide independent evidence. The analysis showed that high algorithmic confidence did not always correspond to high evidential confidence, and that uncertainty often reflected incomplete or ambiguous evidence rather than simply weak similarity.

The same structure appears in many biological AI problems, including gene-disease association, drug-target prediction, perturbation-response modeling, patient stratification, and single-cell integration. In each case, the central question is not only whether a model predicts a relationship, but whether the relationship is supported, contradicted, or unresolved by available evidence.
