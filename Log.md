## Log📍

1.continue  & break & return✔

2.try catch ✔

3.matlab 为程序添加帮助（注释）✔

4.dbscan聚类算法

5.命令行

```
--global 
-g 
具体使用
```

## Log:pineapple:

1.蓝牙通信采集数据特征；

2.kaggle室内定位https://mp.weixin.qq.com/s/bSSXrfeneHaLta_FGsIp7A



## Log:one:

1.git下载单个文件 https://www.zhihu.com/question/25369412

2.matlab参数检查方式

3.matlab绘图类继承关系（获取各个属性）√

```matlab
get
set
```

4.scatter colormap sz c

5.why matlab figure uglier than matplot

## Log:2nd_place_medal:



# Painting in PyQt5

#### PyQt之窗口绘图类控件(QPainter、Qpen、QBrush)

PyQt5绘画系统能够呈现矢量图形，图像和轮廓基于字体的文本。当我们想要更改或增强现有的小部件，或者从头开始创建自定义小部件时，应用程序中需要绘画。 要进行绘制，我们使用PyQt5工具包提供的绘制API。 



## QPainter

 QPainter在小部件和其他绘画设备上执行低级绘画。 它可以绘制从简单的线条到复杂形状的所有内容。

## The paintEvent method

绘画是在paintEvent方法中完成的。 绘画代码位于QPainter对象的begin和end方法之间。 它在小部件和其他绘画设备上执行低级绘画。 

## PyQt5 draw text

#### drawText

...

#### drawPoints

...



颜色是代表红色，绿色和蓝色（RGB）强度值的组合的对象。 有效的RGB值在0到255之间。我们可以通过多种方式定义颜色。 最常见的是RGB十进制值或十六进制值。 我们还可以使用代表红色，绿色，蓝色和Alpha的RGBA值。 在这里，我们添加了一些有关透明度的额外信息。 Alpha值为255表示完全不透明，0表示完全透明，例如 颜色不可见。 



## PyQt5 draw points



https://zetcode.com/gui/pyqt5/painting/

开发文档 https://blog.csdn.net/wowocpp/article/details/105199080

开发文档-1https://www.riverbankcomputing.com/static/Docs/PyQt5/sip-classes.html

https://zetcode.com/gui/pyqt5/painting/

## Log:kissing:

1. 最小二乘法https://zhuanlan.zhihu.com/p/38128785
2. gauss filter 
3. matlab画阴影面 



# Gaussian Filtering

高斯滤波器是一种线性滤波器，能够有效的抑制噪声，平滑图像。其作用原理和均值滤波器类似—窗口内数据的线性组合之和做为输出。其窗口模板的系数和均值滤波器不同，均值滤波器的模板系数都是相同的为$1/n$ ，n为窗口大小；而高斯滤波器的模板系数，则随着距离模板中心的增大而系数减小。所以，高斯滤波器相比于均值滤波器对图像个模糊程度较小。

一维高斯函数：



## 高斯函数：

高斯函数的标准偏差在其行为中起着重要作用。

https://www.cnblogs.com/wangguchangqing/p/6407717.html

## Log:point_up_2:

1. 修改时间格式https://blog.walterlv.com/ime/2017/09/18/date-time-format-using-microsoft-pinyin.html

```python
# date
%yyyy%-%MM%-%dd% %HH%:%mm%

# 日期
%yyyy%-%MM%-%dd%

# 时间
%HH%:%mm%
 
```

2. 翻译并实现三边定位算法

https://www.cnblogs.com/sddai/p/5663463.html

[Calculating the intersection area of 3+ circles](http://www.benfrederickson.com/calculating-the-intersection-of-3-or-more-circles/)

基于rssi的三点定位算法

3. bash启动程序详细
4. excel数据处理—甘特图 √
5. git 同时输入两条指令 √



## Log:four:

1. 最小二乘求解

https://zhuanlan.zhihu.com/p/113946848

2.  matlab绘图配色标准
3. 专业书：kindle

https://search.pandown.cn/api/query?surl=https://pan.baidu.com/share/init?surl=UAf3I3nk1J1SicuCJN712A

## Log:five:

1. conda install && pip install
2. numel 
3. add remote repo √
4. MATLAB 地图工具箱[Mapping Toolbox](https://localhost:31516/static/help/map/index.html) > [Geometric Geodesy](https://localhost:31516/static/help/map/coordinates-geodesy-and-projections.html)



## Log:six:

1. miui最简系统
2. search  path-cmd
   - 添加folder 及 child folder √
   - 保存path添加
3. UIFIGURE 总结
4. 对象管理
5. [使用 App 设计工具](https://www.mathworks.com/help/releases/R2018b/matlab/creating_guis/ways-to-build-matlab-guis.html#bu7g5rw-1)
6. [使用 GUIDE](https://www.mathworks.com/help/releases/R2018b/matlab/creating_guis/ways-to-build-matlab-guis.html#bu7g5rr)
7. [以编程方式使用 MATLAB 函数创建 App](https://www.mathworks.com/help/releases/R2018b/matlab/creating_guis/ways-to-build-matlab-guis.html#bu7g5rv-1)
8. matlab **global** 总结、
9. strcmpi、strncmp、find、uigetfile（参数设置）

## Log:seven:

1.  加载文件的方式：load read readtable fopen
2. 使用正则表达式替换文本https://ww2.mathworks.cn/help/matlab/ref/regexprep.html
3. 组件间共享数据https://ww2.mathworks.cn/help/matlab/creating_guis/share-data-among-callbacks.html √

## Log:eight:

1. 嵌套函数 √ 



## 回调-matlab

定义:

当图形界面发生特殊事件时，GUI 传递将要执行的函数代码到M文件中，以对响应相对事件，做出响应的函数。



## Log:one:

1.字符串做变量名；

https://cloud.tencent.com/developer/article/1596326



## Log:two:

1.统计信息

https://blog.csdn.net/u010186354/article/details/104100303

https://ww2.mathworks.cn/help/stats/statistical-visualization.html

```matlab
clc;
tcf;
m_1_copy = m_1;
m_1_copy = sort(m_1_copy,'descend');
tbl = tabulate(m_1_copy);
subplot(3,3,1)
bar(tbl(:,1),tbl(:,2))

subplot(3,3,2)
x = 0:1:10;
y = x+rand(size(x));
scatter(x,y,'o','filled')
refline
```



2.root color

3.方差分析

https://zhuanlan.zhihu.com/p/30323106

https://www.cnblogs.com/HuZihu/p/9442316.html

https://zhuanlan.zhihu.com/p/53184516

https://blog.csdn.net/qq_33039859/article/details/85248430

4.匿名函数绘图

5.matlab找出重写plot函数-参数检查

6.Gaussian滤波

https://loopvoid.github.io/2017/03/04/%E4%B8%80%E7%BB%B4%E4%BF%A1%E5%8F%B7%E7%9A%84%E9%AB%98%E6%96%AF%E6%BB%A4%E6%B3%A2/

https://www.jianshu.com/p/961490ea0458

## Log:five:

1.git push 

```bash
$ git push
fatal: The upstream branch of your current branch does not match
the name of your current branch.  To push to the upstream branch
on the remote, use

    git push main HEAD:master

To push to the branch of the same name on the remote, use

    git push main HEAD

To choose either option permanently, see push.default in 'git help config'.

```

2.todo:set --upstream-to 

3.理想三边定位结果



## log:three:

1.bash copy

https://www.jb51.net/article/18981.htm

2.雅各比、海塞矩阵

3.Googleplay https://www.moerats.com/archives/112/

4.429 response



## Log:four:

1.R语言

2.自动驾驶技术栈

3.git push time out 429

4.数据结构设计



