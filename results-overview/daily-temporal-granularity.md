# Daily Temporal Granularity



best config for f1: sens .75, threshold 1.0

f1: .886, precision: .897, recall: .875

Assuming a recording schedule used during the 2024/2025 season:\
5pm to 11pm, 9 min off, 1 minute on, 432 1-minute files.&#x20;





High precision option:

Sens 1.5, threshold: 0.3;

F1: 76.1, Precision: 98.5, Recall: 62.0

adjust threshold to 0.05;&#x20;

F1: 80.0, Precision: 93.6, Recall: 70.0



**Context & Methodology:**

To estimate real-world performance at daily temporal granularity, I analyzed calling activity from the 2024/2025 field season for days where positive RADR detections occurred. this included 9 recorders and 139 recording nights.&#x20;

This revealed typical calling patterns. In days where RADR calls were identified median of 20 positive files/night, with 84% of nights having ≥5 calls. 16% have only one file

Our recording schedule (5pm-11pm, 1 min on / 9 min off) produces **432 1-minute files per night**, which are split into **8,640 3-second segments** for model inference. We use this ground truth to project false positive burden and detection confidence under different model configurations.

***

#### Expected performance for Daily Detections

| Files/Night | % of Nights  | Detection Probability (Best F1) | Detection Probability (High Precision) |
| ----------- | ------------ | ------------------------------- | -------------------------------------- |
| 1 file      | 16%          | 87.5%                           | 62.0%                                  |
| 5 files     | 25th %ile    | 99.97%                          | 99.0%                                  |
| 20 files    | Median (50%) | >99.9999%                       | >99.9999%                              |
| 53 files    | 75th %ile    | \~100%                          | \~100%                                 |

***

#### Trade-Off Analysis

| Metric                              | Best F1 Model | High Precision Model |
| ----------------------------------- | ------------- | -------------------- |
| **Review burden**                   | 45 min/night  | 7 min/night          |
| **FP per night (3-sec segments)**   | 888           | 129                  |
| **Detection (median night)**        | >99.9999%     | >99.9999%            |
| **Detection (quiet 1-call nights)** | 87.5%         | 62.0%                |

***

#### Recommendation

**For daily presence/absence monitoring, the High Precision Model is strongly recommended:**

**Key Benefits:**

* **85% reduction in false positives** (129 vs 888 per night)
* **Saves 88 hours of review time** per season (16 vs 104 hours total)
* **Still maintains >99% detection confidence on 84% of nights with positive detections** (those with ≥5 calls)
* **4.6× better signal-to-noise ratio** (8.8% vs 1.9%)

**Acceptable Trade-Off:**

* **Lower recall** (62% vs 87.5%) primarily affects the rarest scenario: single-call nights (16% of nights)
* On typical calling nights (median 20 calls), both models achieve >99.9999% detection probability
* The F1 drop (0.886 → 0.761) is acceptable when review burden is the primary constraint

**Mitigation Strategy for Low-Call Nights:**

* Days with 0 detections: Flag 10-20% for manual spot-check validation
* Document any systematic patterns in missed detections
* High confidence in "presence" calls (98.5% precision means false positives are rare)

**Bottom Line:** The High Precision Model reduces workload by 85% while maintaining excellent performance for the primary use case of daily presence/absence determination. The lower recall on rare single-call nights is an acceptable trade-off for the dramatic reduction in false positives.



{% file src="../.gitbook/assets/positive_counts_by_recorder_date (1).txt" %}
