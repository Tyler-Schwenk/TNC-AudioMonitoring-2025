# Human In The Loop

Talk abot how tis was explored, but found to be less effective given our stongly labelled data. but perhaps it would work well in the future as new data comes in from the field

using: [https://colab.research.google.com/drive/1gPBu2fyw6aoT-zxXFk15I2GObfMRNHUq#scrollTo=2qHKlHuuJrEp](https://colab.research.google.com/drive/1gPBu2fyw6aoT-zxXFk15I2GObfMRNHUq#scrollTo=2qHKlHuuJrEp)

* BirdNET supports a custom classifier interface (train → output → `--classifier`)
* The CCAI / Perch method trains _just_ the classification head on top of the same embedding backbone
* The embedding dimensions, input audio segmentation, and architecture assumptions match BirdNET’s setup
