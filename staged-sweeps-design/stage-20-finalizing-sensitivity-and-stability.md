# Stage 20 - Finalizing Sensitivity and Stability



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
