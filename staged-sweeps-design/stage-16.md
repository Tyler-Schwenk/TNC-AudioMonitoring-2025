# Stage 16 - Decision Boundary Regularization

#### **Experimental Design**

**Sweep Parameters**

* **Seeds:** 3 (123, 456, 789) for reproducibility
* **Balance:** True vs False
* **Label Smoothing:** True vs False
* **Mixup:** True vs False
* **Use Validation:** False vs True

**Base Config**

* **Quality:** \[High, Medium, Low]&#x20;
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Frequency Range:** 0-15000 Hz
* **Upsampling:** None (ratio 0.0)

**Total Configurations: 3 seeds × 1 quality × 2 balance × 2 label\_smoothing × 2 mixup × 2 use\_validation = 48 experiments**

```yaml
stage: 16
out_dir: config/sweeps/stage16_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  quality:
  - - high
    - medium
    - low
  balance:
  - true
  - false
  label_smoothing:
  - true
  - false
  mixup:
  - true
  - false
  use_validation:
  - false
  - true
base_params:
  epochs: 50
  upsampling_ratio: 0.0
  mixup: false
  label_smoothing: false
  focal-loss: false
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

{% file src="../.gitbook/assets/Stage_16_leaderboard_table.csv" %}
