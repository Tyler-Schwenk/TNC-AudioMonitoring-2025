# Stage 13 - Hyperparameter fine-tuning

### Goal

With training data finalized, the goal of this sweep was to take a second pass at the hyperparameters to ensure the best configuration, as it may have changed from our initial setup .

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

### Results

#### Stage 13 – OOD Performance Summary (Top Configurations)

<table><thead><tr><th width="122.79998779296875">Experiments</th><th>Hidden Units</th><th>Dropout</th><th>Learning Rate</th><th>OOD F1 (mean ± std)</th><th>OOD Precision (mean ± std)</th><th>OOD Recall (mean ± std)</th></tr></thead><tbody><tr><td>stage13_021, stage13_057, stage13_093, stage13_153</td><td>512</td><td>0.0</td><td>0.001</td><td>0.950 ± 0.065</td><td>0.950 ± 0.070</td><td>0.950 ± 0.061</td></tr><tr><td>stage13_032, stage13_068, stage13_104, stage13_110, stage13_170</td><td>1024</td><td>0.25</td><td>0.0005</td><td>0.912 ± 0.081</td><td>0.938 ± 0.067</td><td>0.888 ± 0.097</td></tr><tr><td>stage13_030, stage13_066, stage13_102, stage13_168</td><td>1024</td><td>0.0</td><td>0.001</td><td>0.912 ± 0.108</td><td>0.963 ± 0.055</td><td>0.872 ± 0.154</td></tr><tr><td>stage13_029, stage13_065, stage13_101, stage13_167</td><td>1024</td><td>0.0</td><td>0.0005</td><td>0.862 ± 0.130</td><td>0.845 ± 0.193</td><td>0.914 ± 0.138</td></tr></tbody></table>

full results:

{% file src="../.gitbook/assets/stage_13_leaderboard_table (1).csv" %}
