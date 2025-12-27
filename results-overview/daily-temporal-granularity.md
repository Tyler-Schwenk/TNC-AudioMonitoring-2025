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

#### False Absence Risk by Calling Activity

**Probability of missing detection = (1 - Recall)^N**, where N = number of positive files

| Scenario                 | Nights (%) | Best F1 Model | High Precision Model |
| ------------------------ | ---------- | ------------- | -------------------- |
| **1 file**               | 11 (7.9%)  | 12.5% miss    | 38.0% miss           |
| **5 files** (25th %ile)  | \~25%      | 0.03% miss    | 1.0% miss            |
| **20 files** (median)    | \~50%      | <0.0001% miss | <0.0001% miss        |
| **53 files** (75th %ile) | \~75%      | negligible    | negligible           |

#### Expected Nights with Missed Detection Per Season

Out of 139 recording nights with RADR present:

| Model                    | Expected Missed Nights/Season     |
| ------------------------ | --------------------------------- |
| **Best F1 Model**        | **1.4 nights** (11 × 0.125 = 1.4) |
| **High Precision Model** | **4.2 nights** (11 × 0.380 = 4.2) |

**Key Insight:** The high-precision model would miss RADR on approximately **3% of nights** (4.2/139) when it's actually present, compared to **1% of nights** (1.4/139) with the best F1 model.

#### Weighted False Absence Rate Across All Nights

Calculating across the full distribution:

| Model                    | Weighted False Absence Rate     |
| ------------------------ | ------------------------------- |
| **Best F1 Model**        | **\~1%** of RADR-present nights |
| **High Precision Model** | **\~3%** of RADR-present nights |

***

#### Trade-Off Analysis

| Metric                              | Best F1 Model | High Precision Model |
| ----------------------------------- | ------------- | -------------------- |
| **Review burden**                   | 45 min/night  | 7 min/night          |
| **FP per night (3-sec segments)**   | 888           | 129                  |
| **Detection (median night)**        | >99.9999%     | >99.9999%            |
| **Detection (quiet 1-call nights)** | 87.5%         | 62.0%                |

***

####



{% file src="../.gitbook/assets/positive_counts_by_recorder_date (1).txt" %}
