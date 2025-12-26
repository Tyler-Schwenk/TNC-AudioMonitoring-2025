# Introduction

## Introduction

The goal of:\
contract stated: "Test and determine optimal BirdNET Analyzer settings to maximize daily detection precision and reduce verification&#x20;workload."

to the end of:\
monitioring CRLF recovery in reintroduced sites - localize location to search for egg masses/ juveniles.

### Call overview:

grut vs growl, examples, hig vs medium vs low quality data explain that we are attempting to identify all of these - including low quality and growls in test set

### entry point:

we had a previous model, which will be referred to as ""

## Methodology:

We began by generating a labeled audio data set of total: 21,887 3-second files (7,887 poitive, 14,000 negative). link to more info

BirdNET description - talk baout how this works, maybe show the coo graphic of hw we use their embeddings with our custom classiier head over top. maybe even include a gif/video visualization. maybe include fancy impressive metrics like the 8 million parameters.

### Training

All parameters were swept in stages, varying one parameter at a time while holding thers constant. When applicable multiple parameters were varied in a fctorial sweep to detemine interactions between parameters (such as hyper paremetrs). Each configuration was duplicated 3 times, varying the seed for each run to ensure stability, as described below:

These were trained within a custom training pipeline i created, linked [here](https://github.com/Tyler-Schwenk/BirdNET-CustomClassifierSuite). This allowed me to implement custom parameters not supported by birdnet, as well as train in sweeps of 100 models at a time, automating file selection, model training, inference, and evalutaiton on my iid and ood datasets.

#### Seeds

Correct. Seeds are **ONLY** used for:

1. **Data selection** - deterministically shuffling and sampling which audio files go into training/validation packages

**Yes, absolutely.** Even if seeds did nothing for data selection, training multiple models is crucial because neural network training is **inherently non-deterministic**. Since your pipeline doesn't seed BirdNET-Analyzer's training, each run will have:

* **Random weight initialization** - starting point affects final convergence
* **Random mini-batch shuffling** during training epochs
* **Potential GPU non-determinism** - floating-point operations aren't always deterministic
* **Optimizer stochasticity** - SGD/Adam have random elements

### parameters explored (link to heir pages):

if aplicable include the birdnet flag definitions form theirdocs

#### Datasets

Varations of High, Medium, and low also subsets of low data inclusion

Custom Validation dataset

Balancing (True/False)

#### Data Augmentation

#### Regularization techniques

Mixup -

Label smoothing -

#### Hyperparameters
