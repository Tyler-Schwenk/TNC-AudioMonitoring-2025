# Separate Call Types

The California red-legged frog has two distinct call types, one of shorter repeating 'grunts', and another, less common call type of a longer, lower 'growl' (often preceded by grunts). Examples can be found at [Audio Data Examples](../audio-data-split-design/audio-data-examples.md)

It is possible that a model could perform better if trained to focus on each call type as separate classes, rather than both combined as "RADR". This could lead to more focused classes. It would, however, require deviating from a binary classifier, which could reduce overall performance.

Due to the need to curate separate sets of data, and adjust the design of the experiments and model infrastructure, I consider it out of the scope of this current contract.&#x20;

A brief evaluation was conducted on our data, and results are found at [Stage 7](../staged-sweeps-design/stage-7.md)
