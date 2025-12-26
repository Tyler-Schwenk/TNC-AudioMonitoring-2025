# Stage 17 - Data Balance Regularization

**Sweep Parameters**

* **Seeds:** 3 (123, 456, 789) for reproducibility
* **Quality:** \[High, Medium] vs \[High, Medium, Low]
* **Upsampling Mode:** 3 methods (linear, mean, SMOTE)
* **Focal Loss:** True vs False
* **Upsampling Ratio:** 3 levels (0.0 = none, 0.5 = partial, 1.0 = full balance)

**Base Config**

* **Validation:** False
* **Balance:** False
* **Mixup:** False
* **Label Smoothing:** False
* **Focal Loss:** True (overridden by axes)
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Frequency Range:** 0-15000 Hz
* **Overlap:** 0.0

**Total Configurations: 3 seeds × 2 quality × 1 balance × 3 upsampling\_mode × 2 focal-loss × 3 upsampling\_ratio = 108 experiments**

```yaml
stage: 17
out_dir: config/sweeps/stage17_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  quality:
  - - high
    - medium
  - - high
    - medium
    - low
  balance:
  - false
  upsampling_mode:
  - linear
  - mean
  - smote
  focal-loss:
  - true
  - false
  upsampling_ratio:
  - 0.0
  - 0.5
  - 1.0
base_params:
  epochs: 50
  upsampling_ratio: 0.0
  mixup: false
  label_smoothing: false
  focal-loss: true
  focal-loss-gamma: 2.0
  focal-loss-alpha: 0.25
  dropout: 0.25
  learning_rate: 0.0005
  batch_size: 32
  fmin: 0
  fmax: 15000
  overlap: 0.0
  use_validation: false


```

{% file src="../.gitbook/assets/Stage_17_leaderboard_table.csv" %}
