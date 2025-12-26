# Stage 0 - 2024 model

Below is the old 2024 model tested on our new larger set of data curated for the 2025 model development season. This larger test set of data gave us improved insight into the performance of the previous model. Key take aways include its poor generalization to new sets of data, and its reliance on recall as the cost of precision.

model file: [https://huggingface.co/TylerSchwenk/Rana-Draytonii-Detection/tree/main](https://huggingface.co/TylerSchwenk/Rana-Draytonii-Detection/tree/main)

Key setup

* Data: These metrics are from recomputing on our new larger set of data. this will give more accurate metrics, as well as allow one-to-one comparison with our new models as we train them
* Pull & describe more about the parameters used
* Inference knobs compared: sensitivity 1.0 vs 0.5, min\_conf=0.25, same analyzer args (fmin/fmax/overlap).

***

### IID Performance by Sensitivity (2024 Baseline)

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

| Sensitivity | IID F1 (mean ± std) | IID Precision (mean ± std) | IID Recall (mean ± std) |
| ----------- | ------------------- | -------------------------- | ----------------------- |
| 0.50        | 0.866 ± 0.000       | 0.764 ± 0.000              | 1.000 ± 0.000           |
| 0.75        | 0.964 ± 0.000       | 0.939 ± 0.000              | 0.991 ± 0.000           |
| 1.00        | 0.847 ± 0.000       | 0.734 ± 0.000              | 1.000 ± 0.000           |
| 1.25        | 0.960 ± 0.000       | 0.924 ± 0.000              | 0.998 ± 0.000           |
| 1.50        | 0.960 ± 0.000       | 0.924 ± 0.000              | 0.998 ± 0.000           |

{% file src="../.gitbook/assets/Stage_0_IID_leaderboard_table.csv" %}

***

### OOD Performance by Sensitivity (2024 Baseline)

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

| Sensitivity | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) |
| ----------- | ------------------- | -------------------------- | ----------------------- |
| 0.50        | 0.691 ± 0.000       | 0.528 ± 0.000              | 1.000 ± 0.000           |
| 0.75        | 0.800 ± 0.000       | 0.694 ± 0.000              | 0.944 ± 0.000           |
| 1.00        | 0.675 ± 0.000       | 0.509 ± 0.000              | 1.000 ± 0.000           |
| 1.25        | 0.803 ± 0.000       | 0.760 ± 0.000              | 0.851 ± 0.000           |
| 1.50        | 0.803 ± 0.000       | 0.760 ± 0.000              | 0.851 ± 0.000           |

{% file src="../.gitbook/assets/Stage_0_OOD_leaderboard_table.csv" %}

