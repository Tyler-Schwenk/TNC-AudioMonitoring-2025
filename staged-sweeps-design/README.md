# Staged Sweeps Design

### Staged Sweep Strategy

#### Why staged sweeps?

* Keeps experiments interpretable.
* Reveals clear trends (learning curves, overfitting patterns, etc.).
* Matches ML best practices for hyperparameter optimization.
* Allows us to build on prior knowledge step by step.

***

#### Stage Design

#### Stage 1: Capacity & Regularization

**Goal:** Find the right model size and learning dynamics.

**Factors swept:**

* Hidden Units: \[0, 128, 512, 1024]
* Dropout: \[0.0, 0.25, 0.5]
* Learning Rate: \[1e-4, 5e-4, 1e-3]
* Batch Size: \[16, 32]
* Data: High + Medium quality only, balanced negatives
* Total configs: 72

**Key Insights:**

* Dropout = 0.25 consistently improved OOD generalization.
* Larger heads (1024 HU) gave the strongest averages, but smaller heads (128–512) occasionally outperformed on OOD.
* Learning rate: 1e-3 stable on average, 5e-4 produced the single best OOD run.
* Batch size: 32 slightly better than 16, but minor effect.
* Variability was high → multi-seed runs are needed in future stages.

**Anchors for Stage 2:**

* Hidden Units: 128–1024
* Dropout: 0.25
* Learning Rate: 5e-4–1e-3
* Batch Size: 32

[Full Stage 1 Results →](error-found-in-evaluation/archive-stage-1-capacity-and-regularization.md)

***

####

***

####

***

####

***

#### Expected Insights

* Does larger capacity help or overfit?
* Does dropout prevent collapse?
* Which learning rate regime works best?
* How does batch size interact with learning rate?
* Do augmentation methods (mixup, smoothing, focal loss) add robustness?
* Does synthetic balancing help recall without tanking precision?
* How robust is the model when exposed to noisy/low-quality calls?



### **Performance Evolution Overview (Legacy → Stage 4)**

| Phase                                               | Year / Stage Focus                      | Key Changes / Experiment Focus                      | OOD F1 (± SD)     | OOD Precision | OOD Recall | Qualitative Outcome                                                            |
| --------------------------------------------------- | --------------------------------------- | --------------------------------------------------- | ----------------- | ------------- | ---------- | ------------------------------------------------------------------------------ |
| **Legacy Baseline (2024)**                          | Pre-contract baseline                   | Default BirdNET model, no tuning, minimal negatives | **0.61 (–)**      | 0.32          | 0.93       | Overfit to recall; poor generalization; weak calibration                       |
| **Pre-Sweep Rebaseline (2025 Q1)**                  | Data pipeline validation                | Verified split logic; established OOD test site     | **0.70 (± 0.02)** | 0.54          | 0.86       | Stable training; confirmed OOD framework                                       |
| **Stage 1 — Capacity & Regularization**             | Controlled architecture search          | Hidden units × dropout × LR sweep                   | **0.72 (± 0.02)** | 0.58          | 0.88       | Found 512–1024 HU, dropout 0.25 as sweet spot                                  |
| **Stage 2 — Augmentation Sweep**                    | Data augmentation interaction           | Label smoothing + mixup (+/– focal loss)            | **0.81 (± 0.02)** | 0.74          | 0.89       | Major boost from combined augmentations; focal loss harmful                    |
| **Stage 3 — Data Balancing & Upsampling**           | Distribution control                    | Tested upsampling mode × ratio                      | **0.78 (± 0.03)** | 0.70          | 0.90       | Mild upsampling (0.3–0.5, linear) helped recall; precision stable              |
| **Stage 4 — Data Robustness & Quality Integration** | Realistic noise + imbalance stress test | Balanced vs unbalanced × upsampling mode/ratio      | **0.85 (± 0.02)** | 0.91          | 0.80–0.95  | Precision ↑ 20 pts; robust to noise and imbalance; best generalization to date |

***

#### **Performance Trajectory (Visual Summary)**

| Metric                                                      | Legacy → Stage 4 Δ |
| ----------------------------------------------------------- | ------------------ |
| **OOD F1:** 0.61 → **0.85 (+0.24 abs ≈ +39%)**              |                    |
| **Precision:** 0.32 → **0.91 (+0.59 abs ≈ 3× increase)**    |                    |
| **Recall:** 0.93 → **0.80–0.95 (stable across conditions)** |                    |
| **AUROC:** \~0.49 → \~0.78 (estimated from stage reports)   |                    |

***

#### **Interpretation**

* Each stage produced a **targeted, reproducible improvement** by isolating a single variable class:\
  capacity → augmentation → balancing → robustness.
* The model evolved from **recall-biased and fragile** to **precise, calibrated, and robust under noise.**
* Gains now plateau near F1 ≈ 0.85, suggesting the next logical step (Stage 5) should stress **domain shift and external generalization**, not additional tuning of the same dataset.
