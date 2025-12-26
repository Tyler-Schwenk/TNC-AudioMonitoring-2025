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

**Nyquist theorem** - you need to sample at **2× the highest frequency** you want to capture.

* **4 kHz sample rate** → captures up to **2 kHz** (4 / 2)
* **8 kHz sample rate** → captures up to **4 kHz** (8 / 2) ✓
* **10 kHz sample rate** → captures up to **5 kHz** (10 / 2) - slight buffer for safety

If you recorded at 4 kHz sample rate, you'd only capture 0-2 kHz, which is the over-filtered scenario that gave you 75.9% F1 with terrible precision (62.1%).

You need the **8 kHz minimum** to capture the full 0-4 kHz band that gives you optimal 88.1% F1 performance.

In practice, recorders often use 8 kHz, 11.025 kHz, or 16 kHz as standard sample rates. Going with **8 kHz** perfectly matches your fmax=4000 Hz setting.

## Appended labels

This explores the idea of appending our classifier head other the classifier that birdnet creates. GIVE MORE OF A DESCITPTION

This result sin weaker scored for our target species, but allows for more flexibiliy in the models use.
