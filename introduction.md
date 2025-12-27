# Introduction

This project improves _Rana draytonii_ (RADR) call detection using BirdNET Analyzer. The primary goal is **higher daily detection precision**, so you review fewer false positives. The secondary goal is **robust performance under domain shift**, across sites and recorders.

This work delivers:

* **Custom CRLF classifiers** (high-precision and high-F1 operating points).
* A **fixed IID/OOD evaluation split** to measure generalization.
* A **staged sweep process** to isolate which settings actually matter.

### Where to go next

* [Usage Instructions](setup-workflow.md)\
  Pick a model, and run inference.
* [Final Model Analysis](results-overview/)\
  The headline results. Precision/recall tradeoffs. Comparisons to the 2024 baseline.
* [Audio Data Split Design](audio-data-split-design/)\
  How the labeled dataset was built and split. Includes the strict OOD (held-out site) test.
* [Parameter Effects](parameter-effects/)\
  Deep dives on what moved metrics: data composition, augmentation, regularization, imbalance, and hyperparameters.
* [Alternative Methodologies Explored](other-methodologies-explored/)\
  Approaches that were explored, and either dropped or held for future development.
* [Environmental Impact](environmental-impact.md)\
  Training cost and practical compute notes.
* [Staged Sweeps Design](staged-sweeps-design/)\
  The full archive of experiments designed and evaluated over the course of this contract.

### Resources

* Training pipeline repo: [https://github.com/Tyler-Schwenk/BirdNET-CustomClassifierSuite](https://github.com/Tyler-Schwenk/BirdNET-CustomClassifierSuite)
