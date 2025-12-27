# Usage Instructions - copy this to higher level

1. Download the latest release of [BirdNET Analyzer](https://github.com/birdnet-team/BirdNET-Analyzer/releases/tag/v2.4.0)
2. Download desired [custom model](setup-workflow.md#custom-models), and unzip
3. Under 'Batch Analysis' - select your input directory with audio files to be reviewed, and output directory for results.
4. Adjust 'Inference Settings'. Recommended with Precision model:
   1. Sensitivity - 1.5
   2. Minimum Confidence - 0.3
   3. All else default
5. Adjust 'Species Selection'
   1. Select 'Custom Species List'
   2. select 'model\_Labels.txt' from zip file
6. Adjust 'Model selection'
   1. Select 'custom classifier' - model.tflite from zip file
7. Adjust output settings as desired. I recommend selecting 'Combine Selection Tables'



### Custom Models

Full descriptions of performance at [Final Model Analysis](results-overview/)

#### Recommended: High precision model

Recommended for general daily presence/absence monitoring, when recording many hours per day and where minimal manual review is desired.

Sens 1.5, threshold: 0.3;

F1: 76.1, Precision: 98.5, Recall: 62.0

adjust threshold to 0.05;&#x20;

F1: 80.0, Precision: 93.6, Recall: 70.0

{% file src=".gitbook/assets/Precision_Model_2025 (1).zip" %}

High F1 model

best config for f1: sensitivity .75, threshold 1.0

F1: .886, Precision: .897, Recall: .875

{% file src=".gitbook/assets/F1_Model_2025 (1).zip" %}

Full walkthrough from 2024 contract:

[https://tyler-schwenk.gitbook.io/workflow-rana-draytonii-analysis](https://tyler-schwenk.gitbook.io/workflow-rana-draytonii-analysis)
