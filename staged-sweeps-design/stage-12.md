# Stage 12

ok now ive found that error in the calculation bullshit. so im going to retest the different data subsets.



all stage 12 results will be redistributed through 9 and act like they werre always a part of them.&#x20;

here is stage 12 spec:<br>

```yaml
stage: 12
out_dir: config/sweeps/stage12_sweep
axes:
  seed:
  - 123
  - 456
  quality:
  - - high
  - - high
    - medium
    - low
  balance:
  - true
  - false
  negative_subsets:
  - []
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
  use_validation: true

```

\
\
before stage 12 being added stage 9 had 72 experiments, as defined by:<br>

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

now i will add the 24 from stage 12 to be in stage 9. i will do this by renaming stage 12\_001 - 024 to be stage 9\_073 - 9\_096. I will also have to rekon with the sweep design stuff.
