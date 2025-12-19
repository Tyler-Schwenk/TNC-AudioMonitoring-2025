# Stage 5 - Curated Data Subset Addition

Stage 5 tested the addition of curated data sets - specifically; new mined hard negatives from field data that was previously now included in our dataset at all, and and subsets of our low quality data that were of higher quality. All tests were run with no mixup or label smoothing.

#### How Subsets were created <a href="#evaluation-metrics" id="evaluation-metrics"></a>

* **Positive Subsets:**
  * The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model.&#x20;
  * This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through  which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted in the 4 folders below:\
    small: 51 (5%), medium: 154 (15%), large: 309 (30%), top50: 515 (50%)
* **Negative Subsets:**
  * I took 20,457 new (entirely outside the train/test/val data) negative audio files from brad's audio (audio recorders 2, 9, and 10) and ran them through inference using model stage3\_046. Then to determine the hardest negative files, I took subsets based on the highest confidence value for RADR fora given audio file. The subsets I took were based on the minimum confidence value for the audio file. so I gathered the following subsets:
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_85 (+981 hard negatives at 85% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Balance**: True/False (class balancing on/off)
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

* **Validation**: False&#x20;
* **Quality**: \[High, Medium]
* **Mixup**: False
* **Label Smoothing**: False
* **Dropout**: 0.25
* **Focal Loss:** False
* **Learning Rate**: 0.0005
