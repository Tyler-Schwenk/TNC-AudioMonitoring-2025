# Stage 11

## **Experimental Design**

**Sweep Parameters**

* **Seeds:** 123, 456, 789
* **Balance:** True (fixed)
* **Positive Subsets:**
  * None (baseline - no additional positives)
  * bestLowQuality\small (smallest curated set)
  * bestLowQuality\medium (medium-sized curated set)
  * bestLowQuality\top50 (top 50 quality samples)
  * bestLowQuality\large (largest curated set)
* **Negative Subsets:**
  * hardneg\_conf\_min\_99 (highest confidence false positives)
  * hardnet\_conf\_min\_85 (high+ confidence false positives)

**Base Config**

* **Validation:** False
* **Quality:** \[High, Medium]
* **Mixup:** True
* **Label Smoothing:** True
* **Focal Loss:** False
* **Dropout:** 0.25
* **Learning Rate:** 0.0005
* **Hidden Units:** 512 (default)
* **Epochs:** 50
* **Frequency Range:** 0-15000 Hz
* **Upsampling:** None (ratio 0.0)
