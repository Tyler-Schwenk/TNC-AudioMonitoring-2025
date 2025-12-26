# Stage 20 - Sensitivity and Stability

**Sweep Parameters**

* **Seeds:** 5 (111, 222, 333, 444, 555) for robust statistics
* **Fmax:** 2 levels
  * 15000 Hz (full spectrum)
  * 4000 Hz (low-frequency focus)
* **Sensitivity:** 5 levels (0.5, 0.75, 1.0, 1.25, 1.5)&#x20;
* **Negative Subset:**
  * hardneg\_conf\_min\_85 (high confidence false positives - fixed)

**Base Config**

* **Validation:** False
* **Quality:** \[High, Medium, Low]&#x20;
* **Balance:** False&#x20;
* **Focal Loss:** False&#x20;
* **Mixup:** False
* **Label Smoothing:** False
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Frequency Range:** 0 Hz to \[fmax] (variable)
* **Upsampling:** None (ratio 0.0)

**Total Configurations: 5 seeds × 1 quality × 1 balance × 1 focal-loss × 2 fmax × 1 upsampling × 5 sensitivity × 1 negative = 50 experiments**

```yaml
stage: 20
out_dir: config/sweeps/stage20_sweep
axes:
  seed:
  - 111
  - 222
  - 333
  - 444
  - 555
  quality:
  - - high
    - medium
    - low
  balance:
  - false
  focal-loss:
  - false
  fmax:
  - 15000
  - 4000
  upsampling_ratio:
  - 0.0
  sensitivity:
  - 0.5 
  - 0.75
  - 1.0
  - 1.25
  - 1.5
  negative_subsets:
  - - AudioData\curated\hardNeg\hardneg_conf_min_85
base_params:
  epochs: 50
  upsampling_ratio: 0.0
  mixup: false
  label_smoothing: false
  dropout: 0.25
  learning_rate: 0.0005
  batch_size: 32
  fmin: 0
  fmax: 15000
  overlap: 0.0
  use_validation: false

```

{% file src="../.gitbook/assets/Stage_20_leaderboard_table.csv" %}
