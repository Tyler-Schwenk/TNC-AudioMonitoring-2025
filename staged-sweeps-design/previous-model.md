---
description: >-
  The model from the end of our First contract, used for evaluation during the
  2024/2025 season. This will serve as the baseline for our development
---

# Previous model

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













OLD BAD METRICS

Key setup

* Data: These metrics are from recomputing on our new larger set of data. this will give more accurate metrics, as well as allow one-to-one comparison with our new models as we train them
* Pull & describe more about the parameters used
* Inference knobs compared: sensitivity 1.0 vs 0.5, min\_conf=0.25, same analyzer args (fmin/fmax/overlap).

| Sensitivity | Split   | F1        | Precision | Recall | Threshold |
| ----------- | ------- | --------- | --------- | ------ | --------- |
| 0.5         | IID     | 0.622     | 0.766     | 0.524  | 0.95      |
| 0.5         | **OOD** | **0.700** | 0.554     | 0.952  | 1.00      |
| 1.0         | IID     | 0.808     | 0.957     | 0.699  | 0.95      |
| 1.0         | **OOD** | **0.773** | 0.697     | 0.868  | 1.00      |

Evaluation

This baseline model demonstrates **strong in-distribution performance** but **limited generalization** to out-of-distribution (OOD) conditions.

* **In-Distribution (IID):**\
  The model performs well, achieving an F1 of **0.81** at high precision (**0.96**) and moderate recall (**0.70**). Predictions are highly confident, and accuracy remains stable across thresholds, indicating good calibration within familiar data domains.
* **Out-of-Distribution (OOD):**\
  Performance declines notably when applied to new sites or novel acoustic conditions. F1 drops to **0.70–0.77**, driven primarily by a **sharp loss in precision** (down to **0.55–0.70**) even at the most conservative thresholds. Recall remains high (≈0.87–0.95), suggesting the model still detects most true positives but with a significant increase in false alarms.
* **Overall:**\
  The baseline model is **precision-biased and well-calibrated in-domain**, but it **over-predicts positives under domain shift**, consistent with distributional mismatch and limited noise robustness. It serves as a solid starting point for refinement and OOD adaptation.
