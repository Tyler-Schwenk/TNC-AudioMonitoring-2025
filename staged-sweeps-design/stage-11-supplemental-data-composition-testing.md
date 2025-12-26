# Stage 11 - Supplemental Data Composition Testing

## **Experimental Design**

**Sweep Parameters**

* **Seeds:** 123, 456, 789
* **Balance:** True (fixed)
* **Positive Subsets:**
  * None (baseline - no additional positives)
  * bestLowQuality\small (smallest curated set)
  * bestLowQuality\medium (medium-sized curated set)
  * bestLowQuality\top50 (top 50 quality samples)
  * bestLowQuality\large (largest curated set)
* **Negative Subsets:**
  * hardneg\_conf\_min\_99 (highest confidence false positives)
  * hardnet\_conf\_min\_85 (high+ confidence false positives)

**Base Config**

* **Validation:** False
* **Quality:** \[High, Medium]
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
stage: 11
out_dir: config/sweeps/stage11_sweep
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
  - []
  - - AudioData\curated\bestLowQuality\small
  - - AudioData\curated\bestLowQuality\medium
  - - AudioData\curated\bestLowQuality\top50
  - - AudioData\curated\bestLowQuality\large
  negative_subsets:
  - - AudioData\curated\hardNeg\hardneg_conf_min_99
  - - AudioData\curated\hardNeg\hardnet_conf_min_85
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

{% file src="../.gitbook/assets/Stage_11_leaderboard_table.csv" %}
