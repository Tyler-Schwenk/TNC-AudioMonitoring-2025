# Datasets

This is created - we will fill this in. it will not require a new sweep. tis inludes the maind high, med, low, ad well as the low subsets. it will validaion shown separate. also look at balanceing



### Positive Datasets:

X total datasets were created, and organized by their quality. First, 3 sets of data were created at the time of data labelling. These were emperically labelled at 'High', 'medium', or 'low' quality based on their spectrograms, as described in [Audio Data Split Design](../audio-data-split-design.md). \
Next, to create finer grained subsets of the large (X files) low quality set, I created 4 subsets of the low quality data. The goal was to create various sizes of subsets of the Highest quality, low quality data. To do this I ran inference on the test set of low quality data using model stage4\_038, which was trained on only medium/high quality data, ensuring this was the first time the low quality data was seen. I then took subsets of the low quality data by selecting the top performing data based on the confidence rating of the positive detections by the model. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted in the 4 folders below:\
small: 51 (5%), medium: 154 (15%), large: 309 (30%), top50: 515 (50%)

### **Hard Negative Mining:** <a href="#evaluation-metrics" id="evaluation-metrics"></a>

I took 20,457 new (entirely outside the train/test/val data) negative audio files from brad's audio (audio recorders 2, 9, and 10) and ran them through inference using model stage3\_046. Then to determine the hardest negative files, I took subsets based on the highest confidence value for RADR fora given audio file. The subsets I took were based on the minimum confidence value for the audio file. so I gathered the following subsets:

* hardneg\_conf\_min\_50 (+1,401 hard negatives at 50% confidence)
* hardneg\_conf\_min\_85 (+981 hard negatives at 85% confidence)
* hardneg\_conf\_min\_99 (+475 hard negatives at 99% confidence)

### Custom Validation Set:

my custom validation st includes 15% of dates held out from each recorder for use in the BirdNET pipelien using their X training flag (647 positives, 2602 negatives).

Wen not using the custom validation set (validation = false), birdnet will use 20% <- \[TODO CHECK THIS] of the training set of data, INCLUDE BIRDNE DEFINITION.

### Balancing:

Balance = True: drops samples from the larger class to match the smaller. In my case the negative class is always larger, and will be reduced to match the size of the positive class.

**What happens:**

1. **After filtering** (quality, call\_type, subsets), you have e.g., 800 positives, 3000 negatives
2. **`balance: false`** → Uses all 800 pos + 3000 neg (imbalanced)
3. **`balance: true`** → Finds [min(800, 3000) = 800](https://vscode-file/vscode-app/c:/Users/tyler/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html), randomly samples 800 from each class
   * Final: 800 pos + 800 neg (balanced)
   * The 2200 extra negatives are dropped

**Sampling is deterministic:**

* Uses the experiment's [seed](https://vscode-file/vscode-app/c:/Users/tyler/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) value
* Same seed = same files selected every time
* Different seeds get different random samples from the larger class
