# Frequency - Max

### Shared Configuration

* **Seeds:** 123, 456, 789 (3 replicates each)
* **Epochs:** 50 | **Batch size:** 32 | **Threads:** 4
* **Val split:** 0.2 | **Include negatives:** True
* **Learning rate:** 0.0005 | **Hidden units:** 512
* **Dropout:** 0.25 | **Focal loss:** Yes (gamma=2.0, alpha=0.25)
* **Upsampling:** mean, ratio=0.0
* **Frequency range:** 0-2000 Hz (stage19) vs 0-15000 Hz (stage17)
* **Overlap:** 0.0 | **Sensitivity:** 1.0

***

### Effect of Reducing fmax to 2000 Hz

**Massive precision-recall tradeoff favoring recall:**

**Stage 17 (0-15 kHz):** 87.0% F1 | 90.5% precision | 84.3% recall\
**Stage 19 (0-2 kHz):** 75.9% F1 | 62.1% precision | **98.9% recall**

#### Why this happens:

1. **Anuran calls concentrate below 2 kHz** - capturing the core energy of frog vocalizations
2. **Removes high-frequency noise/interference** - eliminates bird calls, insect noise, and environmental artifacts above 2 kHz
3. **Simpler acoustic space** - model sees less spectral complexity, becomes more sensitive to any signal in the 0-2 kHz band
4. **Over-detection penalty** - the model now flags almost everything with energy in 0-2 kHz as a positive, causing many false positives (precision drops 28.4 points)
5. **Near-perfect recall** - captures 98.9% of true anuran calls vs 84.3% at full bandwidth (+14.6 points)

**Net effect:** The 2 kHz filter creates an extremely sensitive detector that rarely misses real calls but generates substantially more false alarms. The F1 score drops 11.1 points due to the precision collapse outweighing the recall gain.
