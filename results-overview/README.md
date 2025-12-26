# Improvement Overview

## Key improvements

The improvements of this year's model can be summarized by a few key changes;

* An increase in stability across Sensitivity values and threshold settings.
* More balanced precision-recall tradeoff, favoring stronger precision.
* More generalized model, stronger performance under domain shift.



#### 2024 Model OOD performance

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

#### 2025 Model OOD

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>





{% columns %}
{% column %}
#### 2024 @ Ideal Settings

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
#### 2025 @ Ideal Settings

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}









give auc. give other metrics. relat eback to reality of using in field. show improvemnt form previous models

talk about how we know we have reached the maximum extraction of information from our given dataset, it will likely only be improved with more data



### Sensitivity effect

how it performs at different sensitivities



best threshold at different sensitivities

maybe show this via a graph. maybe these are not a single answer but more of a range



### two versions - one low data (for brad audio moths), one full:

**Nyquist theorem** - you need to sample at **2× the highest frequency** you want to capture.

* **4 kHz sample rate** → captures up to **2 kHz** (4 / 2)
* **8 kHz sample rate** → captures up to **4 kHz** (8 / 2) ✓
* **10 kHz sample rate** → captures up to **5 kHz** (10 / 2) - slight buffer for safety

If you recorded at 4 kHz sample rate, you'd only capture 0-2 kHz, which is the over-filtered scenario that gave you 75.9% F1 with terrible precision (62.1%).

You need the **8 kHz minimum** to capture the full 0-4 kHz band that gives you optimal 88.1% F1 performance.

In practice, recorders often use 8 kHz, 11.025 kHz, or 16 kHz as standard sample rates. Going with **8 kHz** perfectly matches your fmax=4000 Hz setting.

## Temporal granularity

Model metrics have been computed based on file-level granularity. For scientist use in the filed, we are more concerned with day-level presence/absence monitoring. To determing the model's effectiveness at the day-level, we will review data from the 2024-2025 season to determine metrics for the ground-truth amound of true positive recordings collected.

it sould also be noted that the groud truth taken here, is still potentially different from the real ground truth of the amount of callig frogs, as we are working under the assumption that all calling frogs are picked up with our audiomoths.

also do this analysis on the original model

{% file src="../.gitbook/assets/positive_counts_by_recorder_date.txt" %}
