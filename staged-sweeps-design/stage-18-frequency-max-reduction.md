# Stage 18 - Frequency Max Reduction





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
