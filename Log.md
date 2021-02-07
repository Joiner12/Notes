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

