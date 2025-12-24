# Stage 6 - Data Composition

### Executive Summary <a href="#executive-summary" id="executive-summary"></a>

Stage 6 systematically tested the impact of curated data subsets on model performance using a 54-experiment sweep (3 seeds × 2 balance settings x 3 positive subsets × 3 negative subsets).

{% include "../.gitbook/includes/experimental-design.md" %}

```yaml
stage: 6
out_dir: config/sweeps/stage6_sweep
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
  - - AudioData\curated\bestLowQuality\small
  - - AudioData\curated\bestLowQuality\top50
  negative_subsets:
  - []
  - - AudioData\curated\hardNeg\hardneg_conf_min_50
  - - AudioData\curated\hardNeg\hardneg_conf_min_99
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

```

### Results

{% file src="../.gitbook/assets/stage_6_leaderboard_table.csv" %}
