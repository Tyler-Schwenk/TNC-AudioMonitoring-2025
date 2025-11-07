---
description: 10/28/2025
---

# --Error found in Evaluation--

After the third stage of sweeps, an error was found in the post-inference evaluation script that resulted in our models appearing to be performing worse than reality. After discovering the error, all models were reevaluated with the correct logic. This showed us that our models were performing better than expected, but our understanding of how our hyperparameters effected model performance needed to be reevaluated. Below is a description of the error and how it effected the data.

### Problem:

The evaluation pipeline aggregated at the wrong granularity. The ground truth is at the file level (file contains the target species or not), but the scoring came from per-row confidences. Without consolidating those confidences per-file (e.g., by using the maximum RADR confidence per file), negative rows diluted the true positive signal.

### Effect:

* For positive files: if RADR was below threshold but a Negative row existed, the file’s positives were undercounted (recall was penalized) and negatives overcounted (precision skewed).
* For negative files: Negative rows inflated true negatives, but if a RADR row also slipped in below threshold, it wasn’t properly accounted for as a false positive at the file level.
* Reported false negatives were inflated, precision/recall degraded.
* ROC/PR curves became misleading because the “unit” was inconsistent.

#### Fix implemented

* Compute a single score per file: the maximum RADR confidence for that file (0.0 if RADR never appears).
* Threshold that file-level score to decide RADR vs Negative for the file.
* Compute metrics/curves from these file-level predictions.

### How our outputs changed

Below is are the full evaluation metrics for all experiments from before and after they were reevaluated.

{% file src="../../.gitbook/assets/all_experiments.csv" %}

{% file src="../../.gitbook/assets/all_experiments_new.csv" %}

#### Performance Change Overview

| Stage       | Old F1 | New F1 | Δ F1      | Old Precision | New Precision | Δ P       | Old Recall | New Recall | Δ R       |
| ----------- | ------ | ------ | --------- | ------------- | ------------- | --------- | ---------- | ---------- | --------- |
| **Stage 1** | 0.30   | 0.84   | **+0.54** | 0.48          | 0.73          | **+0.25** | 0.29       | 0.99       | **+0.70** |
| **Stage 2** | 0.51   | 0.82   | **+0.31** | 0.58          | 0.75          | **+0.18** | 0.55       | 0.93       | **+0.38** |
| **Stage 3** | 0.60   | 0.72   | **+0.12** | 0.77          | 0.86          | **+0.09** | 0.61       | 0.71       | **+0.10** |
| **Stage 4** | 0.64   | 0.76   | **+0.12** | 0.70          | 0.80          | **+0.10** | 0.71       | 0.81       | **+0.10** |
