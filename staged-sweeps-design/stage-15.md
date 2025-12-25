# Stage 15 - Additional Sensitivity testing



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
