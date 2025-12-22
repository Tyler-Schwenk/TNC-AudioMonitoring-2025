# Label Smoothing

## Label Smoothing (LS)

Todo: Does this even make sense wit 2-calss data?

Label smoothing is a loss function modification that discourages models from becoming overconfident in a single class. Mechanism: Instead of using "hard" one-hot labels (e.g., \[1, 0, 0]), it creates "soft" targets by distributing a small amount of probability mass to all other classes (e.g., \[0.9, 0.05, 0.05]). This adds noise to the labels, improving generalization and robustness.

Role in Unbalanced Data:

In imbalanced datasets, it can prevent the model from overfitting to the majority class by forcing it to be less certain of those predictions, which indirectly benefits the minority class performance. Limitation: It is a general regularization technique and does not explicitly generate new data or balance the distribution of samples. Its effect on imbalance is a byproduct of its regularizing nature.
