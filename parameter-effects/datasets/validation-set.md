# Validation Set

### Overview

Below are results from experiments run with \[high,medium,low] quality data, swept across validation sets and balancing. Validation = True uses my custom validation set, false uses the default BirdNET configuration of 20% of the training data.

### Key metrics:

With Balancing = False:

* Validation True; OOD F1: 83.25, Std: 2.25&#x20;
* Validation False; OOD F1: 77.82, Std: 2.65

With balancing = True:&#x20;

* Validation True; OOD F1: 76.35, Std: 3.40&#x20;
* Validation False; OOD F1: 80.25, Std: 2.91

Validation selection improves mean OOD F1 in unbalanced configurations but degrades OOD performance when class balancing is applied, indicating a strong interaction between validation usage and balancing. As a result, validation-based selection cannot be treated as a universally beneficial strategy over BirdNET's standard distribution for OOD generalization.

***

### Full Data Used

#### OOD Performance Summary - No Balancing

| Experiments                              | Balance | Use Validation | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) |
| ---------------------------------------- | ------- | -------------- | ------------------- | -------------------------- | ----------------------- |
| stage16\_012, stage16\_028, stage16\_044 | No      | True           | 0.864 ± 0.036       | 0.833 ± 0.100              | 0.908 ± 0.053           |
| stage16\_010, stage16\_026, stage16\_042 | No      | True           | 0.824 ± 0.026       | 0.740 ± 0.078              | 0.941 ± 0.060           |
| stage16\_016, stage16\_032, stage16\_048 | No      | True           | 0.831 ± 0.081       | 0.784 ± 0.175              | 0.915 ± 0.077           |
| stage16\_014, stage16\_030, stage16\_046 | No      | True           | 0.811 ± 0.055       | 0.717 ± 0.135              | 0.956 ± 0.070           |
| stage16\_013, stage16\_029, stage16\_045 | No      | False          | 0.815 ± 0.109       | 0.736 ± 0.194              | 0.952 ± 0.059           |
| stage16\_011, stage16\_027, stage16\_043 | No      | False          | 0.776 ± 0.032       | 0.639 ± 0.044              | 0.993 ± 0.005           |
| stage16\_009, stage16\_025, stage16\_041 | No      | False          | 0.770 ± 0.041       | 0.710 ± 0.196              | 0.906 ± 0.159           |
| stage16\_015, stage16\_031, stage16\_047 | No      | False          | 0.752 ± 0.028       | 0.604 ± 0.038              | 0.999 ± 0.002           |

#### OOD Performance Summary - With Balancing

| Experiments                              | Balance | Use Validation | OOD F1 (mean ± std) | OOD Precision (mean ± std) | OOD Recall (mean ± std) |
| ---------------------------------------- | ------- | -------------- | ------------------- | -------------------------- | ----------------------- |
| stage16\_001, stage16\_017, stage16\_033 | Yes     | False          | 0.840 ± 0.013       | 0.767 ± 0.051              | 0.931 ± 0.043           |
| stage16\_002, stage16\_018, stage16\_034 | Yes     | True           | 0.814 ± 0.029       | 0.717 ± 0.065              | 0.949 ± 0.039           |
| stage16\_003, stage16\_019, stage16\_035 | Yes     | False          | 0.811 ± 0.040       | 0.706 ± 0.073              | 0.959 ± 0.025           |
| stage16\_007, stage16\_023, stage16\_039 | Yes     | False          | 0.781 ± 0.026       | 0.647 ± 0.042              | 0.987 ± 0.016           |
| stage16\_005, stage16\_021, stage16\_037 | Yes     | False          | 0.778 ± 0.072       | 0.688 ± 0.163              | 0.935 ± 0.098           |
| stage16\_006, stage16\_022, stage16\_038 | Yes     | True           | 0.752 ± 0.035       | 0.606 ± 0.047              | 0.997 ± 0.005           |
| stage16\_008, stage16\_024, stage16\_040 | Yes     | True           | 0.748 ± 0.023       | 0.599 ± 0.030              | 0.997 ± 0.002           |
| stage16\_004, stage16\_020, stage16\_036 | Yes     | True           | 0.740 ± 0.097       | 0.638 ± 0.192              | 0.939 ± 0.103           |
