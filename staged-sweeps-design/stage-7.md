# Stage 7 - Focus on specific call type

In this experimental stage, I briefly explored the idea of training the model to identify specific types of the California red-legged frog's call, rather than both as the same label.&#x20;



This would take a significant amount of time to make a new experiment structure and testing dataset around each call type, and I consider it out of the scope of this current contract. It is an idea that could be explored in the future though



#### Stage 7 – OOD Performance Summary

| Experiments                           | Balance | Call Type          | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) |
| ------------------------------------- | ------- | ------------------ | ------------------- | -------------------------- | ----------------------- |
| stage7\_001, stage7\_005, stage7\_009 | Yes     | grunt, growl, both | 0.778 ± 0.045       | 0.899 ± 0.063              | 0.695 ± 0.111           |
| stage7\_002, stage7\_006, stage7\_010 | Yes     | grunt, both        | 0.754 ± 0.035       | 0.874 ± 0.042              | 0.669 ± 0.080           |
| stage7\_003, stage7\_007, stage7\_011 | No      | grunt, growl, both | 0.756 ± 0.047       | 0.833 ± 0.111              | 0.717 ± 0.145           |
| stage7\_004, stage7\_008, stage7\_012 | No      | grunt, both        | 0.708 ± 0.009       | 0.983 ± 0.022              | 0.554 ± 0.013           |

```yaml
stage: 7
out_dir: config/sweeps/stage7_sweep
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
  call_type:
  - - grunt
    - growl
    - both
  - - grunt
    - both
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

{% file src="../.gitbook/assets/stage_7_leaderboard_table.csv" %}
