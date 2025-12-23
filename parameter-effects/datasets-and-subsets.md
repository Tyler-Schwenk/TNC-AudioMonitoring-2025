# Positive Datasets & Subsets

Results\
The graphs below describe a few telling metrics for our positive data subsets. Graphs are ordered from all positive data included on the left, decreasing the amount of data by dropping the lowest quality data first, until reaching only high quality data on the right. More information about datasets can be found in my [Audio Data Split Design](../audio-data-split-design.md).

All data experiments shown in these graphs used balancing (), and no use of the custom validation set.

<figure><img src="../.gitbook/assets/bar_ood_f1_vs_quality_subsets.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bar_ood_recall_vs_quality_subsets.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/bar_ood_precision_vs_quality_subsets.png" alt="" width="563"><figcaption></figcaption></figure>

The data used in these graphs can be found below:

{% file src="../.gitbook/assets/DataSet_leaderboard_table.csv" %}

All data in this section was synthesized from [stage 6](../staged-sweeps-design/stage-6-data-composition.md) and [stage 9](../staged-sweeps-design/stage-9.md).

