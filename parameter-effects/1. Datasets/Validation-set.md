# Validaiton set


my custom validaiton st includes 15% of dates held out from each recorder for use in the BirdNET pipelien using their X training flag (647 positives, 2602 negatives). 

Wen not using the custom validation set (validation = false), birdnet will use 20% <- [TODO CHECK THIS] of the trianing set of data,   INCLUDE BIRDNE DEFINITION.


## Results

Including the validation set showed improvement on unbalanced datasets. below are results from experiments run wit [high,medium,low] quality data, no balancing, swept across validation sets

Signature,Experiments,Balance,Use Validation,ood.f1__mean,ood.f1__std,ood.precision__mean,ood.precision__std,ood.recall__mean,ood.recall__std
9bfc858c,"stage16_012, stage16_028, stage16_044",No,True,0.864,0.036,0.833,0.1,0.908,0.053
7e00e17d,"stage16_010, stage16_026, stage16_042",No,True,0.824,0.026,0.74,0.078,0.941,0.06
c74e0666,"stage16_016, stage16_032, stage16_048",No,True,0.831,0.081,0.784,0.175,0.915,0.077
b23c3803,"stage16_014, stage16_030, stage16_046",No,True,0.811,0.055,0.717,0.135,0.956,0.07
4ac3abb2,"stage16_013, stage16_029, stage16_045",No,False,0.815,0.109,0.736,0.194,0.952,0.059
58209b07,"stage16_011, stage16_027, stage16_043",No,False,0.776,0.032,0.639,0.044,0.993,0.005
129203e5,"stage16_009, stage16_025, stage16_041",No,False,0.77,0.041,0.71,0.196,0.906,0.159
8d1d706c,"stage16_015, stage16_031, stage16_047",No,False,0.752,0.028,0.604,0.038,0.999,0.002


{% file src="../.gitbook/assets/chart_Use_Validation_OOD_F1.svg %}

## Key metrics:

Validation True; OOD F1: 83.25, Std: 2.25
Validation False; OOD F1: 77.82, Std: 2.65

----------------


With [high,medium,low] quality data, balancing = true we got:
Validation True; OOD F1: 76.35, Std: 3.40
Validation False; OOD F1: 80.25, Std: 2.91

This shows slightly better performance from the Standard birdNET selection, but not enough to be statistically significant given the standard deviation.

Signature,Experiments,Balance,Use Validation,ood.f1__mean,ood.f1__std,ood.precision__mean,ood.precision__std,ood.recall__mean,ood.recall__std
22dd7c35,"stage16_001, stage16_017, stage16_033",Yes,False,0.84,0.013,0.767,0.051,0.931,0.043
19ba8769,"stage16_002, stage16_018, stage16_034",Yes,True,0.814,0.029,0.717,0.065,0.949,0.039
82ec6ada,"stage16_003, stage16_019, stage16_035",Yes,False,0.811,0.04,0.706,0.073,0.959,0.025
88490c45,"stage16_007, stage16_023, stage16_039",Yes,False,0.781,0.026,0.647,0.042,0.987,0.016
9471a601,"stage16_005, stage16_021, stage16_037",Yes,False,0.778,0.072,0.688,0.163,0.935,0.098
97e30fd2,"stage16_006, stage16_022, stage16_038",Yes,True,0.752,0.035,0.606,0.047,0.997,0.005
8f040d0b,"stage16_008, stage16_024, stage16_040",Yes,True,0.748,0.023,0.599,0.03,0.997,0.002
ed295a8f,"stage16_004, stage16_020, stage16_036",Yes,True,0.74,0.097,0.638,0.192,0.939,0.103
