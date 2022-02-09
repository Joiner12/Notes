# 最短路径(Shortest Path)

## 问题背景

地图中，从某个点(起始点)到另外一个点(终点)找一条最短路径。

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019173346.png)



## 算法发展

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019174441.png)



## 应用场景

最短路径是一种广泛有用的问题解决模式。

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019174644.png)

## 图(Graph)

### 加权有向图

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019173703.png)

- 给定一个加权有向图，找出从起始点s到目标点t的最短路径(shortest path)；
- 路径成本(path cost):路径中每条边的长度和，上图中最短路径为：s→6→3→5→t，路径成本：14 + 18 + 2 + 16 = 50；

**Note:权重是任意数字**

- 不一定是距离 
- 不需要满足三角不等式 
- 例如：航空公司票价

### 图的基本概念

图是用于表示元素对之间的“连接”关系的数据结构。图包括：无向图(Undirected Graph)、有向图（Directed Graph）。

- 这些元素称为节点(Node)。它们代表真实的物体，人员或实体。
- 节点之间的连接称为边缘(Edge)。

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211020222346.png)

图是直接适用于现实世界的情景。例如，我们可以使用图形来建模运输网络，其中节点将代表发送或接收产品的地方，边缘代表连接它们的道路或路径。

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211020222656.png)

### 加权图（Weighted Graphs）

加权图是一种其边缘具有“重量(weight)”或“成本(cost)”。边缘的权重可以表示它连接的一对节点之间的“连接”的距离，时间或任何东西。



## Dijkstra算法

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211020225241.png)

Dijkstra算法将生成从起始节点(source node)-节点0到图表中所有其他节点的最短路径。

节点0到其他节点距离列表：

<img src="https://www.freecodecamp.org/news/content/images/2020/06/image-77.png">

未未访问节点，

<img src="https://www.freecodecamp.org/news/content/images/2020/06/image-78.png">

一旦将所有节点添加到路径中，算法都已完成。





## Reference

1. [15ShortestPaths.key (princeton.edu)](https://www.cs.princeton.edu/~rs/AlgsDS07/15ShortestPaths.pdf)
2. [Dijkstra算法详解 通俗易懂 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/338414118)
3. [Dijkstra’s Algorithm in Python (pythonwife.com)](https://pythonwife.com/dijkstras-algorithm-in-python/)
4. [Dijkstra's Shortest Path Algorithm - A Detailed and Visual Introduction (freecodecamp.org)](https://www.freecodecamp.org/news/dijkstras-shortest-path-algorithm-visual-introduction/)

