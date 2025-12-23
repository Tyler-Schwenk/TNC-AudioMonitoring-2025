# Regularization techniques

### Label Smoothing

#### Goal

I hope to reduce overconfidence on ambiguous positive and negative examples, improving OOD generalization and decision-boundary stability.&#x20;

#### Mechanism

Label smoothing is a loss function modification that discourages models from becoming overconfident in a single class, applied during the BirdNET model training. Instead of using "hard" one-hot labels (e.g., \[1, 0, 0]), it creates "soft" targets by distributing a small amount of probability mass to all other classes (e.g., \[0.9, 0.05, 0.05]). This adds noise to the labels, improving generalization and robustness.

In imbalanced datasets, it can prevent the model from overfitting to the majority class by forcing it to be less certain of those predictions, which indirectly benefits the minority class performance.&#x20;

***

### Mixup

#### **Goal**

Reduce overconfidence and improve OOD generalization by encouraging smoother decision boundaries through training on interpolated examples rather than relying solely on hard, discrete samples.

#### **Mechanism**

Mixup is a data-level regularization technique applied during training that linearly interpolates both audio features and labels from pairs of training samples, producing synthetic examples with soft targets. By training on these interpolated samples, the model is discouraged from learning overly sharp or brittle class boundaries and instead learns more stable, continuous decision regions in feature space.

In unbalanced datasets, standard Mixup can unintentionally reinforce majority-class structure due to random pairing. However, imbalance-aware variants (e.g., balanced or targeted Mixup) address this by preferentially generating synthetic examples involving minority-class samples, effectively increasing coverage of underrepresented regions. Unlike label smoothing, which only modifies the loss, Mixup expands the effective training distribution by creating new, semantically plausible samples, making it particularly effective when minority data is scarce.

{% hint style="info" %}
More info on mixup [here](https://arxiv.org/abs/1710.09412)
{% endhint %}

