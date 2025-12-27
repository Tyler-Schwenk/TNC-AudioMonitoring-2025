# Appended labels

## Overview

All of my models thus far have used the 'replace' save mode within BirdNET, which takes the BirdNET embeddings, and replaces their classifier head with my custom classifier head (a binary classifier). This section explores the idea of using the 'append' save mode, which appends my custom classifier head on top of the standard classifier that BirdNET creates over their embeddings.&#x20;

This append mode allows us to retain their 6,000+ classes with the addition of our custom RADR class.

### Results

Overall this has shown to be a weaker model, due to its less targeted classification - particularly as we cannot use binary classification techniques.&#x20;

In our current use case we do not have need for this kind of classifier, as RADR and Bullfrog calling is separated temporally, allowing us to search for only one frog at a time.

Full results at [Stage 8](../staged-sweeps-design/stage-8.md)
