# other methodologies explored

We initiated preliminary explorations into other training techniques to identify potential future areas for develoment

## Human In the Loop (HITL):

Talk abot how tis was explored, but found to be less effective given our stongly labelled data. but perhaps it would work well in the future as new data comes in from the field

using: [https://colab.research.google.com/drive/1gPBu2fyw6aoT-zxXFk15I2GObfMRNHUq#scrollTo=2qHKlHuuJrEp](https://colab.research.google.com/drive/1gPBu2fyw6aoT-zxXFk15I2GObfMRNHUq#scrollTo=2qHKlHuuJrEp)

* BirdNET supports a custom classifier interface (train → output → `--classifier`)
* The CCAI / Perch method trains _just_ the classification head on top of the same embedding backbone
* The embedding dimensions, input audio segmentation, and architecture assumptions match BirdNET’s setup

## Focus on specific call type

the California red-legged frog has two distinct call types, one of shorter repeating 'grunts', and another, less common call type of a longer, lower 'growl' (often preceded by grunts).

In this experimental stage, I briefly explored the idea of training the model to identify specific types of the California red-legged frog's call, rather than both as the same label.

This would take a significant amount of time to make a new experiment structure and testing dataset around each call type, and I consider it out of the scope of this current contract. It is an idea that could be explored in the future though

## Reduced Frequency Models

This showed promise. While it has not shown improvement in absolute performance metrics, its ability to work with data at reduced file size could have practical implications given its comparable metrics.

## Appended labels

This explores the idea of appending our classifier head other the classifier that birdnet creates. GIVE MORE OF A DESCITPTION

This result sin weaker scored for our target species, but allows for more flexibiliy in the models use.
