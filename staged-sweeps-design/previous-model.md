---
description: >-
  The model from the end of our First contract, used for evaluation during the
  2024/2025 season. This will serve as the baseline for our development
---

# Previous model

NEW DATA<br>

| Experiments                                        | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) | IID F1 (mean ± std) | IID Precision (mean ± std) | IID Recall (mean ± std) |
| -------------------------------------------------- | ------------------- | -------------------------- | ----------------------- | ------------------- | -------------------------- | ----------------------- |
| 000\_OldModel2024\_baseline\_mc25\_sens50\_seed01  | 0.691 ± 0.000       | 0.528 ± 0.000              | 1.000 ± 0.000           | 0.866 ± 0.000       | 0.764 ± 0.000              | 1.000 ± 0.000           |
| 000\_OldModel2024\_baseline\_mc25\_sens100\_seed01 | 0.675 ± 0.000       | 0.509 ± 0.000              | 1.000 ± 0.000           | 0.847 ± 0.000       | 0.734 ± 0.000              | 1.000 ± 0.000           |

***





below is the model traine don our new larger set of data curated for the 2025 model development season. This larger test set of data gave us improved insight into the performance of the previous model. key take aways include its poor generalization to new sets of data, and its reliance on recall as the cost of precision.

model file: [https://huggingface.co/TylerSchwenk/Rana-Draytonii-Detection/tree/main](https://huggingface.co/TylerSchwenk/Rana-Draytonii-Detection/tree/main)

Key setup

* Data: These metrics are from recomputing on our new larger set of data. this will give more accurate metrics, as well as allow one-to-one comparison with our new models as we train them
* Pull & describe more about the parameters used
* Inference knobs compared: sensitivity 1.0 vs 0.5, min\_conf=0.25, same analyzer args (fmin/fmax/overlap).

| Sensitivity | Split   | F1        | Precision | Recall    | Threshold |
| ----------- | ------- | --------- | --------- | --------- | --------- |
| **0.5**     | **IID** | **0.966** | **0.939** | **0.994** | **0.95**  |
| **0.5**     | **OOD** | **0.800** | **0.694** | **0.945** | **1.00**  |
| **1.0**     | **IID** | **0.963** | **0.936** | **0.993** | **0.95**  |
| **1.0**     | **OOD** | **0.775** | **0.638** | **0.987** | **1.00**  |

### Evaluation

This baseline model demonstrates strong in-distribution performance but limited generalization to out-of-distribution (OOD) conditions.

* **In-Distribution (IID):**\
  The model performs well, achieving an F1 of 0.96 at high precision (0.93) and moderate recall (1.00). Predictions are highly confident, and accuracy remains stable across thresholds, indicating good calibration within familiar data domains.
* **Out-of-Distribution (OOD):**\
  Performance declines notably when applied to new sites or novel acoustic conditions. F1 drops to 0.75–0.80, driven primarily by a sharp loss in precision (down to 0.60–0.69) even at the most conservative thresholds. Recall remains high (≈0.94–1.00), suggesting the model still detects most true positives but with a significant increase in false alarms.
* **Overall:**\
  The baseline model is precision-biased and well-calibrated in-domain, but it over-predicts positives under domain shift, consistent with distributional mismatch and limited noise robustness. It serves as a solid starting point for refinement and OOD adaptation.

