# Stage 18 - Frequency Max Reduction

## **Experimental Design**

**Sweep Parameters**

* **Seeds:** 10 (123, 111, 222, 333, 444, 555, 666, 777, 888, 999) for high statistical certainty
* **Fmax:** 2 levels
  * 15000 Hz (full spectrum)
  * 4000 Hz (low-frequency focus for target species)
* **Sensitivity:** 5 levels (0.5, 0.75, 1.0, 1.25, 1.5) - conservative to aggressive detection

**Base Config**

* **Validation:** True
* **Balance:** False
* **Quality:** \[High, Medium, Low]&#x20;
* **Mixup:** True
* **Label Smoothing:** True
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 128 (compact model)
* **Epochs:** 50
* **Frequency Range:** 0 Hz to \[fmax] (variable)
* **Upsampling:** None (ratio 0.0)

**Total Configurations: 10 seeds × 1 hidden\_units × 1 quality × 1 balance × 2 fmax × 5 sensitivity = 100 experiments**

```yaml
stage: 18
out_dir: config/sweeps/stage18_sweep
axes:
  seed:
  - 123
  - 111
  - 222
  - 333
  - 444
  - 555
  - 666
  - 777
  - 888
  - 999
  hidden_units:
  - 128
  quality:
  - - high
    - medium
    - low
  balance:
  - false
  fmax: 
  - 15000
  - 4000
  sensitivity:
  - 0.5 
  - 0.75
  - 1.0
  - 1.25
  - 1.5
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
  overlap: 0.0
  use_validation: true

```

{% file src="../.gitbook/assets/Stage_18_leaderboard_table.csv" %}
