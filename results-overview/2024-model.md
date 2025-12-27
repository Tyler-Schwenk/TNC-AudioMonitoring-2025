---
description: >-
  The model from the end of our first contract, used for evaluation during the
  2024/2025 season. The model serves as the baseline for our development
---

# 2024 Model

Below is the model tested on our new larger set of data curated for the 2025 model development season. This larger test set of data gave us improved insight into the performance of the previous model and allow a one-to-one comparison with our new models.

Key limitations include its poor generalization to new sets of data, and its reliance on recall as the cost of precision.

model file: [https://huggingface.co/TylerSchwenk/Rana-Draytonii-Detection/tree/main](https://huggingface.co/TylerSchwenk/Rana-Draytonii-Detection/tree/main)

***

### IID Performance by Sensitivity (2024 Baseline)

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

| Sensitivity | IID F1 | IID Precision  | IID Recall |
| ----------- | ------ | -------------- | ---------- |
| 0.50        | 0.866  | 0.764          | 1.000      |
| 0.75        | 0.964  | 0.939          | 0.991      |
| 1.00        | 0.847  | 0.734          | 1.000      |
| 1.25        | 0.960  | 0.924          | 0.998      |
| 1.50        | 0.960  | 0.924          | 0.998      |

{% file src="../.gitbook/assets/Stage_0_IID_leaderboard_table.csv" %}

***

### OOD Performance by Sensitivity (2024 Baseline)

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

| Sensitivity | OOD F1  | OOD Precision  | OOD Recall  |
| ----------- | ------- | -------------- | ----------- |
| 0.50        | 0.691   | 0.528          | 1.000       |
| 0.75        | 0.800   | 0.694          | 0.944       |
| 1.00        | 0.675   | 0.509          | 1.000       |
| 1.25        | 0.803   | 0.760          | 0.851       |
| 1.50        | 0.803   | 0.760          | 0.851       |

{% file src="../.gitbook/assets/Stage_0_OOD_leaderboard_table.csv" %}

***
