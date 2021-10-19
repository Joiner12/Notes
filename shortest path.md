# 最短路径(Shortest Path)

## 问题背景

地图中，从某个点(起始点)到另外一个点(终点)找一条最短路径。

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019173346.png)

### 加权有向图

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019173703.png)

- 给定一个加权有向图，找出从起始点s到目标点t的最短路径(shortest path)；
- 路径成本(path cost):路径中每条边的长度和，上图中最短路径为：s→6→3→5→t，路径成本：14 + 18 + 2 + 16 = 50；

**Note:权重是任意数字**

- 不一定是距离 
- 不需要满足三角不等式 
-  例如：航空公司票价

## 算法发展

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019174441.png)



## 应用场景

最短路径是一种广泛有用的问题解决模式。

![](https://gitee.com/RiskyJR/pic-bed/raw/master/20211019174644.png)

## Dijkstra算法

### 单源最短路径



## Reference

1. [15ShortestPaths.key (princeton.edu)](https://www.cs.princeton.edu/~rs/AlgsDS07/15ShortestPaths.pdf)
2. [Dijkstra算法详解 通俗易懂 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/338414118)

