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
5. git 同时输入两条指令



## Log:four:

1. 最小二乘求解

https://mp.weixin.qq.com/s/MSswKzWuziBHEvbZbEkeVw

https://zhuanlan.zhihu.com/p/113946848

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
   - 添加folder 及 child folder
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
3. 组件间共享数据https://ww2.mathworks.cn/help/matlab/creating_guis/share-data-among-callbacks.html



## Log:eight:

1. 嵌套函数
2. 回调函数http://blog.sina.com.cn/s/blog_6163bdeb0100i2id.html

https://ww2.mathworks.cn/help/matlab/creating_plots/callback-definition.html



## 回调-matlab

定义:

当图形界面发生特殊事件时，GUI 传递将要执行的函数代码到M文件中，以对响应相对时间，做出响应的函数。



## MATLAB局部变量、全局变量、永久变量作用域

### 基础和函数工作区

**基础工作区**

基础工作区存储命令行创建的变量以及通过通过命令行或者编辑器运行的脚本中创建的变量；

**函数工作区**

MATLAB中为了保护数据的完整性，设计了函数工作区、基础工作区和其他工作区(workspace)。每个函数有独立的函数工作区，即使普通函数的`局部函数`也有其独立的工作区。每个函数工作区中的变量都为局部变量。函数调用脚本时，使用的是函数工作区。

**嵌套函数**

嵌套函数：在函数内部定义的函数。

嵌套函数也有其自身的工作区，同局部函数不同的是：

- 嵌套函数可以对其所在的函数的变量进行读写；
- 嵌套函数或包含嵌套函数的函数中的所有变量都需要显式定义；

### 在工作区之间共享数据

Matlab中，不同的工作区之间共享数据的方式有以下几种：

- [ ] 传递参数 (parameter)
- [ ] 嵌套函数 (nested function)
- [ ] 持久性变量 (persistent)
- [ ] 全局变量 (global)
- [ ] 在另一工作区中计算

**传递参数**

扩大函数作用域的最安全的方式是通过函数输入、输出参数；

**嵌套函数**${^{[1]}}$

嵌套函数可以访问其所在的所有函数的工作区。

```matlab
function NestedParentFcn()
	disp('parent function');
	VarX = 0;
    NestedFcn;
    function NestedFcn()
        VarX = VarX + 1;
        VarY = 1;
    end
    try
    	%警告: 文件:LiveEditorEvaluationHelperESectionEval.mlx 行:11 列:9
		%在嵌套函数中定义 "VarY" 会将其与父函数共享。在以后的版本中，
		%要在父函数和嵌套函数之间共享 "VarY"，请在父函数中显式定%义它。 

        disp(VarY)
    catch
        disp('Access Variable VarY Error');
    end
end
```



**持久性变量**

- 持久性变量是声明该变量的局部变量；
- 其值保存在每次调用声明持久变量函数的内存中，类似于C语言中的statics local var；
- 命令行或其他函数不能访问持久变量；
- 持久变量和全局变量类似，其值都一直保存于内存中，差异在于其可见性范围；



**syntax**

```matlab
%% example-persistent
clear varP; % 清除persistent变量
for i = 1:1:10
PersistentFcn();
end
function PersistentFcn()
persistent varP; % 声明persistent变量
if isempty(varP)
    varP = 1;
end
varP = varP + 1;
disp(varP);
end
```



**持久变量的使用**

- 持久变量必须先进行声明，声明时候其值初始化为[]；
- 必须先声明持久变量，才能对其进行其他引用；
- 以下操作可清除函数的持久性变量：`clear all`、`clear functionname`、编辑函数文件；



**全局变量**

全局变量是可以从函数或命令行中访问的变量。它们拥有自己的工作区，这些工作区与基础和函数工作区分开。如果多个函数都将特定的变量名称声明为`global`，则它们都共享该变量的一个副本。在任何函数中对该变量的值做任何更改，在将该变量声明为全局变量的所有函数中都是可见的。

**syntax**

```matlab
%% 
global g_var; % 声明global



```





[1] .[嵌套函数](https://ww2.mathworks.cn/help/matlab/matlab_prog/nested-functions.html?s_tid=srchtitle)





