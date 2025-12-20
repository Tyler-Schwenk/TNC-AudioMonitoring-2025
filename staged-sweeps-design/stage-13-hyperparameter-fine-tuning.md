# Stage 13 - Hyperparameter fine-tuning

taking the best config from all of the runs - stage 9\_006, and running with it. sweeping across all hyperparameters

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

Dropout:

<figure><img src="../.gitbook/assets/chart_Dropout_OOD_F1.png" alt="" width="360"><figcaption></figcaption></figure>

Learning Rate:

<figure><img src="../.gitbook/assets/chart_Learning_Rate_OOD_F1 (1).png" alt="" width="360"><figcaption></figcaption></figure>



Hidden units:<br>

<figure><img src="../.gitbook/assets/chart_Hidden_Units_OOD_F1 (1).png" alt="" width="360"><figcaption></figcaption></figure>



full results:

{% file src="../.gitbook/assets/stage_13_leaderboard_table (1).csv" %}

**We will carry forward:**\
**learning rate: 0.001**

**dropout: 0.25**\
**hidden units: 1024**
