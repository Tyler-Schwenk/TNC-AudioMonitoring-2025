# Final Model Analysis

## Key

Three models will be discussed throughout this analysis:

* [**2024 model**](2024-model.md) - My previously developed model, that was used during the 2024/2025 audio monitoring season for RADR.
* [**F1 model**](../setup-workflow.md#high-f1-model) - My new highest performing model created for this contract. This model has the highest discriminatory power (F1, AUC) and is technically the best performing classifier.
* [**Precision model**](../setup-workflow.md#recommended-high-precision-model) - Another new model created for this contract. This model excels at our target task of maximizing precision with the goal of reducing false positive review workload. It comes at a cost to recall as compared to the F1 model.

## Key improvements

The improvements of this year's best model can be summarized by a few key changes;

* An increase in stability across Sensitivity values and threshold settings.
* More balanced precision-recall tradeoff, favoring stronger precision.
* More generalized model, with stronger performance under domain shift.

A full comparison of metrics to the previous 2024 model and be found [here](comparative-analysis.md)

***

## Metrics Overview

#### Operating-Point Summary (OOD)

| Configuration Goal  | F1    | Precision | Recall |
| ------------------- | ----- | --------- | ------ |
| **Best Overall F1** | 88.6% | 89.7%     | 87.5%  |
| **High-Precision**  | 76.1% | 98.5%     | 62.0%  |
| **2024**            | 80.3% | 76.0%     | 85.1%  |

***

## Daily Presence/Absence Detection

The primary use-case for this model is for daily presence/absence detections for audio monitoring at the Santa Rosa Plateau. For this reason, I used records from the 2024/2025 audio monitoring season to estimate the practicality of these models for real world deployment.

| Metric                                     | F1 Model   | Precision Model | 2024        |
| ------------------------------------------ | ---------- | --------------- | ----------- |
| Daily Detection Accuracy                   | 99.0%      | 95.5%           | 98.8%       |
| False Positive Burden; Flagged Audio/Night | 45 minutes | 7 minutes       | 104 minutes |
| False positive files/night                 | 886        | 121             | 2,066       |
