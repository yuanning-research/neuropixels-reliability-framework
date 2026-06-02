# Bombcell Pipeline Adaptation Notes

## Dataset Transition

The original Bombcell workflow was first developed and tested on a smaller two-session dataset.

The current version was adapted for a four-session dataset (AA23), which introduced minor differences in dataset organization and metadata structure.

Several updates were made to improve pipeline robustness and compatibility with the current Bombcell version.

---

## Issues Encountered

### 1. Bombcell API mismatch

Problem:

runAllQualityMetrics(...) in the current Bombcell version required an additional savePath input argument.

The original script failed with:

Not enough input arguments

Fix:

Added outDir as the final input argument.

[qMetric, unitType] = bc.qm.runAllQualityMetrics( ...
    param, spikeTimes_samples, spikeClusters, ...
    templateWaveforms, templateAmplitudes, ...
    pcFeatures, pcFeatureIdx, channelPositions, outDir);

---

### 2. Recursive metadata search returned multiple meta files

Problem:

The original workflow used recursive metadata search:

dir(fullfile(sessionPath, '**', '*imec0.ap.meta'))

This worked for the earlier dataset, where only one metadata file was present.

The new dataset contained additional original_data directories, causing multiple .meta files to be returned. This produced malformed metadata paths inside qualityParamValues(...).

Fix:

Restricted metadata search to the session root:

dir(fullfile(sessionPath, '*imec0.ap.meta'))

---

### 3. Deprecated saveMetrics call

Problem:

The original script explicitly called:

bc.save.saveMetrics(...)

This function was unavailable in the current Bombcell version.

Observation:

runAllQualityMetrics(...) already performs internal saving when savePath is provided.

Fix:

Removed the explicit saveMetrics call and used Bombcell's built-in saving behavior.

---

## Current Status

Bombcell quality metrics were successfully generated for all four sessions.

Outputs include:

- qMetric files
- unit classification results
- QC figures
- TSV / parquet exports
- GUI-compatible outputs
