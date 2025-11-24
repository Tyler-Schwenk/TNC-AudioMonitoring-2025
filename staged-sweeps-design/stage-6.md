# Stage 6

1. **Balance=True experiments**:
   * All have equal pos/neg counts
   * Subset files are MIXED into the balanced set
   * Cannot directly measure subset impact (they're sampled with manifest files)
2. **Balance=False experiments**:
   * Show full dataset size
   * Subset files are ALL included
   * Better for measuring raw subset contribution



| Comparison               | Experiments                                                                  | What it shows                                  |
| ------------------------ | ---------------------------------------------------------------------------- | ---------------------------------------------- |
| Baseline vs Hard Neg     | stage6\_001 (balance=T, no subsets) vs stage6\_002 (balance=T, +hardneg\_50) | Impact of \~282 hard negatives mixed into 2017 |
| Baseline Unbalanced      | stage6\_037 (balance=F, no subsets) vs stage6\_050 (balance=F, +both)        | Impact of +51 pos, +1401 neg on full dataset   |
| Small vs Top50 Positives | Compare experiments with small vs top50 subsets                              | Quality of curated positives                   |
|                          |                                                                              |                                                |





<table><thead><tr><th width="107">Exp Range</th><th width="97">Seed</th><th width="66">Balance</th><th width="111">Pos Subset</th><th>Neg Subset</th><th width="95">Pos Count</th><th>Neg Count</th></tr></thead><tbody><tr><td>001-003</td><td>123-789</td><td>T</td><td>none</td><td>none</td><td>2017</td><td>2017</td></tr><tr><td>004-006</td><td>123-789</td><td>T</td><td>none</td><td>hardneg_50</td><td>2017</td><td>2017</td></tr><tr><td>007-009</td><td>123-789</td><td>T</td><td>none</td><td>hardneg_99</td><td>2017</td><td>2017</td></tr><tr><td>010-012</td><td>123-789</td><td>T</td><td>small</td><td>none</td><td>2068</td><td>2068</td></tr><tr><td>013-015</td><td>123-789</td><td>T</td><td>small</td><td>hardneg_50</td><td>2068</td><td>2068</td></tr><tr><td>016-018</td><td>123-789</td><td>T</td><td>small</td><td>hardneg_99</td><td>2068</td><td>2068</td></tr><tr><td>019-021</td><td>123-789</td><td>T</td><td>top50</td><td>none</td><td>2067</td><td>2067</td></tr><tr><td>022-024</td><td>123-789</td><td>T</td><td>top50</td><td>hardneg_50</td><td>2067</td><td>2067</td></tr><tr><td>025-027</td><td>123-789</td><td>T</td><td>top50</td><td>hardneg_99</td><td>2067</td><td>2067</td></tr><tr><td>028-030</td><td>123-789</td><td>F</td><td>none</td><td>none</td><td>2017</td><td>8525</td></tr><tr><td>031-033</td><td>123-789</td><td>F</td><td>none</td><td>hardneg_50</td><td>2017</td><td>9926</td></tr><tr><td>034-036</td><td>123-789</td><td>F</td><td>none</td><td>hardneg_99</td><td>2017</td><td>9926</td></tr><tr><td>037-039</td><td>123-789</td><td>F</td><td>small</td><td>none</td><td>2068</td><td>8525</td></tr><tr><td>040-042</td><td>123-789</td><td>F</td><td>small</td><td>hardneg_50</td><td>2068</td><td>9926</td></tr><tr><td>043-045</td><td>123-789</td><td>F</td><td>small</td><td>hardneg_99</td><td>2068</td><td>9926</td></tr><tr><td>046-048</td><td>123-789</td><td>F</td><td>top50</td><td>none</td><td>2067</td><td>8525</td></tr><tr><td>049-051</td><td>123-789</td><td>F</td><td>top50</td><td>hardneg_50</td><td>2067</td><td>9926</td></tr><tr><td>052-054</td><td>123-789</td><td>F</td><td>top50</td><td>hardneg_99</td><td>2067</td><td>9926</td></tr></tbody></table>

<br>



