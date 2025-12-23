# Balancing

**`balance: true`** - Yes, drops samples from the larger class to match the smaller

**Code (**[**make\_training\_package.py:336-340**](https://vscode-file/vscode-app/c:/Users/tyler/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)**):**

*
*
*
*

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

**When to use:**
