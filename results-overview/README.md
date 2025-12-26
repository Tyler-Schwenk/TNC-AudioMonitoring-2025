# Final Model Analysis

## Key improvements

The improvements of this year's best model can be summarized by a few key changes;

* An increase in stability across Sensitivity values and threshold settings.
* More balanced precision-recall tradeoff, favoring stronger precision.
* More generalized model, stronger performance under domain shift.

A full comparison to the previous 2024 model and be found [here](./#comparative-analysis)

***

## Metrics Overview

#### Operating-Point Summary (OOD)

Two models are shown for different use cases.

| Configuration Goal        | F1    | Precision | Recall |
| ------------------------- | ----- | --------- | ------ |
| **Best Overall F1**       | 88.6% | 89.7%     | 87.5%  |
| **High-Precision Option** | 76.1% | 98.5%     | 62.0%  |

***

## Daily Prsence/Absence Detection

The primary use-case for this model is for daily presence/absence detections for audio monitoring at the Santa Rosa Plateau. For this reason, I used records from the 2024/2025 audio monitoring season to estimate the practicality of these models for real world deployment

COmpare TO PREVIOUS MODEL AS WELL
