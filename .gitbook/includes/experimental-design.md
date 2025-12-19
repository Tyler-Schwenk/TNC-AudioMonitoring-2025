---
title: Experimental Design
---

## Experimental Design <a href="#experimental-design" id="experimental-design"></a>

### Sweep Parameters <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Seeds**: 3 (123, 456, 789) for reproducibility testing
* **Balance**: True/False (class balancing on/off)
* **Quality levels**: 2 (\[high] only, \[high, medium, low]) - \*These were only swept with no positive subsets to avoid redundancy.
* **Positive Subsets**:
  * None (baseline: 2,017 files)
  * small (+51 files from bestLowQuality)
  * top50 (+515 files from bestLowQuality)
* **Negative Subsets**:
  * None (baseline: 8,525 files)
  * hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
  * hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

### Base Config <a href="#sweep-parameters" id="sweep-parameters"></a>

* **Validation**: False&#x20;
* **Mixup**: True
* **Label Smoothing**: true
* **Dropout**: 0.25
* **Focal Loss:** False
* **Learning Rate**: 0.0005
