# Reduced Max-Frequency Models

## Overview

Our calls typically exist within the range of 0\~2 kHz. For this reason I attempted training with a reduced (bandpass filter) maximum frequency of 2 kHz, 4 kHz.

This showed promise, with comparable metrics, its ability to work with data at reduced file size could have practical implications.

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

## Performance

A full evaluation can be found under Parameter Effects at [Frequency - Max](../parameter-effects/frequency-max.md).

## File Size Reduction

Due to the Nyquist theorem, we need to sample at 2× the highest frequency used in bandpass filtering. This means we would record at a sample rate of 8 kHz, rather than the current 48 kHz.

This gives a reduction of 16.7% of the original size.

Example:

* 1-minute WAV at 48 kHz, 16-bit mono: \~5.5 MB
* 1-minute WAV at 8 kHz, 16-bit mono: \~0.9 MB

In context:

* 432 files/night at 48 kHz: \~2.4 GB/night
* 432 files/night at 8 kHz: \~0.4 GB/night

This could significantly improve storage capabilities of devices in the field, and reduce processing times at the workstation.

