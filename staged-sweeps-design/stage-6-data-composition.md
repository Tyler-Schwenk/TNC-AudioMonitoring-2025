---
description: >-
  FIRST!! ADD  FULL DESCRIPTOIN OF WHAT THESE SUBSETS ARE/ HOW THEY WERE
  GATHERED
---

# Stage 6: Data Composition

### Executive Summary <a href="#executive-summary" id="executive-summary"></a>

Stage 6 systematically tested the impact of curated data subsets on model performance using a 54-experiment sweep (3 seeds × 2 balance settings × 3 positive subsets × 3 negative subsets).

**Key Finding**: The combination of **top50 positive subset + hardneg\_99 negative subset + class balancing** achieved the best performance with F1=0.945 on OOD data, representing a **10.9% improvement** over the baseline (F1=0.852).



### Experimental Design <a href="#experimental-design" id="experimental-design"></a>

#### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Balance**: True/False (class balancing on/off)
* **Positive Subsets**:
  * None (baseline: 2,017 files)
  * small (+51 files from bestLowQuality)
  * top50 (+515 files from bestLowQuality)
* **Negative Subsets**:
  * None (baseline: 8,525 files)
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

#### How Subsets were created <a href="#evaluation-metrics" id="evaluation-metrics"></a>

* **Positive Subsets:**
  * The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model.&#x20;
  * This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through  which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted i nthe 4 folders below:\
    small: 51 (5%), medium: 154 (15%), large: 309 (30%), xl: 515 (50%)
* **Negative Subsets:**
  * I took 20,457 new (entirely outside the train/test/val data) negative audio files from brad's audio (audio recorders 2, 9, and 10) and ran them through inference using model stage3\_046. Then to determine the hardest negative files, I took subsets based on the highest confidence value for RADR fora given audio file. The subsets I took were based on the minimum confidence value for the audio file. so I gathered the following subsets:
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_85 (+981 hard negatives at 85% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)
