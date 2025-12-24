# Hidden Units

**Overall Impact (36 configurations across 108 experiments):**

* Swept across: 0, 128, 512, 1024 hidden units
* All experiments using \[high, medium] quality, balanced training
* Swept across 3 dropout values (0.0, 0.25, 0.5) and 3 learning rates (0.0001, 0.0005, 0.001)

<figure><img src="../../.gitbook/assets/hidden units.png" alt=""><figcaption></figcaption></figure>

#### Interaction with Dropout

| Dropout | H=0   | H=128 | H=512 | H=1024 | **Best** |
| ------- | ----- | ----- | ----- | ------ | -------- |
| 0.0     | 79.3% | 74.5% | 77.7% | 75.3%  | **0**    |
| 0.25    | 80.2% | 77.5% | 76.0% | 80.1%  | **0**    |
| 0.5     | 75.1% | 76.7% | 77.1% | 75.7%  | **512**  |

#### Interaction with Learning Rate

| LR     | H=0   | H=128 | H=512 | H=1024 | **Best** |
| ------ | ----- | ----- | ----- | ------ | -------- |
| 0.0001 | 75.1% | 76.0% | 76.0% | 74.3%  | **512**  |
| 0.0005 | 79.2% | 75.5% | 76.5% | 79.2%  | **1024** |
| 0.001  | 80.2% | 77.1% | 78.3% | 77.5%  | **0**    |

No strong correlation can be drawn between introduced hidden units and any key metrics, including its interaction with other hyperparameters. There is a tendency for the standard deviation to increase with the introduction of hidden units, and thus it will likely not be included in the final model to prevent the introduction of instability.
