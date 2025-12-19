# Stage 14 - Sensitivity & Stability

#### **taking:**&#x20;

**learning rate: 0.001**

**dropout: 0.25**\
**hidden units: 1024**<br>

#### **Phase 3: Sensitivity & Threshold Optimization** (2-3 days)

For the best config from Phase 2:

* Run inference at **sensitivity values**: \[0.5, 0.75, 1.0, 1.25, 1.5]
* For each sensitivity, sweep **min\_conf thresholds**: \[0.1, 0.25, 0.5, 0.75, 0.9]
* Plot precision vs recall curves to find your desired operating point

#### **Phase 4: Multi-seed Stability Test** (2-3 days)

Train the final config with **10 seeds** to:

* Measure precision/recall variance
* Select the best-performing checkpoint
* Have backup models if primary fails
