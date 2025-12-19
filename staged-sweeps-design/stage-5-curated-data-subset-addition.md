# Stage 5 - Curated Data Subset Addition

This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through stage4\_038 which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted i nthe 4 folders below:\
small: 51 (5%), medium: 154 (15%), large: 309 (30%), xl: 515 (50%)



it looks like stage 5 had pretty much the same config as stag 6, but wit all subsets of data, and keeping mixup and label smoothing false instead of true.:<br>

```yaml
stage: 5
out_dir: config/sweeps/stage5_sweep
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
  - false
  positive_subsets:
  - []
  - - AudioData\curated\bestLowQuality\large
  - - AudioData\curated\bestLowQuality\medium
  - - AudioData\curated\bestLowQuality\small
  - - AudioData\curated\bestLowQuality\top50
  negative_subsets:
  - []
  - - AudioData\curated\hardNeg\hardneg_conf_min_50
  - - AudioData\curated\hardNeg\hardneg_conf_min_99
  - - AudioData\curated\hardNeg\hardnet_conf_min_85
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
  fmax: 15000
  overlap: 0.0

```
