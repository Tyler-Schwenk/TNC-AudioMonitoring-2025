# Label Smoothing

### **Label Smoothing: Modest Positive Effect (+2.1 F1 average)**

**Overall Impact** (4 controlled comparisons across 48 experiments):

* All experiments using \[high, medium, low] data
* Swept across Validation (True/False), and Balance (True/False)
* **Average Effect:** +2.1 F1 points

### Label Smoothing Effect by Configuration

| Configuration       | Avg Delta F1 | Precision | Recall |
| ------------------- | ------------ | --------- | ------ |
| Validation True     | +2.5%        | +7.5%     | -5.3%  |
| Validation False    | +1.7%        | +6.9%     | -1.6%  |
| Balanced Training   | +3.6%        | +6.9%     | -1.6%  |
| Unbalanced Training | +0.6%        | +3.5%     | -1.1%  |

Label smoothing provides modest but consistent improvements across 4 controlled comparisons. The overall average effect is +0.021 F1 points (+2.1%). Label smoothing works by reducing model overconfidence, trading a small amount of recall (-2.6 points on average) for larger precision gains (+4.6 points), resulting in a net positive F1 improvement.&#x20;

{% hint style="info" %}
These comparisons used data from [stage 16](../../staged-sweeps-design/stage-16.md)
{% endhint %}

{% file src="../../.gitbook/assets/label_smoothing_comparison_data.csv" %}
