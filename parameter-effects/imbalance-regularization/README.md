# Imbalance Regularization

Two imbalance regularization techniques will be tested. To do this I will sweep across two datasets: \[high, medium, low] and \[high, medium]. I will sweep three upsampling modes: linear, mean, and SMOTE - each at 3 ratios - 0.0, 0.5, 1.0. I will also sweep including focal loss on all iterations. All configurations will be repeated 3 times with different seeds, resulting in 108 experiments.

### Upsampling

**Goal**\
Address class imbalance by augmenting the minority class (positive RADR call samples) to improve the model's ability to learn discriminative features from limited positive examples without sacrificing precision.

**Mechanism**\
Upsampling generates synthetic minority class samples to balance the training distribution, preventing the model from developing a strong bias toward the majority class (non-RADR calls). Three variants will be tested: **Linear interpolation** creates new samples by blending feature representations between existing positive examples; **Mean upsampling** replicates samples by adding Gaussian noise around class centroids; **SMOTE (Synthetic Minority Over-sampling Technique)** generates synthetic examples in feature space by interpolating between k-nearest neighbors of minority class samples. Each approach trades off between distributional realism and augmentation diversity—linear interpolation preserves local structure but may introduce unrealistic intermediate representations, mean upsampling maintains sample authenticity but risks overfitting through duplication, while SMOTE balances novelty and plausibility but can generate out-of-distribution artifacts in sparse feature regions.

***

### Focal Loss

**Goal**\
Improve discrimination of hard-to-classify examples by dynamically reweighting the loss function to focus learning on challenging samples rather than easy negatives.

**Mechanism**\
Focal loss modifies the standard cross-entropy objective by down-weighting well-classified examples and amplifying the contribution of misclassified or uncertain predictions. The loss applies a modulating factor (1 - p\_t)^γ where p\_t is the model's confidence in the correct class, effectively reducing the loss contribution from high-confidence correct predictions while maintaining strong gradients for low-confidence or incorrect predictions. This is particularly valuable in imbalanced scenarios where the model can achieve high accuracy by correctly classifying abundant easy negatives while failing on rare but critical positive examples (RADR calls). Focal loss encourages the model to allocate representational capacity toward difficult boundary cases and ambiguous spectrotemporal patterns, potentially improving recall on edge-case vocalizations without sacrificing precision on clear examples.
