# Mixup

### Weak, Inconsistent Effect (+1.3% F1 average)

**Overall Impact** (4 controlled comparisons across 48 experiments):

* All experiments using \[high, medium, low] data
* Swept across Validation (True/False), and Balance (True/False)
* All other hyerparameters held consistent

#### Mixup Effect by Configuration

| Configuration       | Avg Delta F1 | Avg Precision | Avg Recall |
| ------------------- | ------------ | ------------- | ---------- |
| Custom Validation   | +0.5%        | -1.9%         | +2.1%      |
| Default Validation  | +2.1%        | +7.6%         | -5.3%      |
| Balanced Training   | +2.6%        | +4.7%         | -1.7%      |
| Unbalanced Training | -0.1%        | +1.1%         | -1.5%      |

#### Key Takeaways

Mixup provides small, inconsistent improvements across 16 controlled comparisons. The overall average effect is small, at +1.3% F1. Mixup works as a data augmentation technique, trading a small amount of recall (-1.6% on average) for precision gains (+2.9% on average), but the net F1 improvement is minimal. The effect varies widely across configurations, making it less reliable than label smoothing as a general-purpose regularization technique.

{% file src="../../.gitbook/assets/stage_16_leaderboard_table.csv" %}
