# Stage 19 - Minimal Frequency Max

#### **Experimental Design**

**Sweep Parameters**

* **Seeds:** 3 (123, 456, 789) for reproducibility
* **Frequency Range:** 0-2000 Hz (low frequency focus)

**Base Config**

* **Validation:** True
* **Hidden Units:** 512
* **Quality:** \[High, Medium, Low]
* **Balance:** False&#x20;
* **Mixup:** False
* **Label Smoothing:** False
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Upsampling:** None (ratio 0.0)

**Total Configurations: 3 seeds × 1 hidden\_units × 1 quality × 1 balance = 3 experiments**

```yaml
stage: 19
out_dir: config/sweeps/stage19_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  hidden_units:
  - 512
  quality:
  - - high
    - medium
    - low
  balance:
  - false
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
  fmax: 2000
  overlap: 0.0
  use_validation: true

```

{% file src="../.gitbook/assets/Stage_19_leaderboard_table.csv" %}
