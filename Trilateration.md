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

三边定位法计算方法：

![](figure/理想三边定位计算方法-1.png)



## LS（least square）

​	基于均方误差最小化来进行模型求解的方法称 为"最小二乘法" (least squqare method)。用LS进行多边定位是为了最大程度地减少估计位置$(\hat{x}_0 ,\hat{y}_0)$与节点的实际位置${(x_0,y_0)}$之间的差异。该方法通常涉及迭代搜索技术，例如梯度下降或牛顿法。为了避免出现局部最小值，LS必须以不同的初始起点多次运算，这会导致计算消耗大。 此外，它很容易受到位置偏移的影响，因为它试图在所有样本（包括那些大偏差样本）上实现全局最优。

![](figure/ls-1.png)

## LMS(Least median squares)

<img src="figure/lms-1.png" style="zoom:75%;" />



## Linear LMS(Linear Least median squares)

<img src="figure/linear lms-1.png" style="zoom:75%;" />

$@Book{Gao2017SLAM, title={视觉SLAM十四讲：从理论到实践}, publisher = {电子工业出版社}, year = {2017}, author = {高翔 and 张涛 and 刘毅 and 颜沁睿}, lang = {zh} }$

## Reference

1. [Trilateration三边测量定位算法](https://www.cnblogs.com/sddai/p/5663463.html)
2. 最小二乘 https://zhuanlan.zhihu.com/p/38128785
3. [最小二乘问题的四种解法——牛顿法，梯度下降法，高斯牛顿法和列文伯格-马夸特法的区别和联系](https://zhuanlan.zhihu.com/p/113946848)
4. 最小二乘法定位（2）——定位算法+仿真程序https://blog.csdn.net/qq_30093417/article/details/88944169
5. 最小二乘法节点定位（1）——小知识：非线性方程线性化https://blog.csdn.net/qq_30093417/article/details/86681364
6. 使用三边定位算法进行室内定位https://blog.csdn.net/huangzhichang13/article/details/76076958
7. 使用三邊定位演算法進行室內定位https://www.itread01.com/content/1546576765.html
8. 采用三边定位算法对未知节点进行估算https://www.cnblogs.com/Aaron12/p/7646841.html
9. [数值分析](http://www.math.ecnu.edu.cn/~jypan/Teaching/NA/index.html)
10. IndoorPos https://codechina.csdn.net/mirrors/megagao/indoorpos?utm_source=csdn_github_accelerator
11. An Algebraic Solution to the Multilateration Problem https://www.researchgate.net/publication/275027725_An_Algebraic_Solution_to_the_Multilateration_Problem
12. matlab优化工具箱 https://ww2.mathworks.cn/help/optim/index.html?s_cid=doc_ftr
13. [梯度下降法(梯度下降法，牛顿法，高斯牛顿法，Levenberg-Marquardt算法)](https://www.cnblogs.com/zhizhan/p/5279672.html)
14. 高斯牛顿算法 https://en.m.wikipedia.org/wiki/Gauss%E2%80%93Newton_algorithm 
15. [MATLAB 高斯牛顿法最优化](https://www.cnblogs.com/ybqjymy/p/13645624.html)
16. [matlab实现高斯牛顿法、Levenberg–Marquardt方法](https://www.cnblogs.com/wsine/p/4634581.html)