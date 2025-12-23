# Hyperparameters

#### Hidden Units

**Goal**\
Control model capacity to ensure sufficient expressive power to learn RADR call structure without overfitting to training-specific patterns.

**Mechanism**\
The number of hidden units determines the representational capacity of the neural network by controlling the dimensionality of internal feature embeddings. Increasing hidden units allows the model to capture more complex temporal and spectral patterns, while insufficient capacity can lead to underfitting. Excessive capacity, particularly with limited or noisy data, increases the risk of memorization and degraded OOD generalization.

***

#### Dropout

**Goal**\
Reduce overfitting and improve generalization by preventing reliance on any single internal feature representation during training.

**Mechanism**\
Dropout is a regularization technique that randomly deactivates a fraction of hidden units during each training step, forcing the model to learn redundant and distributed representations. This discourages co-adaptation of features and stabilizes decision boundaries, particularly in higher-capacity models or when training data contains correlated noise.

***

#### Learning Rate

**Goal**\
Ensure stable and efficient optimization while avoiding convergence to sharp, brittle minima that harm generalization.

**Mechanism**\
The learning rate controls the step size of parameter updates during optimization. Higher learning rates accelerate convergence but risk instability or overshooting optimal solutions, while lower learning rates improve stability at the cost of slower training and potential entrapment in suboptimal minima. Learning rate interacts strongly with regularization and model capacity, shaping both convergence behavior and final generalization performance.
