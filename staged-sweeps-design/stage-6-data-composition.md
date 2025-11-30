---
description: >-
  FIRST!! ADD  FULL DESCRIPTOIN OF WHAT THESE SUBSETS ARE/ HOW THEY WERE
  GATHERED
---

# Stage 6: Data Composition

### Executive Summary <a href="#executive-summary" id="executive-summary"></a>

Stage 6 systematically tested the impact of curated data subsets on model performance using a 54-experiment sweep (3 seeds × 2 balance settings × 3 positive subsets × 3 negative subsets).

**Key Finding**: The combination of **top50 positive subset + hardneg\_99 negative subset + class balancing** achieved the best performance with F1=0.945 on OOD data, representing a **10.9% improvement** over the baseline (F1=0.852).



### Experimental Design <a href="#experimental-design" id="experimental-design"></a>

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Balance**: True/False (class balancing on/off)
* **Positive Subsets**:
  * None (baseline: 2,017 files)
  * small (+51 files from bestLowQuality)
  * top50 (+515 files from bestLowQuality)
* **Negative Subsets**:
  * None (baseline: 8,525 files)
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

#### How Subsets were created <a href="#evaluation-metrics" id="evaluation-metrics"></a>

* **Positive Subsets:**
  * The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model.&#x20;
  * This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through  which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted i nthe 4 folders below:\
    small: 51 (5%), medium: 154 (15%), large: 309 (30%), xl: 515 (50%)
* **Negative Subsets:**
  * I took stage3\_046

### Results Summary <a href="#results-summary" id="results-summary"></a>

#### Top 5 Configurations (Ranked by OOD F1) <a href="#top-5-configurations-ranked-by-ood-f1" id="top-5-configurations-ranked-by-ood-f1"></a>

| Rank | Config      | Balance | Pos Subset | Neg Subset  | OOD F1 ± std  | IID F1 ± std  |
| ---- | ----------- | ------- | ---------- | ----------- | ------------- | ------------- |
| 1    | 009,027,045 | Yes     | top50      | hardneg\_99 | 0.945 ± 0.030 | 0.955 ± 0.023 |
| 2    | 013,031,049 | No      | small      | none        | 0.913 ± 0.063 | 0.900 ± 0.042 |
| 3    | 003,021,039 | Yes     | none       | hardneg\_99 | 0.897 ± 0.087 | 0.846 ± 0.133 |
| 4    | 006,024,042 | Yes     | small      | hardneg\_99 | 0.872 ± 0.043 | 0.810 ± 0.073 |
| 5    | 015,033,051 | No      | small      | hardneg\_99 | 0.871 ± 0.051 | 0.844 ± 0.091 |

**Baseline** (001,019,037): none/none/balanced → OOD F1 = 0.852 ± 0.011

### Key Findings <a href="#key-findings" id="key-findings"></a>

#### 1. Curated Subsets Significantly Improve Performance <a href="#id-1-curated-subsets-significantly-improve-performance" id="id-1-curated-subsets-significantly-improve-performance"></a>

**Top50 Positive Subset Impact** (when balanced with hardneg\_99):

* Baseline (none/hardneg\_99): OOD F1 = 0.897
* With top50 (top50/hardneg\_99): OOD F1 = 0.945
* **Improvement: +0.048 F1 points (+5.4%)**

The top50 subset adds 515 high-quality positive examples (25% increase from 2,017 to 2,532), substantially improving model learning.

#### 2. Hard Negative Quality > Quantity <a href="#id-2-hard-negative-quality--quantity" id="id-2-hard-negative-quality--quantity"></a>

**Comparing negative subsets with balanced training**:

| Pos Subset | hardneg\_50 (1,401 files) | hardneg\_99 (475 files) | Difference |
| ---------- | ------------------------- | ----------------------- | ---------- |
| none       | 0.867                     | 0.897                   | +0.030     |
| small      | 0.834                     | 0.872                   | +0.038     |
| top50      | 0.865                     | 0.945                   | +0.080     |

**Finding**: Fewer but higher-confidence hard negatives (hardneg\_99) consistently outperform a larger set of medium-confidence negatives (hardneg\_50). The effect is strongest when combined with top50 positives (+0.080 F1).

**Interpretation**: Models learn better decision boundaries from truly challenging examples rather than moderately difficult ones.

#### 3. Class Balancing is Critical with Hard Negatives <a href="#id-3-class-balancing-is-critical-with-hard-negatives" id="id-3-class-balancing-is-critical-with-hard-negatives"></a>

**Effect of balance setting with hardneg\_99**:

| Pos Subset | Balanced      | Unbalanced    | Difference |
| ---------- | ------------- | ------------- | ---------- |
| none       | 0.897 ± 0.087 | 0.498 ± 0.327 | -0.399     |
| small      | 0.872 ± 0.043 | 0.871 ± 0.051 | -0.001     |
| top50      | 0.945 ± 0.030 | 0.599 ± 0.346 | -0.346     |

**Critical Observation**: Unbalanced training with hardneg\_99 shows:

1. **Catastrophic performance drop**: -0.346 to -0.399 F1 for none/top50
2. **High variance**: std > 0.3 (vs < 0.1 for balanced)
3. **Precision-recall imbalance**: High precision (0.88-0.92) but very low recall (0.41-0.56)

**Root Cause**: Without balancing, the dataset becomes heavily negative-skewed (e.g., 2,532 pos / 9,000 neg = 1:3.6 ratio). The abundance of hard negatives causes the model to become overly conservative.

**Exception**: small subset with hardneg\_99 maintains performance when unbalanced (0.871 vs 0.872). This anomaly warrants further investigation.

#### 4. Small Positive Subset Shows Mixed Results <a href="#id-4-small-positive-subset-shows-mixed-results" id="id-4-small-positive-subset-shows-mixed-results"></a>

**Performance with small subset** (51 files added):

| Neg Subset  | Balance | OOD F1 | vs Baseline (none/none) |
| ----------- | ------- | ------ | ----------------------- |
| none        | Yes     | 0.783  | -0.069 (worse)          |
| none        | No      | 0.913  | +0.068 (better)         |
| hardneg\_99 | Yes     | 0.872  | +0.020 (better)         |
| hardneg\_99 | No      | 0.871  | +0.019 (better)         |

**Interpretation**:

* When paired with hard negatives, small subset provides modest improvement
* When used alone with balance=Yes, performance decreases vs baseline
* Best performance with small subset is when unbalanced with no negative subset (F1=0.913)

The inconsistent results suggest the small subset may contain heterogeneous quality samples.

#### 5. Model Stability Across Seeds <a href="#id-5-model-stability-across-seeds" id="id-5-model-stability-across-seeds"></a>

**Standard deviation analysis**:

* **Balanced configurations**: std typically 0.02-0.09 (good stability)
* **Unbalanced + hardneg\_99**: std 0.31-0.35 (poor stability)
* **Top performer (009,027,045)**: std = 0.030 OOD, 0.023 IID (excellent stability)

Low variance across seeds indicates robust training configurations. High variance in unbalanced+hardneg\_99 experiments suggests training instability or seed-dependent failure modes.

### Performance Characteristics <a href="#performance-characteristics" id="performance-characteristics"></a>

#### Precision vs Recall Trade-offs <a href="#precision-vs-recall-trade-offs" id="precision-vs-recall-trade-offs"></a>

**Top configurations show excellent precision-recall balance**:

| Config                     | OOD Precision | OOD Recall    | Balance        |
| -------------------------- | ------------- | ------------- | -------------- |
| top50/hardneg\_99/balanced | 0.910 ± 0.047 | 0.984 ± 0.014 | Excellent      |
| small/none/unbalanced      | 0.844 ± 0.112 | 1.000 ± 0.001 | Recall-favored |
| none/hardneg\_99/balanced  | 0.826 ± 0.149 | 0.992 ± 0.009 | Recall-favored |

**Worst configurations are precision-dominated**:

| Config                       | OOD Precision | OOD Recall    | Issue             |
| ---------------------------- | ------------- | ------------- | ----------------- |
| none/hardneg\_99/unbalanced  | 0.924 ± 0.070 | 0.407 ± 0.343 | Extreme imbalance |
| top50/hardneg\_99/unbalanced | 0.879 ± 0.103 | 0.558 ± 0.393 | Extreme imbalance |

Models trained without balancing on hard negatives become overly conservative, rejecting positive examples to avoid false positives.

#### IID vs OOD Generalization <a href="#iid-vs-ood-generalization" id="iid-vs-ood-generalization"></a>

**Generalization gap (IID F1 - OOD F1)**:

| Config                     | IID F1 | OOD F1 | Gap    | Assessment               |
| -------------------------- | ------ | ------ | ------ | ------------------------ |
| top50/hardneg\_99/balanced | 0.955  | 0.945  | +0.010 | Excellent generalization |
| small/none/unbalanced      | 0.900  | 0.913  | -0.013 | Better on OOD (unusual)  |
| small/none/balanced        | 0.759  | 0.783  | -0.024 | Better on OOD            |
| none/hardneg\_99/balanced  | 0.846  | 0.897  | -0.051 | Generalizes well         |

**Observation**: Most configurations generalize well to OOD data (gap < 0.05). Some show better OOD than IID performance, suggesting the IID test set may be slightly harder or that hard negatives improve robustness.

### Worst Performers <a href="#worst-performers" id="worst-performers"></a>

#### Bottom 2 Configurations <a href="#bottom-2-configurations" id="bottom-2-configurations"></a>

| Rank | Config      | Balance | Pos/Neg Subset    | OOD F1 ± std  | Issue                     |
| ---- | ----------- | ------- | ----------------- | ------------- | ------------------------- |
| 18   | 012,030,048 | No      | none/hardneg\_99  | 0.498 ± 0.327 | High variance, low recall |
| 17   | 018,036,054 | No      | top50/hardneg\_99 | 0.599 ± 0.346 | High variance, low recall |

**Common pattern**: Both are unbalanced with hardneg\_99 negative subset.

* Extremely high variance (std > 0.3) indicates unreliable training
* Precision stays high (0.88-0.92) but recall collapses (0.41-0.56)
* Class imbalance with difficult negatives creates pathological behavior

### Statistical Significance <a href="#statistical-significance" id="statistical-significance"></a>

**Confidence in top performer** (top50/hardneg\_99/balanced):

* Mean OOD F1: 0.945 ± 0.030
* 95% CI: \[0.892, 0.998] (assuming normal distribution with n=3)
* Improvement over baseline: +0.093 F1 points
* Cohen's d effect size vs baseline: 4.2 (very large effect)

**Note**: Limited sample size (n=3 seeds) means confidence intervals are wide. Statistical testing would benefit from additional seed replicates.

### Recommendations <a href="#recommendations" id="recommendations"></a>

#### For Production Models <a href="#for-production-models" id="for-production-models"></a>

1. **Use top50 + hardneg\_99 + balance=True**
   * Highest performance (OOD F1 = 0.945)
   * Excellent stability (std = 0.030)
   * Balanced precision/recall (0.91/0.98)
   * Strong generalization (IID/OOD gap = 0.010)
2. **Always enable class balancing when using hard negatives**
   * Prevents precision/recall imbalance
   * Reduces training variance
   * Essential for model stability
3. **Prioritize hard negative quality over quantity**
   * 475 files @ 99% confidence > 1,401 files @ 50% confidence
   * Focus curation efforts on truly challenging examples

#### For Future Experimentation <a href="#for-future-experimentation" id="for-future-experimentation"></a>

1. **Investigate small subset anomaly**
   * Why does small/none/unbalanced (013,031,049) achieve OOD F1=0.913?
   * Examine the 51 files in small subset for quality patterns
   * Test with more seeds to confirm stability
2. **Expand top50 curation**
   * Top50 provides clear performance gains (+515 files → +0.048 F1)
   * Document curation criteria for reproducibility
   * Consider expanding to top100 or similar
3. **Test intermediate hard negative thresholds**
   * Large gap between hardneg\_50 and hardneg\_99 (1,401 vs 475 files)
   * Test hardneg\_75 or hardneg\_85 as middle ground
   * Balance quality vs quantity trade-off
4. **Add more seed replicates**
   * Current n=3 limits statistical power
   * Increase to n=5-10 for tighter confidence intervals
   * Especially important for configs with high variance

### Data Composition Details <a href="#data-composition-details" id="data-composition-details"></a>

#### Final Training Set Sizes <a href="#final-training-set-sizes" id="final-training-set-sizes"></a>

| Balance | Pos Subset | Neg Subset  | Pos Count | Neg Count | Total  |
| ------- | ---------- | ----------- | --------- | --------- | ------ |
| Yes     | none       | none        | 2,017     | 2,017     | 4,034  |
| Yes     | none       | hardneg\_50 | 2,017     | 2,017     | 4,034  |
| Yes     | none       | hardneg\_99 | 2,017     | 2,017     | 4,034  |
| Yes     | small      | none        | 2,068     | 2,068     | 4,136  |
| Yes     | small      | hardneg\_50 | 2,068     | 2,068     | 4,136  |
| Yes     | small      | hardneg\_99 | 2,068     | 2,068     | 4,136  |
| Yes     | top50      | none        | 2,532     | 2,532     | 5,064  |
| Yes     | top50      | hardneg\_50 | 2,532     | 2,532     | 5,064  |
| Yes     | top50      | hardneg\_99 | 2,532     | 2,532     | 5,064  |
| No      | none       | none        | 2,017     | 8,525     | 10,542 |
| No      | none       | hardneg\_50 | 2,017     | 9,926     | 11,943 |
| No      | none       | hardneg\_99 | 2,017     | 9,000     | 11,017 |
| No      | small      | none        | 2,068     | 8,525     | 10,593 |
| No      | small      | hardneg\_50 | 2,068     | 9,926     | 11,994 |
| No      | small      | hardneg\_99 | 2,068     | 9,000     | 11,068 |
| No      | top50      | none        | 2,532     | 8,525     | 11,057 |
| No      | top50      | hardneg\_50 | 2,532     | 9,926     | 12,458 |
| No      | top50      | hardneg\_99 | 2,532     | 9,000     | 11,532 |

**Note**: When balance=True, negative count is downsampled to match positive count. Hard negatives are mixed into the balanced sample proportionally (not added separately).

### Methodology Notes <a href="#methodology-notes" id="methodology-notes"></a>

#### Subset Addition Process <a href="#subset-addition-process" id="subset-addition-process"></a>

1. **Filter manifest**: Apply quality filters to base dataset
2. **Add subsets**: Concatenate curated subset files
3. **Apply balance**: If enabled, downsample to min(pos\_count, neg\_count)

**Important**: When balanced, hard negatives are sampled proportionally. For example:

* hardneg\_99 (475 files) + manifest (8,525) = 9,000 total negatives
* When balanced to 2,017: \~475/9000 × 2,017 = \~107 hard negatives in final set (5.3%)
* Remaining \~1,910 negatives come from manifest

#### Reproducibility <a href="#reproducibility" id="reproducibility"></a>

* All experiments use deterministic sampling with fixed seeds
* Seeds: 123, 456, 789
* Same base hyperparameters across all experiments (50 epochs, lr=0.0005, batch=32, etc.)

### Conclusion <a href="#conclusion" id="conclusion"></a>

Stage 6 demonstrates that **strategic data curation significantly improves model performance**. The optimal configuration combines:

1. **High-quality positive augmentation** (top50: +515 files, +25%)
2. **High-confidence hard negatives** (hardneg\_99: +475 files at 99% conf)
3. **Class balancing** to prevent negative-class dominance

This achieves **OOD F1 = 0.945**, a **10.9% improvement** over baseline, with excellent stability and generalization. The results strongly support investing in curated hard negative mining and positive example expansion for future model iterations.

**Critical Lesson**: When working with hard negatives, class balancing is not optional—it's essential for stable training and balanced model behavior.
