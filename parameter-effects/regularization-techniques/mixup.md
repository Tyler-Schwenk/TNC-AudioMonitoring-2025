# Mixup

### Weak, Inconsistent Effect (+1.3 F1 average)

**Experiment Setup (Mixup Analysis):**

* **Data Source:** 48 high-performing experiments from Stage 16 leaderboard
* **Quality Levels:** All experiments use \[High, Medium, Low] quality data
* **Parameters Swept:**
  * Class Balancing: True (balanced negatives) vs False (unbalanced)
  * Label Smoothing: True vs False
  * Validation Package: False only (BirdNET default 20%)
* **Controlled Comparisons:** 16 comparisons where only mixup varies (True/False)
* **Overall Effect:** +0.013 F1 points (+1.3%) average across all comparisons

#### Mixup Effect by Configuration

| Configuration       | Avg Delta F1 | Precision | Recall |
| ------------------- | ------------ | --------- | ------ |
| Balanced Training   | +2.6%        | +12.9%    | -0.8%  |
| Unbalanced Training | -0.1%        | +13.2%    | -4.7%  |
| Default Validation  | +1.3%        | +12.9%    | -0.8%  |

#### Key Takeaways

Mixup provides small, inconsistent improvements across 16 controlled comparisons. The overall average effect is +0.013 F1 points (+1.3%), helping in only 56% of cases (9/16). Mixup works as a data augmentation technique, trading a small amount of recall (-1.6 points on average) for precision gains (+2.9 points), but the net F1 improvement is minimal. The effect varies widely across configurations, making it less reliable than label smoothing as a general-purpose regularization technique.

{% file src="../../.gitbook/assets/stage_16_leaderboard_table.csv" %}
