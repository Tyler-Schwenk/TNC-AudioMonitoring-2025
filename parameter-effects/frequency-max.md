# Frequency - Max

## **Goal**

Optimize the frequency range to focus on target vocalizations while filtering out irrelevant acoustic energy, improving precision without sacrificing recall. Reduce the total file size of audio recordings.

**Mechanism**

Frequency filtering limits the spectrogram to a specific frequency band during both training and inference. The f-min (minimum frequency) and f-max (maximum frequency) parameters define a bandpass filter applied to the audio before conversion to mel-spectrograms. This reduces the model's acoustic input space, focusing learning on the most relevant frequency ranges for the target species.

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

## Evaluation

**Stage 17 (0-15 kHz):** 87.0% F1 | 90.5% precision | 84.3% recall\
**Stage 19 (0-4 kHz):** 88.1% F1 | 88.8% precision | 87.6% recall \
**Stage 19 (0-2 kHz):** 75.9% F1 | 62.1% precision | 98.9% recall

#### Key Findings

**15 kHz (full bandwidth)**

* Strong performance with highest precision but slightly lower recall
* Model must learn to ignore bird calls, insects, and environmental noise above 4 kHz

**4 kHz performs well all-around (+1.1% F1 over full bandwidth)**

* Balanced performance: 88.8% precision, 87.6% recall
* Removes high-frequency noise while preserving critical anuran acoustic features

**2 kHz over-filters and collapses precision (-11.1% F1)**

* Near-perfect recall (98.9%) but catastrophic precision loss (62.1%)
* Over-simplifies acoustic space, making model flag any low-frequency signal as positive
* Potentially some important signal being lost above 2 kHz

### Limitations

These reduced F-max files were created via a bandpass filter over the original, full bandwidth recordings. It is possible these results would not translate to audio files natively recorded at a reduced frequency.

We also only performed 3 experiments per configuration, more robust testing would be required for a solid conclusion.

<br>
