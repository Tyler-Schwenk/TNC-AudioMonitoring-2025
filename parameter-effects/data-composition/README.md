# Data Composition

### Positive Datasets:

7 total datasets were created, and organized by their quality. First, 3 sets of data were created at the time of data labelling. These were emperically labelled at 'High', 'medium', or 'low' quality based on their spectrograms, as described in [Audio Data Split Design](../../audio-data-split-design.md). \
Next, to create finer grained subsets of the large (X files) low quality set, I created 4 subsets of the low quality data. The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted in the 4 folders below:\
small: 51 (5%), medium: 154 (15%), large: 309 (30%), top50: 515 (50%)

### **Hard Negative Mining:** <a href="#evaluation-metrics" id="evaluation-metrics"></a>

I took 20,457 new (entirely outside the train/test/val data) negative audio files from brad's audio (audio recorders 2, 9, and 10) and ran them through inference using model stage3\_046. Then to determine the hardest negative files, I took subsets based on the highest confidence value for RADR fora given audio file. The subsets I took were based on the minimum confidence value for the audio file. so I gathered the following subsets:

* hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
* hardneg\_conf\_min\_85 (+981 hard negatives at 85% confidence)
* hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

### Custom Validation Set:

My custom validation set includes 15% of dates held out from each recorder for use in the BirdNET pipeline (647 positives, 2602 negatives).

When not using the custom validation set (validation = false), BirdNET will use 20% of the training set of data as validation data.

### Balancing:

Applied during my custom pipeline, Balance = True drops samples from the larger class to match the smaller one. In my case the negative class is always larger, and will be reduced to match the size of the positive class.

Balancing is applied after filtering (by quality, call type, subsets) by taking a random, deterministic sampling of both sets of data, equal to the size of the smaller set of data. Sampling uses the experiment's seed value to enforce deterministic randomness.
