# NOTES TO SELF

* **Positive Subsets:**
  * The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model.&#x20;
  * This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through  which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted i nthe 4 folders below:\
    small: 51 (5%), medium: 154 (15%), large: 309 (30%), top50: 515 (50%)
  * RENAMING: top50 -> extra large
* **Negative Subsets:**
  * I took 20,457 new (entirely outside the train/test/val data) negative audio files from brad's audio (audio recorders 2, 9, and 10) and ran them through inference using model stage3\_046. Then to determine the hardest negative files, I took subsets based on the highest confidence value for RADR fora given audio file. The subsets I took were based on the minimum confidence value for the audio file. so I gathered the following subsets:
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_85 (+981 hard negatives at 85% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

**how the heck are we computing metrics? for deciding precision, do we take a minimunm confidence threshold? how doe sthis relate to sensitivity?**&#x20;

### **Evaluation Logic - Concise Summary**

#### **How it works:**

1. **Per-file scoring**: Each audio file gets ONE score = max RADR confidence across all detections
2. **No minimum confidence**: Even 0.01 counts if it's the highest RADR detection
3. **Negative predictions ignored**: Only looks at RADR detections, not other species
4. **Threshold sweep**: Tests 21 thresholds (0.0, 0.05, 0.10, ..., 1.0) to find best F1

#### **Code snippet:**

```python
# From evaluate_results.py line 197-201
radr = df[df["Scientific name"] == "RADR"].groupby("File")["Confidence"].max()
files = files.merge(radr.rename("score"), on="File", how="left")
files["score"] = files["score"].fillna(0.0)  # No RADR detection = 0.0
```



#### **Example:**

* File has RADR detections: \[0.03, 0.12, 0.85] → **Score = 0.85**
* File has no RADR detections → **Score = 0.0**
* At threshold 0.5: score ≥ 0.5 → predicted positive
* "best\_f1" = whichever threshold (0.0-1.0) gives highest F1

#### **Key takeaway:**

Any RADR detection, no matter how low, contributes to the file score. There's no confidence filtering before evaluation.



**THEBIG BUG:**\
**The Bug:**

1. BirdNET only outputs CSV rows for files where it detects **ANY species above the confidence threshold**
2. If a file has NO detections above threshold → **BirdNET outputs NOTHING** for that file (no row at all)
3. The old evaluation code only processed files **present in BirdNET output**
4. Files missing from BirdNET output = **never evaluated at all**

**Real-world example (stage14\_013):**

* Test set: 3,585 files (1,691 RADR positive, 1,894 negative)
* BirdNET output: Only 888 files (all positive)
* **Missing: 2,697 files** (803 positives + 1,894 negatives)
  * The model detected RADR in 888 positive files
  * For the other 2,697 files: **no detections above confidence threshold** → no output row

**This is DIFFERENT from predicting "Negative":**

* **Predicting "Negative"** = model outputs "Negative" class → BirdNET writes a row
* **No detection** = model finds nothing above min\_conf → BirdNET writes NO row

**Why stage14\_013 was so broken:**

* Model only outputs RADR predictions, never "Negative"
* Conservative model: only confident on actual RADRs
* For negatives: no detection above threshold → no BirdNET output row
* Old evaluation: missing files ignored → metrics looked perfect (F1=0.992)
* Fixed evaluation: missing files scored as 0.0 → correct metrics (F1=0.681)

So yes - files with no prediction whatsoever weren't counted at all in the old evaluation! 🎯
