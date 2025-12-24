# Frequency - Max

### Frequency Filtering (fmin/fmax)

**Goal**

Optimize the frequency range to focus on anuran vocalizations while filtering out irrelevant acoustic energy, improving precision without sacrificing recall.

**Mechanism**

Frequency filtering limits the spectrogram to a specific frequency band during both training and inference. The fmin (minimum frequency) and fmax (maximum frequency) parameters define a bandpass filter applied to the audio before conversion to mel-spectrograms. This reduces the model's acoustic input space, focusing learning on the most relevant frequency ranges for the target species.

For anuran calls, which typically contain energy below 4 kHz, filtering out higher frequencies removes bird vocalizations, insect noise, and environmental artifacts that could confuse the classifier. However, filtering too aggressively (e.g., 0-2 kHz) can over-simplify the acoustic space, causing the model to become overly sensitive to any low-frequency signal.

***

### Shared Configuration

* **Seeds:** 123, 456, 789 (3 replicates each)
* **Epochs:** 50 | **Batch size:** 32 | **Threads:** 4
* **Val split:** 0.2 | **Include negatives:** True
* **Learning rate:** 0.0005 | **Hidden units:** 512
* **Dropout:** 0.25 | **Focal loss:** Yes (gamma=2.0, alpha=0.25)
* **Upsampling:** mean, ratio=0.0
* **Overlap:** 0.0 | **Sensitivity:** 1.0

***

### Effect of Frequency Range on Performance

**Stage 17 (0-15 kHz, full bandwidth):** 87.0% F1 | 90.5% precision | 84.3% recall\
**Stage 19 (0-4 kHz, optimal):** 88.1% F1 | 88.8% precision | 87.6% recall ⭐ **BEST**\
**Stage 19 (0-2 kHz, over-filtered):** 75.9% F1 | 62.1% precision | 98.9% recall

#### Key Findings

1. **4 kHz is optimal (+1.1% F1 over full bandwidth)**
   * Balanced performance: 88.8% precision, 87.6% recall
   * Removes high-frequency noise while preserving critical anuran acoustic features
   * Superior to both full bandwidth (15 kHz) and over-aggressive filtering (2 kHz)
2. **2 kHz over-filters and collapses precision (-11.1% F1)**
   * Near-perfect recall (98.9%) but catastrophic precision loss (62.1%)
   * Over-simplifies acoustic space, making model flag any low-frequency signal as positive
   * Generates 28.4 percentage points more false positives than full bandwidth
   * Model becomes too sensitive: "everything below 2 kHz looks like a frog"
3. **15 kHz (full bandwidth) includes unnecessary noise**
   * Strong performance but slightly lower recall (84.3% vs 87.6% at 4 kHz)
   * Model must learn to ignore bird calls, insects, and environmental noise above 4 kHz
   * More complex decision boundary leads to missed detections

#### Why 4 kHz Works Best

* **Captures anuran call structure:** Frog vocalizations concentrate energy in 0-4 kHz range, including fundamental frequencies and harmonics
* **Eliminates bird interference:** Most bird calls have energy above 4 kHz, removing a major source of false positives
* **Preserves spectral detail:** Unlike 2 kHz cutoff, 4 kHz retains enough spectral complexity for the model to discriminate between frog species and low-frequency environmental noise
* **Balanced sensitivity:** Model learns to detect frogs without flagging every rumble, wind gust, or mechanical hum

**Net effect:** The 4 kHz filter creates the optimal tradeoff between sensitivity and specificity by focusing the model on the most informative frequency band for anuran detection while removing confounding high-frequency noise.<br>
