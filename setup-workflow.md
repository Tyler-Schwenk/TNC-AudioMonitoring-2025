# Usage Instructions

## Setup & First Inference

1. Download desired [custom model](setup-workflow.md#custom-models), and unzip.
2. Download the latest release of [BirdNET Analyzer](https://github.com/birdnet-team/BirdNET-Analyzer/releases/tag/v2.4.0), and run.
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

***

## Custom Models

Full descriptions of performance at [Final Model Analysis](results-overview/)

#### Recommended: High Precision model

Recommended for general daily presence/absence monitoring - when recording high volumes of data and where minimal manual review is desired.

Ideal config for high Precision - **Sensitivity:** 1.5, **Minimum Confidence**: 0.3

3-second file-level performance:&#x20;

F1: 76.1, Precision: 98.5, Recall: 62.0

{% hint style="info" %}
Adjusting 'Minimum Confidence' down increases Recall at a cost to Precision. For example, at Minimum Confidence: 0.05 the model performs at F1: 80.0, Precision: 93.6, Recall: 70.0 at the file level.
{% endhint %}

{% file src=".gitbook/assets/Precision_Model_2025 (1).zip" %}

#### High F1 model

The model reaching highest overall performance metrics. Best used for more fine-grained analysis where&#x20;

Ideal config for high F1 - **Sensitivity**: .75, **Minimum Confidence**: 1.0

3-second file-level performance:&#x20;

F1: 88.6, Precision: 89.7, Recall: 87.5

{% file src=".gitbook/assets/F1_Model_2025 (1).zip" %}

Full walkthrough of BirdNET Analysis from 2024 contract:

[https://tyler-schwenk.gitbook.io/workflow-rana-draytonii-analysis](https://tyler-schwenk.gitbook.io/workflow-rana-draytonii-analysis)
