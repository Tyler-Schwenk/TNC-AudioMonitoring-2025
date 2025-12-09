# Stage 9 - Custom Validation Set

This was where i ttempted using my custom validation set instead of the birdnet default pulling 20 from my standard set.

and swept all subsets. \
as described here:<br>

```yaml
stage: 9
out_dir: config/sweeps/stage9_sweep
axes:
  seed:
  - 123
  - 456
  - 789
  quality:
  - - high
    - medium
  balance:
  - true
  use_validation:
  - true
  - false
  positive_subsets:
  - - AudioData\curated\bestLowQuality\top50
  - - AudioData\curated\bestLowQuality\small
  - - AudioData\curated\bestLowQuality\medium
  - - AudioData\curated\bestLowQuality\large
  negative_subsets:
  - - AudioData\curated\hardNeg\hardnet_conf_min_85
  - - AudioData\curated\hardNeg\hardneg_conf_min_99
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
  use_validation: false

```

