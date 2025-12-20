# Staged Sweeps Design

### Staged Sweep Strategy

#### Why staged sweeps?

* Keeps experiments interpretable.
* Reveals clear trends (learning curves, overfitting patterns, etc.).
* Matches ML best practices for hyperparameter optimization.
* Allows us to build on prior knowledge step by step.

***

### Parameters tested

#### Seeds:

used multiple times in our pipeline:

* **Data splitting:** Train/val split uses seed for reproducibility
* **Model initialization:** PyTorch/TensorFlow weight initialization
* **Data augmentation:** Mixup, upsampling use seed for randomness

#### Datasets

balance

#### Validation set



#### Hyperparameters



#### Sensitivity



#### mixup, label smoothing,

***

***

#### Expected Insights

* Does larger capacity help or overfit?
* Does dropout prevent collapse?
* Which learning rate regime works best?
* How does batch size interact with learning rate?
* Do augmentation methods (mixup, smoothing, focal loss) add robustness?
* Does synthetic balancing help recall without tanking precision?
* How robust is the model when exposed to noisy/low-quality calls?



***
