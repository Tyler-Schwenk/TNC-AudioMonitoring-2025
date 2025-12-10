---
description: >-
  FIRST!! ADD  FULL DESCRIPTOIN OF WHAT THESE SUBSETS ARE/ HOW THEY WERE
  GATHERED
---

# Stage 6: Data Composition

### Executive Summary <a href="#executive-summary" id="executive-summary"></a>

Stage 6 systematically tested the impact of curated data subsets on model performance using a 54-experiment sweep (3 seeds × 2 balance settings × 3 positive subsets × 3 negative subsets).





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

tyler is now adding new configs to stage 6 to test the other standard datasets, like this:\
Created 36 new Stage 6 config files (stage6\_055 through stage6\_090)

**Experimental Matrix:**

* **Seeds**: 3 (123, 456, 789)
* **Balance**: 2 (true, false)
* **Negative subsets**: 3 (none, hardneg\_conf\_min\_50, hardneg\_conf\_min\_99)
* **Quality levels**: 2 (\[high] only, \[high, medium, low])
* **Positive subsets**: 0 (none - as requested)
* **Validation**: false (Stage 6 style)

This fills the gap in your experimental design, letting you compare:

* High-quality-only baseline vs full quality spectrum
* With/without validation package (Stage 6 vs Stage 12)
* Impact of hard negatives at both quality levels







#### How Subsets were created <a href="#evaluation-metrics" id="evaluation-metrics"></a>

* **Positive Subsets:**
  * The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model.&#x20;
  * This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through  which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted i nthe 4 folders below:\
    small: 51 (5%), medium: 154 (15%), large: 309 (30%), top50: 515 (50%)
* **Negative Subsets:**
  * I took 20,457 new (entirely outside the train/test/val data) negative audio files from brad's audio (audio recorders 2, 9, and 10) and ran them through inference using model stage3\_046. Then to determine the hardest negative files, I took subsets based on the highest confidence value for RADR fora given audio file. The subsets I took were based on the minimum confidence value for the audio file. so I gathered the following subsets:
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_85 (+981 hard negatives at 85% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)



### Results

| Balance | Positive Subset | Negative Subset | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) |
| ------- | --------------- | --------------- | ------------------- | -------------------------- | ----------------------- |
| Yes     | none            | hardneg\_99     | **0.902 ± 0.057**   | **0.832 ± 0.098**          | **0.991 ± 0.008**       |
| Yes     | top50           | hardneg\_99     | **0.893 ± 0.035**   | **0.835 ± 0.065**          | **0.963 ± 0.009**       |
| Yes     | small           | none            | **0.891 ± 0.056**   | **0.852 ± 0.124**          | **0.944 ± 0.048**       |
| Yes     | top50           | none            | **0.887 ± 0.035**   | **0.802 ± 0.059**          | **0.993 ± 0.008**       |
| No      | small           | hardneg\_50     | **0.888 ± 0.047**   | **0.803 ± 0.077**          | **0.997 ± 0.004**       |
