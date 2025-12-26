# Stage 22 - High Precision Sensitivity Evaluation

Here I took my highest performing model by Precision (stage17\_046) and ran evaluation at 5 different sensitivity values; 0.5, 0.75, 1.0, 1.25, 1.5.

```yaml
dataset:
  audio_root: AudioData
  manifest: data/manifest.csv
experiment:
  name: stage17_046
  seed: 456
training_package:
  include_negatives: true
  balance: false
  quality:
  - high
  - medium
training:
  epochs: 50
  batch_size: 32
  threads: 4
  val_split: 0.2
  autotune: false
  use_validation: false
inference:
  batch_size: 32
  threads: 4
  min_conf: 0.0
evaluation:
  thresholds:
  - 0.5
  output_dir: evaluation
training_args:
  fmin: 0
  fmax: 15000
  overlap: 0.0
  dropout: 0.25
  hidden_units: 512
  learning_rate: 0.0005
  focal-loss: false
  focal-loss-gamma: 2.0
  focal-loss-alpha: 0.25
  label_smoothing: false
  mixup: false
  upsampling_mode: mean
  upsampling_ratio: 0.0
analyzer_args:
  fmin: 0
  fmax: 15000
  overlap: 0.0
  sensitivity: 1.0

```

{% file src="../.gitbook/assets/Stage_22_iid_leaderboard_table.csv" %}

{% file src="../.gitbook/assets/Stage_22_ood_leaderboard_table.csv" %}

{% file src="../.gitbook/assets/Precision_Model_2025.zip" %}
