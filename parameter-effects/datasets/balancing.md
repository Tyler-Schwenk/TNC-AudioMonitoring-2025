# Balancing

#### Key Finding #1: Balancing Dramatically Helps Mixed-Quality Data (+13.8 F1)

When using all quality levels (high/medium/low) with custom validation and hard negatives:

* **Balanced**: F1 = 0.819 (Precision 73.2%, Recall 93.8%)
* **Unbalanced**: F1 = 0.680 (Precision 51.6%, Recall 100%)
* **Effect**: Balancing prevents recall overfitting, gaining +21.6 precision points

#### **Balancing Moderately Helps High+Medium Quality (+3.6 to +9.1 F1)**

With high and medium quality data (10 controlled comparisons):

* **Balanced**: F1 = 0.759 (Precision 90.1%, Recall 66.2%)
* **Unbalanced**: F1 = 0.723 (Precision 93.1%, Recall 61.0%)
* **Effect**: Balancing slightly helps overall performance

#### Balancing Hurts High-Quality-Only Data (-10.2 F1)

When using only high-quality data with BirdNET's default validation:

* **Balanced**: F1 = 0.646 (Precision 63.0%, Recall 83.5%)
* **Unbalanced**: F1 = 0.748 (Precision 85.4%, Recall 68.4%)
* **Effect**: Balancing reduces precision dramatically, worse overall F1

***

#### Overall <a href="#id-4-precision-recall-trade-off-pattern" id="id-4-precision-recall-trade-off-pattern"></a>

#### Precision-Recall Trade-off Pattern <a href="#id-4-precision-recall-trade-off-pattern" id="id-4-precision-recall-trade-off-pattern"></a>

**Balancing Consistently:**

* **Increases Precision:** +2.2 to +26.8 points across comparisons
* **Decreases Recall:** -0.6 to -19.9 points across comparisons
* **Net F1 Effect:** Highly variable depending on context

**When F1 Improves with Balancing:**

* Precision gains outweigh recall losses
* Typically occurs with mixed-quality data and hard negatives

{% hint style="info" %}
Full data used below, containing data from stage 6, stage&#x20;
{% endhint %}

{% file src="../../.gitbook/assets/balancing_comparison_data.csv" %}
