# Hidden Units

**Minimal Benefit, Often Harmful (-1.2% F1 average for added layers)**

**Overall Impact (36 configurations across 108 experiments):**

* Swept across: 0, 128, 512, 1024 hidden units
* All experiments using \[high, medium] quality, balanced training
* Swept across 3 dropout values (0.0, 0.25, 0.5) and 3 learning rates (0.0001, 0.0005, 0.001)

#### Hidden Units Effect

| Hidden Units | Avg F1 | Delta F1 | Precision | Recall |
| ------------ | ------ | -------- | --------- | ------ |
| 0 (Baseline) | 78.2%  | —        | 89.8%     | 70.9%  |
| 128          | 76.2%  | -2.0%    | -0.8%     | -1.1%  |
| 512          | 76.9%  | -1.2%    | -2.8%     | +1.8%  |
| 1024         | 77.0%  | -1.2%    | -0.2%     | -0.4%  |

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

#### Key Takeaways

Adding hidden units to the BirdNET classifier generally reduces performance (-1.2% average), but **interactions exist with dropout and learning rate**. With low/moderate dropout (0.0-0.25), **0 hidden units performs best**. With higher dropout (0.5), 512 units becomes optimal. Similarly, high learning rate (0.001) favors no hidden layers, while mid-range LR (0.0005) allows larger architectures (1024) to match baseline performance. **Best overall: 0 units with 0.25 dropout and 0.001 LR (80.2% F1)**. The baseline architecture is well-tuned for this task - added capacity typically causes overfitting unless paired with aggressive regularization.
