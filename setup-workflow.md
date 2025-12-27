# Usage Instructions - copy this to higher level

run this back through birdnet gui and prep the actual workflow. give best config stuff\
\
copy from previous documentation! [https://tyler-schwenk.gitbook.io/workflow-rana-draytonii-analysis](https://tyler-schwenk.gitbook.io/workflow-rana-draytonii-analysis)



#### High precision model:

Recommended for general daily precensce/absence monitoring, when recording many hours per day and minimal manual review is desired.

Sens 1.5, threshold: 0.3;

F1: 76.1, Precision: 98.5, Recall: 62.0

adjust threshold to 0.05;&#x20;

F1: 80.0, Precision: 93.6, Recall: 70.0

{% file src=".gitbook/assets/Precision_Model_2025 (1).zip" %}

High F1 model

best config for f1: sensitivity .75, threshold 1.0

F1: .886, Precision: .897, Recall: .875

{% file src=".gitbook/assets/F1_Model_2025 (1).zip" %}
