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
