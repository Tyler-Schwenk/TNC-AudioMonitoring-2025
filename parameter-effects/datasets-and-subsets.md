# Positive Datasets & Subsets



Results\
Assuming: no mined hard negatives

| Dataset                       | OOD F1, Std | OOD Precision, Std |
| ----------------------------- | ----------- | ------------------ |
| Full set \[High, Medium, Low] | 77.8 ± 2.4  | 67.5 ± 5.5         |
| \[High, Medium]               | 73.7 ± 2.9  | 87.9 ± 8.3         |
| High quality only             | 68.6 ± 3.9  | 78.8 ± 9.3         |

While adding all of the low quality data significantly improves recall with its ability to identify difficult positive, it decreases precision as it attempts to find RADR in more files. To find a good balance, more granularity was introduced with the positive subsets.

