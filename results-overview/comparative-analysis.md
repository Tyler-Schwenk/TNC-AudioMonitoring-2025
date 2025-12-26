---
description: >-
  This page compares the performance of the 2024 model to my best model from
  2025 (F1 selected)
---

# Comparative Analysis

### Stability & Generalization

Below are metrics of average F1 calculated at 5 sensitivity values \[0.5, 1.5]

The 2025 model shows a much smaller standard deviation across sensitivity values, and improved performance in the OOD test set.

**2024** model:

* IID Mean F1 ± Std - 91.9 ± 5.8
* OOD Mean F1 ± Std - 75.4 ± 6.5

**2025** model:

* IID Mean F1 ± Std - 97.1 ± 0.14
* OOD Mean F1 ± Std - 88.5 ± 0.15

#### 2024 Model OOD Performance

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

#### 2025 Model OOD Performance

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

***

### Performance Curves

The 2025 model showed a 7.9% improvement in AUC under the ROC curve, and a 12.7% improvement under the Precision-Recall curve; indicating an improved discriminatory ability and improved precision at a high recall.

{% columns %}
{% column %}
#### 2024 @ Ideal Sensitivity (1.5)

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
#### 2025 @ Ideal Sensitivity (0.75)

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

***

### Threshold effect

The new model demonstrates improved stability across thresholds for a given sensitivity setting.

{% columns %}
{% column %}
### Sensitivity 0.5

2025 model

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

***

2024 model

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
### Sensitivity 1.5

2025 model

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

***

2024 model

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
