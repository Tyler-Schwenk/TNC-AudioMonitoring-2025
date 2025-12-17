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

Config we will carry forward:&#x20;

Learning Rate:

ALL THESE GRAPHS WILL NEED TO BE UPDATED

<figure><img src="../.gitbook/assets/chart_Learning_Rate_OOD_F1.svg" alt=""><figcaption></figcaption></figure>

Dropout:



<figure><img src="../.gitbook/assets/chart_Dropout_OOD_F1.svg" alt=""><figcaption></figcaption></figure>

Hidden units:<br>

<figure><img src="../.gitbook/assets/chart_Hidden_Units_OOD_F1 (1).svg" alt=""><figcaption></figcaption></figure>



full results:
