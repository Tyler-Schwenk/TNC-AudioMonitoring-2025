# Frequency - Max

### Frequency Filtering (fmin/fmax)

**Goal**

Optimize the frequency range to focus on anuran vocalizations while filtering out irrelevant acoustic energy, improving precision without sacrificing recall.

**Mechanism**

Frequency filtering limits the spectrogram to a specific frequency band during both training and inference. The fmin (minimum frequency) and fmax (maximum frequency) parameters define a bandpass filter applied to the audio before conversion to mel-spectrograms. This reduces the model's acoustic input space, focusing learning on the most relevant frequency ranges for the target species.

Our calls typically exist within the range of 0\~2 kHz. for this reason I attempted training with a maximum frequency of 2 kHz, 4 kHz, and the standard 15 kHz.

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

***

### Shared Configuration

* **Seeds:** 123, 456, 789 (3 replicates each)
* **Quality**: \[high, medium, low]  | **Balance** = False
* **Epochs:** 50 | **Batch size:** 32 | **Threads:** 4
* **Learning rate:** 0.0005 | **Hidden units:** 512
* **Dropout:** 0.25

***

### Effect of Frequency Range on Performance

**Stage 17 (0-15 kHz):** 87.0% F1 | 90.5% precision | 84.3% recall\
**Stage 19 (0-4 kHz):** 88.1% F1 | 88.8% precision | 87.6% recall \
**Stage 19 (0-2 kHz):** 75.9% F1 | 62.1% precision | 98.9% recall

#### Key Findings

**15 kHz (full bandwidth)**

* Strong performance with highest precision but slightly lower recall
* Model must learn to ignore bird calls, insects, and environmental noise above 4 kHz
* More complex decision boundary leads to missed detections

**4 kHz performs well all-around (+1.1% F1 over full bandwidth)**

* Balanced performance: 88.8% precision, 87.6% recall
* Removes high-frequency noise while preserving critical anuran acoustic features

**2 kHz over-filters and collapses precision (-11.1% F1)**

* Near-perfect recall (98.9%) but catastrophic precision loss (62.1%)
* Over-simplifies acoustic space, making model flag any low-frequency signal as positive
* Potentially some important signal being lost above 2 kHz



#### Why 4 kHz Works Best

* **Captures anuran call structure:** Frog vocalizations concentrate energy in 0-4 kHz range, including fundamental frequencies and harmonics
* **Eliminates bird interference:** Most bird calls have energy above 4 kHz, removing a major source of false positives
* **Preserves spectral detail:** Unlike 2 kHz cutoff, 4 kHz retains enough spectral complexity for the model to discriminate between frog species and low-frequency environmental noise
* **Balanced sensitivity:** Model learns to detect frogs without flagging every rumble, wind gust, or mechanical hum

**Net effect:** The 4 kHz filter creates the optimal tradeoff between sensitivity and specificity by focusing the model on the most informative frequency band for anuran detection while removing confounding high-frequency noise.



#### Other considerations

Reducing the frequency can&#x20;

**Nyquist theorem** - you need to sample at **2× the highest frequency** you want to capture.

* **4 kHz sample rate** → captures up to **2 kHz** (4 / 2)
* **8 kHz sample rate** → captures up to **4 kHz** (8 / 2) ✓
* **10 kHz sample rate** → captures up to **5 kHz** (10 / 2) - slight buffer for safety

If you recorded at 4 kHz sample rate, you'd only capture 0-2 kHz, which is the over-filtered scenario that gave you 75.9% F1 with terrible precision (62.1%).

You need the **8 kHz minimum** to capture the full 0-4 kHz band that gives you optimal 88.1% F1 performance.

In practice, recorders often use 8 kHz, 11.025 kHz, or 16 kHz as standard sample rates. Going with **8 kHz** perfectly matches your fmax=4000 Hz setting.<br>
