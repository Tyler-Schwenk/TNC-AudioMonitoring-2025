# \[Archive] Stage 1 - Capacity & Regularization

#### Overview <a href="#overview" id="overview"></a>

The Stage 1 sweep (capacity + regularization) was designed in a breadth-first style to identify which hyperparameter regions are promising for our custom BirdNET classifier. The results show some useful patterns, but also highlight high variability across runs.

**What Stage 1 Told Us**

* **Dropout**: 0.25 consistently improved out-of-distribution (OOD) generalization compared to 0.0 or 0.5.
* **Hidden Units**: Larger heads (1024 HU) gave the best _average_ performance, but smaller heads (128–512 HU) sometimes produced the single best OOD runs.
* **Learning Rate**: 1e-3 produced strong averages, but the _best individual OOD run_ came at 5e-4.
* **Batch Size**: 32 slightly outperformed 16, but was not a major factor.

In Retrospect: Stage 1 successfully established baseline hyperparameter regions but, as only a single seed was used per configuration, the results should be interpreted qualitatively. Subsequent multi-seed sweeps (Stages 2–4) confirmed that a variance floor of roughly ± 0.05 F1 exists, meaning Stage 1 differences smaller than this threshold likely reflected stochastic effects rather than true hyperparameter sensitivity.

***

#### Design <a href="#design" id="design"></a>

I ran a **72-config factorial sweep** to explore model capacity and regularization. **Factors varied:**

* Hidden Units: 0, 128, 512, 1024
* Dropout: 0.0, 0.25, 0.5
* Learning Rate: 1e-4, 5e-4, 1e-3
* Batch Size: 16, 32

#### Base Configuration <a href="#base-configuration" id="base-configuration"></a>

**Dataset & Training**

* Dataset: High + medium quality positives, balanced negatives
* Epochs: 50
* Validation split: 0.2
* Negatives: included and balanced
* Seed: 123

**Inference & Evaluation**

* Thresholds: full sweep (0.0 → 1.0 step 0.05), baseline at 0.5
* Metrics: F1, precision, recall (IID and OOD splits)

**Fixed BirdNET Parameters**

* Frequency range: 0–15 kHz
* Overlap: 0.0
* Sensitivity: 1.0
* No augmentation: label smoothing, mixup, focal loss = off
* No upsampling (upsampling\_ratio=0.0)

Full config file here:

### base.yaml

Code•3KB

***

#### Top Models <a href="#top-models" id="top-models"></a>

Full evaluation of all runs here:

### stage1sweep.csv

Text•45KB**Top 10 by OOD Best-F1**

|       |       |      |      |       |    |       |       |       |       |
| ----- | ----- | ---- | ---- | ----- | -- | ----- | ----- | ----- | ----- |
| 0.812 | 0.692 | 128  | 0.25 | 0     | 32 | 0.605 | 0.434 | 0.996 | 0.982 |
| 0.76  | 0.626 | 1024 | 0.25 | 0     | 16 | 0.642 | 0.474 | 0.998 | 0.969 |
| 0.744 | 0.605 | 128  | 0    | 0.001 | 16 | 0.62  | 0.454 | 0.978 | 0.968 |
| 0.732 | 0.854 | 512  | 0.25 | 0     | 32 | 0.665 | 0.684 | 0.648 | 0.641 |
| 0.729 | 0.768 | 512  | 0    | 0     | 32 | 0.702 | 0.628 | 0.797 | 0.694 |
| 0.72  | 0.562 | 128  | 0.5  | 0     | 16 | 0.653 | 0.589 | 0.733 | 1     |
| 0.702 | 0.541 | 512  | 0    | 0.001 | 32 | 0.528 | 0.359 | 1     | 1     |
| 0.687 | 0.53  | 0    | 0.25 | 0.001 | 32 | 0.523 | 0.354 | 1     | 0.977 |
| 0.683 | 0.689 | 1024 | 0    | 0     | 32 | 0.622 | 0.568 | 0.688 | 0.676 |
| 0.672 | 0.52  | 0    | 0    | 0.001 | 32 | 0.508 | 0.342 | 0.988 | 0.948 |

Hyperparameter EffectsWhat they plot:X-axis = the hyperparameter being swept (e.g. hidden units).Y-axis = F1 score.Two lines: IID F1 (blue) and OOD F1 (orange).Lines: These are averages across all runs with that hyperparameter value.Shaded regions: The shaded band around each line is the confidence interval (CI) -- 95% CI of the mean.Narrow band → metric is consistent across runs.Wide band → metric varies a lot depending on other hyperparameters.Hidden UnitsLarger heads (1024 HU) gave the best average performance, but smaller heads (128–512 HU) sometimes produced the single best OOD runs.Tradeoff: larger heads are stable, smaller heads spike.DropoutDropout = 0.25 consistently shifts performance upward.0.5 sometimes hurts recall, 0.0 overfits.Learning RateLR = 1e-3 produced strong averages, but the best individual OOD run came at 5e-4.There is no clear dominant setting hereBatch SizeBatch size of 32 was slightly better on average than 16, but no clear causation can be drawn to make this a major driver.TakeawaysThese results allow us to narrow the search space:Hidden Units: 128–1024Dropout: 0.25Learning Rate: 5e-4–1e-3Batch Size: 32What Stage 1 Did Not Resolve<br>
