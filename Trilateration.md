# Trilateration

## 问题描述

​	分布均匀的无线传感器网络由一组节点组成，包括锚节点(anchor nodes)和未知节点(unknown nodes)。每个节点都配备有信号收发器，当它们之间的欧式距离(Euclidean distance)小于特定的范围，可以进行通信。每个节点都可以通过某些测距技术（例如TDOA，RSSI或DV-HOP）测量到其他节点的距离。观测距离结果用公式（1）表示，其中${N(0,VD)}$ 是高斯白噪声。
$$
\begin{align}
& d_{measured} = d_{deal} + noise,noisen  \~  N(0,VD)
\end{align}
$$
​	假定一坐标为${(x_0,y_0)}$ 的未知结点 接收到N个信号 ${(x_1,y_1,d_1),...,(x_2,y_2,d_N)}$，理想条件下，有如下公式：
$$
\begin{align}
(x_1-x_0)^2 &+ (y_1-y_0)^2 = d_1^2 \\
(x_2-x_0)^2 &+ (y_2-y_0)^2 = d_2^2 \\
&.\\&.\\
(x_N-x_0)^2 &+ (y_N-y_0)^2 = d_N^2 \\
\end{align}
$$


如果$N \geq 3$ ，且锚节点不在同一条直线上，则能通过求解任意三个公式得到${(x_0,y_0)}$ 的值。

## 经典三边测距法（classical trilateration algorithm）

三边测距法中，二维平面中的解是以三个锚点为中心的三个圆的交点。如图一，实际上，所有以${(x_i,x_i)}$ 为圆心，以${d_i}$ 为半径的圆的交点为${(x_0,y_0)}$。然后，真实环境中， 这N个圆可能并不是相交于一个点，因此通常使用公式（3）中描述的目标函数来最小化未知节点的估计位置与实际位置之间的差异。 该方法即是最小二乘经典三边测距算法。



<img src="figure/三边测距示意图-1.png" style="zoom:50%;" />

在正常条件中使用LS（least square）进行多边测试效果不错。 

<img src="figure/三边测距示意图-2.png" style="zoom:60%;" />

但是如果存在较大噪声干扰下， 坐标估计值与真实坐标偏差会受到较大影响；

## LS（least square）

​	用LS进行多边定位是为了最大程度地减少估计位置$(\hat{x}_0 ,\hat{y}_0)$与节点的实际位置${(x_0,y_0)}$之间的差异。该方法通常涉及迭代搜索技术，例如梯度下降或牛顿法。为了避免出现局部最小值，LS必须以不同的初始起点多次运算，这会导致计算消耗大。 此外，它很容易受到位置偏移的影响，因为它试图在所有样本（包括那些大偏差样本）上实现全局最优。

![](figure/ls-1.png)

## LMS(Least median squares)

<img src="figure/lms-1.png" style="zoom:75%;" />



## Linear LMS(Linear Least median squares)

<img src="figure/linear lms-1.png" style="zoom:75%;" />



## Reference

1.https://www.cnblogs.com/sddai/p/5663463.html

2.最小二乘 https://zhuanlan.zhihu.com/p/38128785