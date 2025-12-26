# Daily Temporal Granularity

best config for f1: sens .75, threshold 1.0

f1: .886, precision: .897, recall: .875

Assuming a recording schedule used during the 2024/2025 season:\
5pm to 11pm, 9 min off, 1 minute on, 432 1-minute files.&#x20;



High precision option:\
Ood.F1

0.7667STD ±0.0172

Ood.Precision

0.9650STD ±0.0209

Ood.Recall

0.6370STD ±0.0333



### Daily Detection Performance Projections

**Model Performance (Best Model):**

* **Recall: 0.875** → Detects 87.5% of true frog calls
* **Precision: 0.897** → 89.7% of detections are correct (10.3% are false positives)
* **F1: 0.886**

***

#### 1. Probability of Detecting Frogs When Present

The key insight: If frogs are calling multiple times per night, you need to miss **ALL** calls to have a false absence.

**Daily Detection Confidence by Call Frequency:**

| Scenario       | True Calls/Day             | Detection Probability | False Absence Risk |
| -------------- | -------------------------- | --------------------- | ------------------ |
| **Very Quiet** | 1-2 files                  | 87.5% - 98.4%         | 12.5% - 1.6%       |
| **Quiet**      | 5 files (25th percentile)  | 99.99%                | 0.01%              |
| **Typical**    | 20 files (median)          | >99.9999%             | <0.0001%           |
| **Busy**       | 53 files (75th percentile) | \~100%                | negligible         |
| **Chorus**     | 127-645 files              | \~100%                | negligible         |

**Math:** Probability of missing all N calls = (1 - 0.875)^N = 0.125^N

**Key Findings:**

* **89% of your recording days have ≥5 positive files** → You'll have >99.99% detection confidence on most nights
* **Only 16% of days have 1 file** → These rare quiet nights have \~87.5% detection confidence
* **Bottom line: If frogs are calling, you'll almost certainly detect them**

***

#### 2. False Positive Burden (Files to Review)

This depends on how many negative files you process. Let's estimate:

**Assumptions:**

* Continuous recording: \~288 files/day (24 hours × 12 files/hour at 5-min intervals)
* OR targeted recording: \~144 files/day (12 hours overnight × 12 files/hour)

**Expected False Positives per Day:**

| Recording Strategy | Total Files | Expected True Positives (median) | Expected False Positives | Total Flagged Files | Review Burden                     |
| ------------------ | ----------- | -------------------------------- | ------------------------ | ------------------- | --------------------------------- |
| **Full 24h**       | 288 files   | 17.5 (20 × 0.875)                | \~**30 files**           | \~48 files          | **17% of day needs review**       |
| **Targeted 12h**   | 144 files   | 17.5                             | \~**15 files**           | \~33 files          | **23% of recordings need review** |

**Calculation:**

* Negative files per day = Total files - True positive files
* Model flags negatives at rate = (1 - precision) = 0.103
* Expected FP = Negative\_files × 0.103

Using median scenario (20 true positives, 144 total files):

* Negatives: 144 - 20 = 124 files
* False positives: 124 × 0.103 ≈ 12.8 → **\~13 false positives**
* Total flagged: 17.5 true + 13 false ≈ **31 files to review/day**

***

#### 3. Practical Implications

**Good News:**

* **Presence Detection: Extremely Reliable** - With median 20 calls/night, you have >99.9999% chance of detecting frogs when present
* **Even quiet nights (5 calls) give 99.99% detection confidence**

**Trade-offs:**

* **\~10% false positive rate** means roughly 1 in 10 flagged detections needs verification
* **Daily review burden: 15-30 files** depending on recording duration
* **For 139 recording days: \~2,100-4,200 total files to review** across the season

**Optimization Strategies:**

1. **Increase threshold** (reduce sensitivity) to reduce false positives
   * Trade-off: Slightly lower recall on quiet nights
   * Your stage21 experiments will show this!
2. **Use confidence scores** to prioritize review
   * High-confidence detections (>0.9) are likely real
   * Low-confidence detections (0.25-0.5) need more scrutiny
3. **Focus review on absence days**
   * Days with 0 detections are your validation targets
   * Only need to verify a sample to confirm true absence

***

#### 4. Confidence Levels for Reporting

**For Daily Presence/Absence:**

| Scenario                            | Confidence            | Justification                                |
| ----------------------------------- | --------------------- | -------------------------------------------- |
| **Detected ≥5 calls**               | **High (>99%)**       | Strong evidence, very low false absence risk |
| **Detected 1-4 calls**              | **Moderate (95-99%)** | Likely real, but verify a sample             |
| **Detected 0 calls**                | **Moderate-High**     | Likely absent IF you processed >100 files    |
| **Detected 0 calls (low coverage)** | **Low**               | Insufficient sampling                        |

**For Seasonal Patterns:**

* Your 139 recording days across 9 recorders provide strong temporal coverage
* Can confidently identify calling phenology (start/peak/end dates)
* Can detect spatial variation across recorders

**Key Question:** How many files per day are you actually processing? This will refine the false positive estimates.

*
*
*
*

<br>



{% file src="../.gitbook/assets/positive_counts_by_recorder_date (1).txt" %}
