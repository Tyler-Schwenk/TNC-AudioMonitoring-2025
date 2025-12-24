# Hard Negative Mining

### Background & Methodology

We mined 20,457 negative audio files (Brad's recorders 2, 9, 10—disjoint from train/test/val) using model stage3\_046. Files were ranked by maximum false-positive confidence for RADR, creating three hardness tiers:

* **hardneg\_conf\_min\_50**: 1,401 files (≥50% confidence) — Largest set of confusing negatives
* **hardneg\_conf\_min\_85**: 981 files (≥85% confidence) — subset of most confusing negatives
* **hardneg\_conf\_min\_99**: 475 files (≥99% confidence) — hardest subsets of negatives

I then trained models with these different negative sets while holding all other variables constant (positive subsets, quality filters, validation scheme, hyperparameters), evaluating on both OOD (out-of-distribution, unseen data) and IID (in-distribution, validation set) test data. Models were trained with different positive subsets, but only compared with other models trained on the same subset.

**What hard negative mining should do:**

1. **Increase precision** by teaching the model to avoid specific false-positive patterns it previously made
2. **Improve OOD generalization** by exposing the model to harder boundary cases during training
3. **Potentially decrease recall** if the model becomes overly conservative to avoid hard negatives
4. **Risk overfitting** if negatives are too hard (model memorizes specific examples rather than learning general patterns)

***

### Key Findings

#### 1. The **85% hard negative threshold** consistently produced the best trade-off between learning and generalization.

**OOD**&#x20;

* **Large positives:**\
  F1 **+5.1**, Recall **+13.1**, Precision −6.8
* **XL positives:**\
  F1 **+1.8**, Recall **+3.3**
* **Medium positives:**\
  Mixed results (Precision generally improves, Recall generally dropped, F1 −1.7)

Interpretation: With sufficient positive data, 85% hard negatives significantly improve recall and overall OOD performance. With smaller positive sets, the expected precision–recall trade-off appears.

***

#### **2. Extremely Hard Negatives (99%) Often Hurt OOD Performance**

Contrary to expectation, **99% confidence negatives frequently degraded OOD results**.

**OOD**

* Medium positives: **−4.8 F1**
* Large positives: **−0.8 F1**
* XL positives: **+2.8 F1** (only case with improvement)

Interpretation: At 99%, negatives appear to reflect mining-model artifacts or outliers, leading to overfitting rather than better boundary learning. Benefits were limited to the smallest positive set.

***

#### **3. Effects Depend Strongly on Positive Dataset Size**

* **Large positive sets:** Hard negatives improve both precision and recall.
* **Medium/small positive sets:** Trade-off emerges (precision increase, recall decrease).
* **With validation:** Trade-offs are dampened; IID improves consistently.

Interpretation: Adequate positive coverage is required for hard negatives to sharpen boundaries without making the model overly conservative.

***

#### **4. IID Improves Reliably; OOD Does Not**

* **IID:** Improvements in all configurations tested.
  * 85%: +3.0 to +3.9 F1
  * 99% (Top50 + val): +5.4 F1
* **OOD:** Highly configuration-dependent.
  * Strong gains only with large positives + 85%
  * Degradation with insufficient positives or overly hard negatives

Interpretation: Hard negatives reliably improve validation metrics, but OOD generalization requires careful tuning of hardness and positive data volume.

***

#### Recommendations

**Use in Production**

* **Default:** `hardneg_conf_min_85` with **large positive datasets**
  * +5.1 OOD F1
  * +13.1 OOD recall
  * +3.0–3.9 IID F1
* **Precision-critical cases:**\
  85% negatives + medium positives (accept small F1 loss for precision gain)

**Avoid**

* 99% hard negatives except with Top50 positives
* Heavy reliance on hard negatives with limited positive data
* Treating validation gains as evidence of OOD improvement

***

#### Limitations

* Small sample sizes (3–7 runs per configuration)
* No formal statistical testing
* Mining restricted to recorders 2, 9, 10
* Potential bias from mining model (stage3\_046)

**Interpret all results as directional trends, not statistically validated effects.**

***

### Detailed Comparison Data

Full controlled comparison tables with experiment counts, mean ± std metrics, and delta calculations are shown below:

{% hint style="info" %}
Full data used for comparison is below, drawn from [stage 6](../../staged-sweeps-design/stage-6-data-composition.md) and [stage 9](../../staged-sweeps-design/stage-9.md)
{% endhint %}

{% file src="../../.gitbook/assets/hard_negative_comparison_data.csv" %}

***
