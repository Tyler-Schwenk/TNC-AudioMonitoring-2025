# Stage 12

#### Experimental Design

**Sweep Parameters**

* **Seeds:** 2 (123, 456) for lightweight testing
* **Quality:** \[High] vs \[High, Medium, Low]
* **Balance:** True vs False
* **Negative Subsets:**
  * None (no hard negatives)
  * hardneg\_conf\_min\_99 (highest confidence false positives)
  * hardneg\_conf\_min\_50 (medium+ confidence false positives)

**Base Config**

* Validation: True
* Mixup: True
* Label Smoothing: True
* Focal Loss: False
* Dropout: 0.25
* Learning Rate: 0.0005
* Hidden Units: 512 (default)
* Epochs: 50
* Frequency Range: 0-15000 Hz
* Upsampling: None (ratio 0.0)

**Total Configurations:** 2 seeds × 2 quality × 2 balance × 3 negative subsets = **24 experiments**

```yaml
stage: 12
out_dir: config/sweeps/stage12_sweep
axes:
  seed:
  - 123
  - 456
  quality:
  - - high
  - - high
    - medium
    - low
  balance:
  - true
  - false
  negative_subsets:
  - []
  - - AudioData\curated\hardNeg\hardneg_conf_min_99
  - - AudioData\curated\hardNeg\hardneg_conf_min_50
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
  use_validation: true

```

#### Results:

{% file src="../.gitbook/assets/stage_12_leaderboard_table.csv" %}
