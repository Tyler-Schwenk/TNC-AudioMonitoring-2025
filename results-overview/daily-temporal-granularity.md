# Daily Temporal Granularity

## Overview

Here I will compare my two models, evaluating their performance at the task of daily presence/absence monitoring, given data from the previous year's audio monitoring. The two models are:

* Precision focused model at Sensitivity: 1.5, Threshold: 0.3
* F1 focused model at Sensitivity: 0.75, Threshold: 1.0

### Model Performance Summary

| Metric                          | F1 Model       | Precision Model |
| ------------------------------- | -------------- | --------------- |
| **F1 Score**                    | 0.886          | 0.761           |
| **Precision**                   | 0.897          | 0.985           |
| **Recall**                      | 0.875          | 0.620           |
| **Daily Detection Accuracy**    | **99.0%**      | **95.5%**       |
| **False Positive Burden/Night** | **45 minutes** | **7 minutes**   |
| Total flagged positive files    | 906            | 141             |
| **Signal-to-Noise Ratio**       | 1.9%           | 8.8%            |

***

## **Context & Methodology:**

To estimate real-world performance at daily temporal granularity I analyzed calling activity from the 2024/2025 field season, collecting days where positive RADR detections occurred. This included data from 9 recorders across 139 recording nights.&#x20;

During that season the recording schedule used was from 5pm-11pm, 1 min on / 9 min off - producing **432 1-minute files per night**, which translates to **8,640 3-second segments** for model inference. This ground truth is used to project false positive burden and detection confidence under different model configurations.

#### **2024/2025 Calling Season Data Summary:**

| Files/Night | # of Nights        | % of Nights | Cumulative |
| ----------- | ------------------ | ----------- | ---------- |
| 1 file      | 11                 | 7.9%        | 7.9%       |
| 2-10 files  | 44                 | 31.7%       | 39.6%      |
| 11-25 files | 19                 | 13.7%       | 53.3%      |
| 26+ files   | 65                 | 46.7%       | 100%       |
| **Median**  | **20 files/night** | 50 %        | 50 %       |

***

## Evaluation

### False Absence Risk by Calling Activity

Probability of missing detection = (1 - Recall)^N, where N = number of positive files

| Calling Activity | Nights  | Best F1 Missed   | High Precision Missed |
| ---------------- | ------- | ---------------- | --------------------- |
| 1 file           | 11      | 1.4 nights       | 4.2 nights            |
| 2-10 files       | 44      | <1 night         | \~2 nights            |
| 11+ files        | 84      | 0 nights         | 0 nights              |
| **Total**        | **139** | **\~1.4 nights** | **\~6.2 nights**      |

#### Expected Missed Detections Per Season

| Model                    | Missed Nights    | Daily Detection Accuracy |
| ------------------------ | ---------------- | ------------------------ |
| **Best F1 Model**        | 1.4 / 139 (1.0%) | **99.0%**                |
| **High Precision Model** | 6.2 / 139 (4.5%) | **95.5%**                |

***

### Expected Review Burden

Per Median Night (20 true positives, 8,640 segments processed):

Review Time = Total Flagged Files × 3 seconds

Where: Total Flagged = (20 × Recall) + (8,620 × (1 - Precision))

| Model                    | False Positives | Total Flagged | Review Time/Night | Season Total (139 nights) |
| ------------------------ | --------------- | ------------- | ----------------- | ------------------------- |
| **Best F1 Model**        | 888 files       | 906 files     | 45 minutes        | 104 hours                 |
| **High Precision Model** | 129 files       | 141 files     | 7 minutes         | 16 hours                  |

{% file src="../.gitbook/assets/positive_counts_by_recorder_date (1).txt" %}
