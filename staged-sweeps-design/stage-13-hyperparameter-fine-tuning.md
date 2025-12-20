# Stage 13 - Hyperparameter fine-tuning

taking the best config from all of the runs - stage 9\_006, and running with it. sweeping across all hyperparameters

### Experimental Design <a href="#experimental-design" id="experimental-design"></a>

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Learning Rate**: 0.0001, 0.0005, 0.001
* **Dropout**: 0.0, 0.25 0.5, 0.75, 0.9
* **Hidden units**: 0, 128, 512, 1024

#### Base Config <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Quality**: \[High, Medium]
* **Positive Subset**: Small
* **Negative Subset**: hardneg\_conf\_min\_50
* **Validation**: True
* **Balance**: True
* **Mixup**: True
* **Label Smoothing**: True
* **Focal Loss:** False

### Results

#### Stage 13 – OOD Performance Summary (Top Configurations)

<table><thead><tr><th width="122.79998779296875">Experiments</th><th>Hidden Units</th><th>Dropout</th><th>Learning Rate</th><th>OOD F1 (mean ± std)</th><th>OOD Precision (mean ± std)</th><th>OOD Recall (mean ± std)</th></tr></thead><tbody><tr><td>stage13_021, stage13_057, stage13_093, stage13_153</td><td>512</td><td>0.0</td><td>0.001</td><td>0.950 ± 0.065</td><td>0.950 ± 0.070</td><td>0.950 ± 0.061</td></tr><tr><td>stage13_032, stage13_068, stage13_104, stage13_110, stage13_170</td><td>1024</td><td>0.25</td><td>0.0005</td><td>0.912 ± 0.081</td><td>0.938 ± 0.067</td><td>0.888 ± 0.097</td></tr><tr><td>stage13_030, stage13_066, stage13_102, stage13_168</td><td>1024</td><td>0.0</td><td>0.001</td><td>0.912 ± 0.108</td><td>0.963 ± 0.055</td><td>0.872 ± 0.154</td></tr><tr><td>stage13_029, stage13_065, stage13_101, stage13_167</td><td>1024</td><td>0.0</td><td>0.0005</td><td>0.862 ± 0.130</td><td>0.845 ± 0.193</td><td>0.914 ± 0.138</td></tr></tbody></table>

### Dropout

There was a clear trend of increased precision and stability across seeds as dropout increased, but this was countered with a decrease of recall. For this reason a dropout of 0.25 will be selected for its slight increase of precision and stability, without a major sacrifice of recall.

<figure><img src="../.gitbook/assets/chart_Dropout_OOD_F1.png" alt="" width="360"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/chart_Dropout_OOD_PRECISION.png" alt="" width="360"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/chart_Dropout_OOD_RECALL.png" alt="" width="360"><figcaption></figcaption></figure>

### Learning Rate

This graph shows the F1 of different learning rate values, at Dropout = 0.25



<figure><img src="../.gitbook/assets/chart_Learning_Rate_OOD_F1 (2).png" alt="" width="360"><figcaption></figcaption></figure>



### Hidden units

512 will be used for its increased stability, and avoiding risk of potential overfitting in higher hidden units

<figure><img src="../.gitbook/assets/chart_Hidden_Units_OOD_F1 (2).png" alt="" width="360"><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/chart_Hidden_Units_OOD_F1 (3).png" alt="" width="360"><figcaption></figcaption></figure>







full results:

{% file src="../.gitbook/assets/stage_13_leaderboard_table (1).csv" %}

**We will carry forward:**\
**learning rate: 0.001**

**dropout: 0.25**\
**hidden units: 1024**
