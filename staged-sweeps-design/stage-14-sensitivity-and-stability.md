# Stage 14 - Sensitivity Testing

### Experimental Design <a href="#experimental-design" id="experimental-design"></a>

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Sensitivity**: 0.5, 0.75, 1.0, 1.25, 1.5
* **Seed**: 123, 456, 789

#### Base Config <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Quality**: \[High, Medium]
* **Positive Subset**: Small
* **Negative Subset**: hardneg\_conf\_min\_50
* **Validation**: True
* **Balance**: True
* **Mixup**: True
* **Label Smoothing**: True
* **Focal Loss:** False
* **learning rate: 0.001**
* **dropout: 0.25**
* **hidden units: 512**



```yaml
stage: 14
out_dir: config/sweeps/stage14_sweep
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
