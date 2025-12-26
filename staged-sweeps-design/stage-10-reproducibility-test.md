# Stage 10 - Reproducibility Test

## **Experimental Design**

**Sweep Parameters**

* **Seeds:** 3 (123, 456, 789) for reproducibility testing
* **Quality:** \[High, Medium] (fixed combination)
* **Balance:** True (fixed)
* **Positive Subsets:**
  * bestLowQuality\top50 (top 50 quality samples - fixed)
* **Negative Subsets:**
  * hardneg\_conf\_min\_99 (highest confidence false positives - fixed)

**Base Config**

* **Validation:** False
* **Mixup:** True
* **Label Smoothing:** True
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Frequency Range:** 0-15000 Hz
* **Upsampling:** None (ratio 0.0)

```yaml
stage: 10
out_dir: config/sweeps/stage10_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  quality:
  - - high
    - medium
  balance:
  - true
  positive_subsets:
  - - AudioData\curated\bestLowQuality\top50
  negative_subsets:
  - - AudioData\curated\hardNeg\hardneg_conf_min_99
base_params:
  epochs: 50
  upsampling_ratio: 0.0
  mixup: true
  label_smoothing: true
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

{% file src="../.gitbook/assets/Stage_10_leaderboard_table.csv" %}
