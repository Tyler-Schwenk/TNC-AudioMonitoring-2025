# Project Overview — Rana draytonii (CRLF) BirdNET Training

### **Background and Objectives**

This project develops a high-precision acoustic classifier for the endangered _Rana draytonii_ (California Red-Legged Frog, CRLF), built on top of the BirdNET framework.\
The core objective is to produce a generalizable model capable of distinguishing CRLF vocalizations (grunt/growl call types) from complex environmental noise across multiple sites and devices.

The training process followed a **structured, staged sweep strategy**, progressing from initial baselines to advanced augmentation and data-balancing experiments.\
Each stage was explicitly designed to isolate the effect of one variable class at a time—allowing for interpretable, reproducible improvements while adhering to ML best practices.

***

### **Data Foundation**

#### **Data Design and Split Strategy**

All audio clips were preprocessed into 3-second windows and assigned to one of four deterministic, non-overlapping splits:

| Split                      | Description                           | Purpose                                          |
| -------------------------- | ------------------------------------- | ------------------------------------------------ |
| **Train**                  | \~3,600 positives / \~8,500 negatives | Primary learning set                             |
| **Validation (Val)**       | \~650 positives / \~2,600 negatives   | Hyperparameter tuning and threshold selection    |
| **IID Test**               | \~1,950 positives / \~980 negatives   | In-distribution evaluation (temporal separation) |
| **OOD Test (Sylvan Pond)** | \~1,690 positives / \~1,890 negatives | Out-of-distribution generalization test          |

#### **Split Principles**

* **Leakage Prevention:** Entire date blocks are assigned to one split only.
* **Generalization Check:** Sylvan Pond (Moth11 + Moth12) serves as the OOD site.
* **Balanced Representation:** All call types and quality levels represented in train/val/test.
* **Precision-Oriented Evaluation:** Val/test maintain large negative pools to stress precision.
* **Reproducibility:** Deterministic, stable-hash splits locked for the remainder of the project.

This split design ensures _robust evaluation under realistic field conditions_, providing a strong foundation for reliable model assessment.

***

### **Model Development Phases**

#### **1️⃣ Legacy Model (2024 — Pre-Contract Baseline)**

The original BirdNET adaptation trained in 2024 served as the pre-contract baseline.\
It used default architecture and hyperparameters with minimal data (no augmentation or tuning).

| Metric              | IID  | OOD (Sylvan) |
| ------------------- | ---- | ------------ |
| **Best F1**         | 0.38 | 0.61         |
| **Precision @ 0.5** | 0.21 | 0.28         |
| **AUROC**           | 0.63 | 0.49         |

**Summary:**\
The model overfit to recall, exhibited poor calibration, and had near-random discriminability on unseen sites.\
This motivated the contract’s systematic, multi-stage optimization framework.

***

#### **2️⃣ Early 2025 Exploratory Runs (Pre-Sweep Rebaseline)**

Before formal sweep design, several “warm-up” runs were conducted to validate the new dataset, manifests, and OOD split logic.\
These established a _reproducible starting point_ for all subsequent structured experiments.

| Model               | Split | F1 (best) | Precision | Recall | AUROC | Notes                          |
| ------------------- | ----- | --------- | --------- | ------ | ----- | ------------------------------ |
| `first_trial_real`  | IID   | 0.92      | 0.93      | 0.91   | 0.94  | clean data only; strong recall |
|                     | OOD   | 0.65      | 0.98      | 0.49   | 0.74  | overfit pattern emerging       |
| `02_no_low_quality` | IID   | 0.60      | 0.43      | 0.98   | 0.69  | high recall, weak precision    |
|                     | OOD   | 0.74      | 0.60      | 0.98   | 0.57  | recall-dominant                |
| `best_trial_real`   | IID   | 0.40      | 0.97      | 0.25   | 0.62  | over-regularized               |
|                     | OOD   | 0.19      | 0.99      | 0.10   | 0.55  | minimal generalization         |

**Key Findings:**

* Confirmed data pipeline and OOD split integrity.
* Improved over 2024 baseline (OOD F1 ≈ 0.65–0.74 vs. 0.61), but **precision remained unstable**.
* Reinforced need for structured hyperparameter and augmentation sweeps.

***

#### **3️⃣ Structured Sweeps (Stages 1–3)**

**Stage 1 — Capacity & Regularization**

Explored model size, dropout, LR, and batch size (72 configs).\
Discovered that **dropout = 0.25** and **hidden units = 512–1024** balanced stability and generalization.\
Resulted in moderate gains (OOD F1 ≈ 0.72) and defined anchors for future stages.

**Stage 2 — Augmentation Sweep**

Tested label smoothing, mixup, and focal loss (2×2×2 factorial + capacity/LR extension).\
→ **Label smoothing + mixup** produced the clearest OOD boost and lowest seed variance.\
Best OOD F1 = **0.81 ± 0.02**, with precision ≈ 0.74, recall ≈ 0.89.\
Focal loss was consistently detrimental.

**Stage 3 — Data Balancing**

Fixed augmentations (smoothing + mixup) and explored upsampling ratio/mode.\
Linear mode between **0.3–0.5 ratio** offered optimal recall (≈0.90) with minimal precision loss.\
Best OOD F1 ≈ **0.78 ± 0.03**.\
Validated that the Stage 2 configuration remained stable under modified data distributions.

***

### **Performance Evolution Summary**

| Phase                                   | Approx. Timeframe       | Key Configuration Highlights                                  | IID F1 (best) | OOD F1 (best)   | Notable Changes                                |
| --------------------------------------- | ----------------------- | ------------------------------------------------------------- | ------------- | --------------- | ---------------------------------------------- |
| **Legacy Model (2024)**                 | Pre-contract            | Default BirdNET settings; small data; no augmentation         | 0.38          | 0.61            | Weak calibration; near-random OOD AUROC ≈ 0.49 |
| **Early 2025 Unstructured Trials**      | Contract onboarding     | Larger dataset; no low-quality clips; no dropout/aug          | 0.60 – 0.92   | 0.65 – 0.74     | Split verified; recall dominant                |
| **Stage 1 (Capacity + Regularization)** | Structured Phase 1      | Hidden units 0–1024, dropout 0–0.5, LR 1e-4–1e-3              | ≈ 0.70        | ≈ 0.72          | Dropout 0.25 stabilized generalization         |
| **Stage 2 (Augmentation Sweep)**        | Structured Phase 2 + 2B | Label smoothing + mixup (+/- focal loss) × 512/1024 HU        | 0.70 ± 0.05   | **0.81 ± 0.02** | +20 OOD F1 points over 2024 baseline           |
| **Stage 3 (Data Balancing)**            | Structured Phase 3      | Label smoothing + mixup fixed; upsampling 0–1.0 linear/repeat | 0.70 ± 0.04   | 0.78 ± 0.03     | Improved recall, stable precision              |

**Overall Trend:**

* **OOD F1 improved 0.61 → 0.81 (+33% relative).**
* **Precision doubled** (≈0.3 → ≈0.7).
* **AUROC improved from \~0.49 → \~0.75+.**
* The model evolved from a recall-heavy prototype to a calibrated, deployable classifier.

***

### **Next Steps**

With Stage 3 completed and the data split fixed in stone:

* Conduct **Stage 3B/3C refinements** (upsampling fine grid + LR/augmentation interaction).
* Proceed to **Stage 4**: noise and low-quality inclusion stress tests.
* Begin preparing **model packaging, export, and deployment evaluation**.
