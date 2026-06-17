# Problem
cross-session neurons alignment is difficult since electrode drifts, physiological changes etc. we want to determine the same neuron across days/sessions.
# exsiting method
unitmatch with bombcell
## bombcell input
spike_times.npy
spike_clusters.npy
spike_templates.npy
templates.npy
amplitudes.npy
pc_features.npy
pc_feature_ind.npy
channel_positions.npy
params.py
## bombcell output
amplitude.npy
templates._bc_qMetrics_all.csv
templates._bc_qMetrics.parquet
templates.qualityMetricDetailsforGUI.mat
templates._bc_fractionRefractoryPeriodViolationsPerTauR.parquet
quality_metrics_distribution.png
waveform_classification.png
mua_units_upset.png
noise_units_upset.png
nonsomatic_units_upset.png
_bc_parameters__bc_qMetrics.parquet
## unitmatch input
spike_times.npy
spike_clusters.npy
templates.npy
channel_positions.npy
channel_map.npy
*.ap.meta
clusinfo is generated using UnitMatch helper functions (getClusinfo), based on Kilosort outputs
and QC labels, and then used as input to UnitMatch.
UnitMatch_sessionVars.mat.waveform info: RawWaveforms
UMparam（MATLAB struct）
...
## unitmatch output
AUC.mat
MatchingScores.mat
MatchProbability.bmp / MatchProbability.fig
ProbabilitiesMatches.bmp / ProbabilitiesMatches.fig
ProbabilityDistribution.bmp / ProbabilityDistribution.fig
ProjectedLocation.bmp / ProjectedLocation.fig
ScoresSelfvsMatch.bmp / ScoresSelfvsMatch.fig
TotalScore.bmp / TotalScore.fig
TotalScoreComponents.bmp / TotalScoreComponents.fig
WithinSessionDistributions.bmp / WithinSessionDistributions.fig
UnitMatch_sessionVars.mat
UnitMatch.mat
UnitMatchModel.mat

unitmatch is quite accurate to provide march probability among neurons across sessions. we can have a exact number(probability), from baiyse model(combining 6 features representing neurons well). 
# i want to improve because...
unitmatch did provide high-confidence pairs, but i think, matching neurons is not a yes or no queston, it's variable. and it's unclear how reliable these good matches are. I want to check the reliability, and the quality.
# what i did...
i re-extract the raw waveforms(contains many messy works) of high-confidence pairs, and then drew the averaged waveforms.
> jih


then i calculated the ACG of high-confidence pairs.
now i got waveforms and ACGs, i put these and the matchProb values together, and checked strong fits, poor fits and ambiguious fits from the unitmatch output.
The reason i chose waveform and ACG is, waveform can show the spaticial features of the neurons, ACG can show the temporal features of the neurons.
# what i found...
strong fits showed supports from waveform and ACG simoutainiously
poor fits showed support from neither waveform nor ACG 
while ambigious fits showed support from either waveform nor ACG only
# what suprised me...
a good tool/model like unitmatch can make mistakes and they are a lot.
# what can i do next?
what if i try more features that is seperated from the features used in unitmatch, will they also show differences? what kins of features i can use?
i can build a model, to check the reliability of models.










