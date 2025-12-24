# Stage 13 - Hyperparameter fine-tuning

### Experimental Design <a href="#experimental-design" id="experimental-design"></a>

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Learning Rate**: 0.0001, 0.0005, 0.001
* **Dropout**: 0.0, 0.25 0.5, 0.75, 0.9
* **Hidden units**: 0, 128, 512, 1024

#### Base Config <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Quality**: \[High, Medium]
* **Positive Subset**: Small
* **Negative Subset**: hardneg\_conf\_min\_50
* **Validation**: True
* **Balance**: True
* **Mixup**: True
* **Label Smoothing**: True
* **Focal Loss:** False

#### Full Sweep Spec

```yaml
stage: 13
out_dir: config/sweeps/stage13_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  hidden_units:
  - 0
  - 128
  - 512
  - 1024
  dropout:
  - 0.0
  - 0.25
  - 0.5
  - 0.75
  - 0.9
  learning_rate:
  - 0.0001
  - 0.0005
  - 0.001
  quality:
  - - high
    - medium
  balance:
  - true
  positive_subsets:
  - - AudioData\curated\bestLowQuality\small
  negative_subsets:
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

### Results:

{% file src="../.gitbook/assets/stage_13_leaderboard_table (1).csv" %}
