# Stage 13

taking the best config from all of the runs - stage 9\_006, and running with it.





config used:<br>

```yaml
dataset:
  audio_root: AudioData
  manifest: data/manifest.csv
experiment:
  name: stage9_006
  seed: 123
training_package:
  include_negatives: true
  balance: true
  quality:
  - high
  - medium
  positive_subsets:
  - AudioData\curated\bestLowQuality\small
  negative_subsets:
  - AudioData\curated\hardNeg\hardneg_conf_min_50
training:
  epochs: 50
  batch_size: 32
  threads: 4
  val_split: 0.2
  autotune: false
  use_validation: true
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
  label_smoothing: true
  mixup: true
  upsampling_mode: repeat
  upsampling_ratio: 0.0
analyzer_args:
  fmin: 0
  fmax: 15000
  overlap: 0.0
  sensitivity: 1.0

```
