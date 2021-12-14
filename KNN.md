与其他机器学习算法（machine learning algorithms）相比，kNN（k-Nearest Neighbors ） 算法有点不典型。 正如您之前看到的，每个机器学习模型都有其需要估计的特定公式。 kNN算法的特殊性在于，这个公式不是在拟合的时候计算的，而是在预测的时候计算的。 大多数其他模型并非如此。当一个新数据点到达时，kNN 算法，顾名思义，将首先寻找这个新数据点的最近邻居。 然后它采用这些邻居的值并将它们用作新数据点的预测。 kNN 算法基于这样一个概念，即您可以根据相邻数据点的特征来预测数据点的特征。 在某些情况下，这种预测方法可能会成功，而在其他情况下则可能不会。 接下来，您将了解数据点“最近”的数学描述以及将多个邻居组合成一个预测的方法。 



### Define “Nearest” Using a Mathematical Definition of Distance

```python
import numpy as np
a = np.array([2, 2])
b = np.array([4, 4])
np.linalg.norm(a - b)
```

### Find the `k` Nearest Neighbors



### Voting or Averaging of Multiple Neighbors

### Average for Regression

## Fit kNN in Python Using scikit-learn

### Splitting Data Into Training and Test Sets for Model Evaluation

### Fitting a kNN Regression in scikit-learn to the Abalone Dataset

### Using scikit-learn to Inspect Model Fit

### Plotting the Fit of Your Model



## Reference

1. [The k-Nearest Neighbors (kNN) Algorithm in Python – Real Python](https://realpython.com/knn-python/)