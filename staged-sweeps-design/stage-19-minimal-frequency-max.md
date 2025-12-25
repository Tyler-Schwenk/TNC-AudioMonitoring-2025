# Stage 19 - Minimal Frequency Max



```yaml
stage: 19
out_dir: config/sweeps/stage19_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  hidden_units:
  - 512
  quality:
  - - high
    - medium
    - low
  balance:
  - false
base_params:
  epochs: 50
  upsampling_ratio: 0.0
  mixup: false
  label_smoothing: false
  focal-loss: false
  focal-loss-gamma: 2.0
  focal-loss-alpha: 0.25
  dropout: 0.25
  learning_rate: 0.0005
  batch_size: 32
  fmin: 0
  fmax: 2000
  overlap: 0.0
  use_validation: true

```
