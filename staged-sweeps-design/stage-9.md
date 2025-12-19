# Stage 9 - Custom Validation Set

This was where i ttempted using my custom validation set instead of the birdnet default pulling 20 from my standard set.

and swept all subsets. \
as described here:<br>

Validation true = using my custom validation set that was held out:

* 15% of date blocks were held out from each recorder/site for hyperparameter tuning and threshold selection.  (647 positives, 2602 negatives)&#x20;

Validation False = using birdnet default validation set

* 20% randomly selected from training data



### Experimental Design <a href="#experimental-design" id="experimental-design"></a>

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Validation**: True & False
* **Positive Subsets**:
  * small (+51 files from bestLowQuality)
  * medium (+154 files from bestLowQuality)
  * large (+309 files from bestLowQuality)
  * extra large (+515 files from bestLowQuality)
* **Negative Subsets**:
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_85 (+899 hard negatives at 85% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

#### Base Config <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Quality**: \[High, Medium]
* **Balance**: true
* **Mixup**: True
* **Label Smoothing**: true
* **Dropout**: 0.25
* **Focal Loss:** False
* **Learning Rate**: 0.0005

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

{% file src="../.gitbook/assets/Stage_9_leaderboard_table.csv" %}
