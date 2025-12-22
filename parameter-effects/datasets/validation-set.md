# Validation Set

## Validation set

my custom validation st includes 15% of dates held out from each recorder for use in the BirdNET pipelien using their X training flag (647 positives, 2602 negatives).

Wen not using the custom validation set (validation = false), birdnet will use 20% <- \[TODO CHECK THIS] of the training set of data, INCLUDE BIRDNE DEFINITION.

### Results

Including the validation set showed improvement on unbalanced datasets. below are results from experiments run wit \[high,medium,low] quality data, no balancing, swept across validation sets

Signature,Experiments,Balance,Use Validation,ood.f1\_\_mean,ood.f1\_\_std,ood.precision\_\_mean,ood.precision\_\_std,ood.recall\_\_mean,ood.recall\_\_std 9bfc858c,"stage16\_012, stage16\_028, stage16\_044",No,True,0.864,0.036,0.833,0.1,0.908,0.053 7e00e17d,"stage16\_010, stage16\_026, stage16\_042",No,True,0.824,0.026,0.74,0.078,0.941,0.06 c74e0666,"stage16\_016, stage16\_032, stage16\_048",No,True,0.831,0.081,0.784,0.175,0.915,0.077 b23c3803,"stage16\_014, stage16\_030, stage16\_046",No,True,0.811,0.055,0.717,0.135,0.956,0.07 4ac3abb2,"stage16\_013, stage16\_029, stage16\_045",No,False,0.815,0.109,0.736,0.194,0.952,0.059 58209b07,"stage16\_011, stage16\_027, stage16\_043",No,False,0.776,0.032,0.639,0.044,0.993,0.005 129203e5,"stage16\_009, stage16\_025, stage16\_041",No,False,0.77,0.041,0.71,0.196,0.906,0.159 8d1d706c,"stage16\_015, stage16\_031, stage16\_047",No,False,0.752,0.028,0.604,0.038,0.999,0.002

### Key metrics:

Validation True; OOD F1: 83.25, Std: 2.25 Validation False; OOD F1: 77.82, Std: 2.65

***

With \[high,medium,low] quality data, balancing = true we got: Validation True; OOD F1: 76.35, Std: 3.40 Validation False; OOD F1: 80.25, Std: 2.91

This shows slightly better performance from the Standard birdNET selection, but not enough to be statistically significant given the standard deviation.

Signature,Experiments,Balance,Use Validation,ood.f1\_\_mean,ood.f1\_\_std,ood.precision\_\_mean,ood.precision\_\_std,ood.recall\_\_mean,ood.recall\_\_std 22dd7c35,"stage16\_001, stage16\_017, stage16\_033",Yes,False,0.84,0.013,0.767,0.051,0.931,0.043 19ba8769,"stage16\_002, stage16\_018, stage16\_034",Yes,True,0.814,0.029,0.717,0.065,0.949,0.039 82ec6ada,"stage16\_003, stage16\_019, stage16\_035",Yes,False,0.811,0.04,0.706,0.073,0.959,0.025 88490c45,"stage16\_007, stage16\_023, stage16\_039",Yes,False,0.781,0.026,0.647,0.042,0.987,0.016 9471a601,"stage16\_005, stage16\_021, stage16\_037",Yes,False,0.778,0.072,0.688,0.163,0.935,0.098 97e30fd2,"stage16\_006, stage16\_022, stage16\_038",Yes,True,0.752,0.035,0.606,0.047,0.997,0.005 8f040d0b,"stage16\_008, stage16\_024, stage16\_040",Yes,True,0.748,0.023,0.599,0.03,0.997,0.002 ed295a8f,"stage16\_004, stage16\_020, stage16\_036",Yes,True,0.74,0.097,0.638,0.192,0.939,0.103
