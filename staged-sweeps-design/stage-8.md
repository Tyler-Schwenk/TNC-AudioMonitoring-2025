# Stage 8 - Appended label

Following up on a discussion from one of our meetings - this was another experimental sweep to gauge the effectiveness of monitoring for both RADR and Bullfrogs at the same time.

Appended labels could be beneficial when being deployed on a device with limited space for custom models, if we are also trying to monitor for a wider range of species within an environment.

This was tested briefly (only 3 seeds total) to get a baseline idea of how effective monitoring for both species at the same time could be.&#x20;

#### Stage 8 – OOD Comparison to Identical Config with replace mode

| Experiments | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) |
| ----------- | ------------------- | -------------------------- | ----------------------- |
| Append      | 0.745 ± 0.015       | 0.929 ± 0.036              | 0.622 ± 0.007           |
| Replace     | 0.837 ± 0.141       | 0.855 ± 0.137              | 0.836 ± 0.189           |

```yaml
stage: 8
out_dir: config/sweeps/stage8_append_test
axes:
  seed:
  - 123
  - 456
  - 789
  quality:
  - - high
    - medium
base_params:
  # Append mode: only use positive examples
  # BirdNET's 6000+ species act as implicit negatives
  model_save_mode: append
  include_negatives: false
  balance: false  # No negatives to balance with
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
