# Mixup

### Mixup

Mixup is a data augmentation technique that synthesizes new training examples by linearly interpolating both input features and their corresponding labels from two random samples.

Mechanism: It creates "virtual" data points and "soft" labels, effectively smoothing the decision boundaries in the feature space and reducing intra-class variance.

Role in Unbalanced Data: Standard Mixup samples randomly, which can sometimes exacerbate the data imbalance. However, specific Mixup variants have been developed to directly target imbalanced data:

BalanceMix / Balanced MixUp uses intelligent sampling strategies (e.g., ensuring minority-augmented instances are generated) to create a more balanced training distribution.

Calibrated Mixup generates high-fidelity synthetic samples for underrepresented regions through targeted mixup and refinement strategies.

Advantage over LS: Mixup actually creates new data points, enriching the training distribution and directly addressing the lack of minority samples, especially when sampling methods are adjusted for imbalance.
