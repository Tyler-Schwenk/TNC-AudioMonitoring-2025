# Positive Datasets & Subsets

Results\
Assuming: no mined hard negatives

| Dataset              | OOD F1, Std | OOD Precision, Std | OOD Recall, Std |
| -------------------- | ----------- | ------------------ | --------------- |
| \[High, Medium, Low] | 77.8 ± 2.4  | 67.5 ± 5.5         | 95.3 ± 3.6      |
| \[High, Medium]      | 73.7 ± 2.9  | 87.9 ± 8.3         | 70.2 ± 7.7      |
| \[High]              | 68.6 ± 3.9  | 78.8 ± 9.3         | 67.9 ± 7.0      |

While adding all of the low quality data significantly improves recall with its ability to identify difficult positive, it decreases precision as it attempts to find RADR in more files. To find a good balance, more granularity was introduced with the positive subsets.



The data here is sythesized from [stage 6](../staged-sweeps-design/stage-6-data-composition.md) and [stage 9](../staged-sweeps-design/stage-9.md)

