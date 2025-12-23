# Balancing

#### Balancing Dramatically Helps Mixed-Quality Data (+13.8 F1)

When using all quality levels (high/medium/low) with custom validation and hard negatives:

* **Balanced**: F1 = 0.819 (Precision 73.2%, Recall 93.8%)
* **Unbalanced**: F1 = 0.680 (Precision 51.6%, Recall 100%)
* **Effect**: Balancing prevents recall overfitting, gaining +21.6 precision points

#### **Balancing Moderately Helps High+Medium Quality (+4.0 F1)**

With high and medium quality data (10 controlled comparisons):

* **Balanced**: F1 = 0.764 (Precision 87.8%, Recall 70.8%)
* **Unbalanced**: F1 = 0.722 (Precision 77.7%, Recall 73.8%)
* **Effect:** Balancing moderately helps overall performance, especially with added negative subsets

#### Balancing Hurts High-Quality-Only Data (-10.2 F1)

When using only high-quality data with BirdNET's default validation:

* **Balanced**: F1 = 0.646 (Precision 63.0%, Recall 83.5%)
* **Unbalanced**: F1 = 0.748 (Precision 85.4%, Recall 68.4%)
* **Effect**: Balancing reduces precision dramatically, worse overall F1

***

#### Overall <a href="#id-4-precision-recall-trade-off-pattern" id="id-4-precision-recall-trade-off-pattern"></a>

#### Precision-Recall Trade-off Pattern <a href="#id-4-precision-recall-trade-off-pattern" id="id-4-precision-recall-trade-off-pattern"></a>

**Balancing Consistently:**

* **Increases Precision:** 65% of comparisons (+2.2 to +26.8 points)
* **Decreases Recall:** 44% of comparisons (-0.6 to -19.9 points)
* **Net F1 Effect:** Highly variable depending on context

**When F1 Improves with Balancing:**

* Precision gains outweigh recall losses
* Typically occurs with mixed-quality data and hard negatives

{% hint style="info" %}
Full data used below, containing data from [stage 6](../../staged-sweeps-design/stage-6-data-composition.md), [stage 12](../../staged-sweeps-design/stage-12.md), [stage 16](../../staged-sweeps-design/stage-16.md),&#x20;
{% endhint %}

{% file src="../../.gitbook/assets/balancing_comparison_data (1).csv" %}
