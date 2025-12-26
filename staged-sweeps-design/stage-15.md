# Stage 15 - Additional Sensitivity testing

#### **Experimental Design**

**Sweep Parameters**

* **Seeds:** 7 (333, 444, 555, 666, 777, 888, 999) for robust statistical analysis
* **Sensitivity:** 5 levels (0.5, 0.75, 1.0, 1.25, 1.5) - conservative to aggressive detection
* **Positive Subsets:**
  * bestLowQuality\small (fixed - minimal curated additions)
* **Negative Subsets:**
  * hardneg\_conf\_min\_50 (medium+ confidence false positives - fixed)

**Base Config**

* **Validation:** True
* **Balance:** True
* **Hidden Units:** 512
* **Quality:** \[High, Medium]&#x20;
* **Mixup:** True
* **Label Smoothing:** True
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.001 (2× higher than Stages 10-12)
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Frequency Range:** 0-15000 Hz
* **Upsampling:** None (ratio 0.0)

**Total Configurations: 7 seeds × 1 hidden\_units × 1 quality × 5 sensitivity × 1 balance × 1 positive × 1 negative = 35 experiments**

```yaml
stage: 15
out_dir: config/sweeps/stage15_sweep
axes:
  seed:
  - 333
  - 444
  - 555
  - 666
  - 777
  - 888
  - 999
  hidden_units:
  - 512
  quality:
  - - high
    - medium
  sensitivity:
  - 0.5 
  - 0.75
  - 1.0
  - 1.25
  - 1.5
  balance:
  - true
  positive_subsets:
  - - AudioData/curated/bestLowQuality/small
  negative_subsets:
  - - AudioData/curated/hardNeg/hardneg_conf_min_50
base_params:
  epochs: 50
  upsampling_ratio: 0.0
  mixup: true
  label_smoothing: true
  focal-loss: false
  focal-loss-gamma: 2.0
  focal-loss-alpha: 0.25
  dropout: 0.25
  learning_rate: 0.001
  batch_size: 32
  fmin: 0
  fmax: 15000
  overlap: 0.0
  use_validation: true

```

{% file src="../.gitbook/assets/Stage_15_leaderboard_table.csv" %}
