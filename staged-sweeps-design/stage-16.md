# stage 16

full dataset, ,&#x20;

sweep mixup, label smoothing, balance, validation.



then go over hyper parameters again.

once this is finished, we will have confrmed our best setup and finalize sensitivity and run with a bunch of seeds for stability. then finally get our

info:
Label Smoothing (LS) and Mixup are regularization techniques to combat overfitting and improve generalization, but they work differently: LS softens "hard" one-hot labels (e.g., from [0, 0] to [0.1, 0.1, 0.8]), teaching models less certainty, while Mixup creates synthetic data by linearly blending input features AND their labels, encouraging smoother, more robust decision boundaries, often outperforming LS for calibration by creating more inherent data variation. Mixup inherently includes label smoothing effects but adds feature mixing, making it a powerful, domain-agnostic regularizer that fosters better calibration and robustness against OOD data. 
Both label smoothing and Mixup are regularization techniques that can help with imbalanced data, but they address the problem differently and Mixup-based methods offer more tailored solutions for imbalance. 


## Label Smoothing (LS)


Label smoothing is a loss function modification that discourages models from becoming overconfident in a single class. 
Mechanism: Instead of using "hard" one-hot labels (e.g., [1, 0, 0]), it creates "soft" targets by distributing a small amount of probability mass to all other classes (e.g., [0.9, 0.05, 0.05]). This adds noise to the labels, improving generalization and robustness.
Role in Unbalanced Data: In imbalanced datasets, it can prevent the model from overfitting to the majority class by forcing it to be less certain of those predictions, which indirectly benefits the minority class performance.
Limitation: It is a general regularization technique and does not explicitly generate new data or balance the distribution of samples. Its effect on imbalance is a byproduct of its regularizing nature. 

## Mixup
Mixup is a data augmentation technique that synthesizes new training examples by linearly interpolating both input features and their corresponding labels from two random samples. 
Mechanism: It creates "virtual" data points and "soft" labels, effectively smoothing the decision boundaries in the feature space and reducing intra-class variance.
Role in Unbalanced Data: Standard Mixup samples randomly, which can sometimes exacerbate the data imbalance. However, specific Mixup variants have been developed to directly target imbalanced data:
BalanceMix / Balanced MixUp uses intelligent sampling strategies (e.g., ensuring minority-augmented instances are generated) to create a more balanced training distribution.
Calibrated Mixup generates high-fidelity synthetic samples for underrepresented regions through targeted mixup and refinement strategies.
Advantage over LS: Mixup actually creates new data points, enriching the training distribution and directly addressing the lack of minority samples, especially when sampling methods are adjusted for imbalance. 
