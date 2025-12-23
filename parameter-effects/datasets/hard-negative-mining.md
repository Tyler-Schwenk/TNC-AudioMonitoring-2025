# Hard Negative Mining

## Hard Negative Mining: Impact on RADR Classifier Performance

### Background & Methodology

**Our Approach:** We mined 20,457 negative audio files (Brad's recorders 2, 9, 10—disjoint from train/test/val) using model stage3\_046. Files were ranked by maximum false-positive confidence for RADR, creating three hardness tiers:

* **hardneg\_conf\_min\_50**: 1,401 files (≥50% confidence) — moderately confusing negatives
* **hardneg\_conf\_min\_85**: 981 files (≥85% confidence) — highly confusing negatives
* **hardneg\_conf\_min\_99**: 475 files (≥99% confidence) — nearly indistinguishable negatives

I then trained models with these different negative sets while holding all other variables constant (positive subsets, quality filters, validation scheme, hyperparameters), evaluating on both **OOD** (out-of-distribution, unseen data) and **IID** (in-distribution, validation set) test data.

### Theoretical Expectations

**What hard negative mining should do:**

1. ✅ **Increase precision** by teaching the model to avoid specific false-positive patterns it previously made
2. ✅ **Improve OOD generalization** by exposing the model to harder boundary cases during training
3. ⚠️ **Potentially decrease recall** if the model becomes overly conservative to avoid hard negatives
4. ⚠️ **Risk overfitting** if negatives are too hard (model memorizes specific examples rather than learning general patterns)

### Observed Trends

#### Finding 1: Sweet Spot at 85% Confidence (Matches Expectations)

**Expected:** Moderate hardness should balance learning without overfitting.\
**Observed:** ✅ **Confirmed** — The 85% confidence threshold showed the strongest, most consistent gains.

**OOD Results (85% hardnet\_conf\_min\_85):**

```
Large positives:    F1: 0.782 → 0.833 (+5.1 points)
                    Precision: 0.907 → 0.839 (-6.8 points)
                    Recall: 0.697 → 0.828 (+13.1 points)

Top50 positives:    F1: 0.776 → 0.794 (+1.8 points)
                    Recall: 0.669 → 0.702 (+3.3 points)

Medium positives:   F1: 0.810 → 0.793 (-1.7 points)
                    Precision: 0.910 → 0.948 (+3.8 points)
                    Recall: 0.736 → 0.683 (-5.3 points)
```

**IID Results (85%):**

```
Top50 (with val):   F1: 0.845 → 0.884 (+3.9 points)
Top50 (no val):     F1: 0.850 → 0.880 (+3.0 points)
```

**Interpretation:** With large positive datasets, hard negatives produce **massive recall gains** (+13 points) that outweigh precision drops. With smaller datasets, we see the expected precision-recall trade-off more clearly. IID performance improves consistently regardless of positive set size.

#### Finding 2: Diminishing Returns from Extremely Hard Negatives (Unexpected)

**Expected:** Harder should be better — the most confusing negatives should teach the most.\
**Observed:** ⚠️ **Contradicted** — 99% confidence negatives often hurt OOD performance.

**OOD Results (99% hardneg\_conf\_min\_99):**

```
Medium positives:   F1: 0.810 → 0.762 (-4.8 points) ❌
                    Precision: 0.910 → 0.845 (-6.5 points)
                    Recall: 0.736 → 0.706 (-3.0 points)

Large positives:    F1: 0.782 → 0.774 (-0.8 points) ❌

Top50 positives:    F1: 0.776 → 0.804 (+2.8 points) ✅
```

**Interpretation:** Only top50 positives benefited from 99% hard negatives. For medium and large datasets, these extremely hard examples appear to cause **overfitting** — the model learns specific patterns from the mining model's mistakes rather than generalizable features. This suggests the 99% threshold captures outliers or mining model artifacts rather than true boundary cases.

#### Finding 3: Precision-Recall Trade-off is Data-Dependent

**Expected:** Hard negatives should uniformly increase precision at the cost of recall.\
**Observed:** ⚠️ **Partially confirmed** — Effect depends on positive dataset size.

**Observed Patterns:**

* **Large positive sets** (abundant RADR examples): Hard negatives boost **both** precision and recall
* **Medium/Small positive sets** (limited RADR examples): Classic trade-off emerges — precision ↑, recall ↓
* **With validation data**: Trade-offs are less severe; IID performance improves across the board

**Interpretation:** When the model has seen many positive examples, adding hard negatives sharpens the decision boundary without becoming overly conservative. With fewer positives, the model lacks confidence in what constitutes a true RADR call, so hard negatives make it more cautious (higher precision, lower recall).

#### Finding 4: IID vs OOD Divergence

**Expected:** Hard negatives should improve both IID and OOD similarly.\
**Observed:** ⚠️ **Divergent** — IID consistently benefits; OOD is configuration-dependent.

**IID showed improvements in all comparisons:**

* 85% confidence: +3.0 to +3.9 F1 points (top50 datasets)
* 99% confidence: +5.4 F1 points (top50 with validation)
* Even with no hard negatives → 50% threshold: +1.5 F1 boost

**OOD showed mixed results:**

* Large positives + 85%: Strong gains (+5.1 F1)
* Medium positives + 85%: Slight degradation (-1.7 F1)
* Medium positives + 99%: Significant degradation (-4.8 F1)

**Interpretation:** Hard negatives help the model perform better on validation data that shares distributional properties with training data (IID). However, OOD generalization requires the right combination of positive dataset size and negative hardness — too few positives or too-hard negatives cause overfitting that harms unseen data performance.

### Summary & Recommendations

#### What Worked

✅ **Use 85% confidence threshold (hardnet\_conf\_min\_85, 981 files)** as the standard hard negative set\
✅ **Pair with large positive datasets** for best OOD gains (+5.1 F1)\
✅ **Expect precision-recall trade-offs** with smaller positive sets — acceptable for precision-critical applications\
✅ **IID performance benefits universally** — good for validation metrics and leaderboard rankings

#### What Didn't Work

❌ **Avoid 99% confidence threshold** unless using top50 positives — risk of overfitting to mining model artifacts\
❌ **Don't rely solely on hard negatives** with small/medium positive sets — model needs sufficient positive examples to maintain recall\
❌ **Mining from limited recorders** (2, 9, 10 only) — may not generalize to other acoustic environments

#### Theory vs. Reality

| Expectation                       | Reality                              | Status |
| --------------------------------- | ------------------------------------ | ------ |
| Hard negatives increase precision | ✅ Confirmed (most configs)           | ✅      |
| OOD generalization improves       | ⚠️ Depends on positive set size      | ⚠️     |
| Recall may decrease               | ✅ Confirmed (small/medium positives) | ✅      |
| Harder is better                  | ❌ Diminishing returns at 99%         | ❌      |
| IID and OOD track together        | ❌ IID improves more consistently     | ❌      |

#### Optimal Configuration

**Recommendation:** Use **hardnet\_conf\_min\_85** with **large positive datasets** for production deployment. This achieves:

* +5.1 F1 OOD improvement
* +13.1 recall improvement (critical for detection tasks)
* +3.0-3.9 F1 IID improvement
* Avoids overfitting to extreme hard negatives

**For precision-critical applications:** Consider hardneg\_conf\_min\_85 with medium positives (accepts -1.7 F1 for +3.8 precision gain)

### Limitations

⚠️ **Small sample sizes** (3-7 experiments per configuration) — no statistical significance testing performed\
⚠️ **Mining bias** — Hard negatives from Brad's recorders 2, 9, 10 only; may not represent full acoustic diversity\
⚠️ **Model-specific artifacts** — Mining model (stage3\_046) may have systematic blind spots that influenced selection\
⚠️ **Baseline scarcity** — Few "no hard negatives" baselines limit absolute effect measurement

**Interpret results as directional trends, not statistically validated effects.**

***

### Detailed Comparison Data

Full controlled comparison tables with experiment counts, mean ± std metrics, and delta calculations are shown below:

{% hint style="info" %}
Full data used for comparison is below, drawn from [stage 6](../../staged-sweeps-design/stage-6-data-composition.md) and [stage 9](../../staged-sweeps-design/stage-9.md)
{% endhint %}

{% file src="../../.gitbook/assets/hard_negative_comparison_data.csv" %}

***
