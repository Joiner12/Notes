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

### Mode for Classification

在分类问题中，目标变量是分类变量。如前所述，不能对类别变量取平均值。例如，三个预测汽车品牌的平均值是多少？这是不可能说的。您不能对类预测应用平均值。相反，在分类的情况下，您可以采用该模式。模式是最常出现的值。这意味着您计算所有相邻项的类，并保留最常见的类。预测是在相邻要素中最常出现的值。

## Fit kNN in Python Using scikit-learn

虽然从头开始编写算法非常适合学习目的，但在处理机器学习任务时通常不是很实用。在本节中，您将探索 scikit-learn 中使用的 kNN 算法的实现，scikit-learn 是 Python 中最全面的机器学习包之一。

### Splitting Data Into Training and Test Sets for Model Evaluation

在本节中，您将评估鲍鱼 kNN 模型的质量。在前面的部分中，关注更多的是KNN原理，但您现在将有一个更加务实和以结果为导向的视觉。

有多种方法可以评估模型，但最常见的方法是训练-测试拆分。使用训练-测试（train-test split）拆分进行模型评估时，可以将数据集拆分为两部分：

- 训练数据用于拟合模型。对于 kNN，这意味着训练数据将用作邻居。
- 测试数据用于评估模型。这意味着您将对测试数据中每个鲍鱼的环数进行预测，并将这些结果与已知的真实环数进行比较。

您可以使用 scikit-learn 的内置train_test_split() 在 Python 中将数据拆分为训练集和测试集:

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=12345)
```



### Fitting a kNN Regression in scikit-learn to the Abalone Dataset

### Using scikit-learn to Inspect Model Fit

### Plotting the Fit of Your Model

## Tune and Optimize kNN in Python Using scikit-learn

您可以通过多种方式提高预测分数。通过使用数据争用处理（ [data wrangling](https://en.wikipedia.org/wiki/Data_wrangling)）输入数据可以进行一些改进，但在本教程中，重点在于 kNN 算法。接下来，您将了解改进建模管道的算法部分的方法。

### Improving kNN Performances in scikit-learn Using `GridSearchCV`

```python
from sklearn.model_selection import GridSearchCV
parameters = {"n_neighbors": range(1, 50)}
gridsearch = GridSearchCV(KNeighborsRegressor(), parameters)
gridsearch.fit(X_train, y_train)
```



![RSSI-FIT1-0](D:/Code/BlueTooth/pos_bluetooth_matlab/Fingerprinting/Doc/BLE-RSSI-CHAR/RSSI-FIT1-0.png)

<p style="color:#56ff52;font-weight:bold;">关键点</p>

指纹提取总体特征如何通过实际定位过程中局部特征完全反映。

## Reference

1. [The k-Nearest Neighbors (kNN) Algorithm in Python – Real Python](https://realpython.com/knn-python/)
1. [K-Nearest Neighbors (KNN) with Python | DataScience+ (datascienceplus.com)](https://datascienceplus.com/k-nearest-neighbors-knn-with-python/)
1. [sklearn实现KNN分类算法 (biancheng.net)](http://c.biancheng.net/ml_alg/sklearn-knn.html)
1. [Advanced Location-Based Technologies and Services - Google 图书](https://books.google.com.hk/books?id=j3zNBQAAQBAJ&printsec=frontcover&hl=zh-CN#v=onepage&q&f=false)
1. [室内定位系列（三）——位置指纹法的实现（KNN） - rubbninja - 博客园 (cnblogs.com)](https://www.cnblogs.com/rubbninja/p/6134481.html)
1. [MachineLearning/2.k-近邻算法.md at python-2.7 · Atlasgorov/MachineLearning (github.com)](https://github.com/Atlasgorov/MachineLearning/blob/python-2.7/docs/2.k-近邻算法.md)
1. [Python成神之路 - 深度学习-标准化、归一化以及数据处理 (iitter.com)](https://python.iitter.com/other/86511.html)
1. [Classification Using Nearest Neighbors - MATLAB & Simulink - MathWorks 中国](https://ww2.mathworks.cn/help/stats/classification-using-nearest-neighbors.html)
1. [k-nearest neighbor classification - MATLAB (mathworks.com)](https://www.mathworks.com/help/stats/classificationknn.html)