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



## Log:two:

1.matlab数学公式 

https://blog.csdn.net/weixin_45026882/article/details/102521477

2.fit曲线拟合

https://www.cnblogs.com/CherryWull/p/5574277.html

## Log:three:

1.matlab 求解方程

https://www.yiibai.com/matlab/matlab_algebra.html

2.自适应KALMAN

https://zhuanlan.zhihu.com/p/100074040

3.EXCEL制作甘特图

https://www.zhihu.com/question/20995941

4.dbscan聚类算法

## Log:four:

**1.房价信息监视**

2.

## Log:five:

1.git搭建局域网

https://segmentfault.com/a/1190000020433824

https://blog.csdn.net/likai503819723/article/details/79704841?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.baidujs&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.baidujs

2.支持向量机(SVM)

https://zhuanlan.zhihu.com/p/31886934

3.heatmap

## Log:one:

1.matlab解析函数求解

2.Gaussian-Lg模型

3.emoji in matlab

 https://www.mathworks.com/help/textanalytics/ug/analyze-test-data-using-emojis.html

https://ww2.mathworks.cn/matlabcentral/discussions/highlights/134287-happy-st-patrick-s-day-simple-emoticon-animation-demo

https://tool.chinaz.com/tools/unicode.aspx



## Log:two:

1.github & gitlab

https://www.yiibai.com/gitlab/gitlab_introduction.html 教程

2.basemap

https://ww2.mathworks.cn/help/map/ref/addcustombasemap.html

3.geo转换Cartesian 

横轴墨卡托投影，将地图经纬度转换为平面直角坐标(BL to UTM)

## Log:three:

1.matlab 匿名函数绘图

https://ww2.mathworks.cn/help/matlab/ref/fplot.html#bu6xntj-1-f

2.拟合过程调整

3.获取wallpaper实时修改壁纸

4.git合并多条提交

5.geobase

https://www.eoas.ubc.ca/~rich/map.html#3._Stereographic_projection_of_North

https://www.shuzhiduo.com/A/6pdDQbkqzw/

6.github ssh有什么用

https://docs.github.com/cn/github/authenticating-to-github/connecting-to-github-with-ssh

## Log:four:

1.键盘-touchpad

2.circlem https://ww2.mathworks.cn/help/map/generate-small-circles.html

https://itectec.com/matlab/matlab-how-to-create-a-map-of-uk-with-circles-plotted-at-certain-locations/

3.https://bbs.rainmeter.cn/thread-117875-1-1.html 

4.环境因子

**硬盘备份**



## Log:one:

1.加权最小二乘法

https://blog.csdn.net/weixin_44194909/article/details/105123867

2.数据拷贝（matlab | python）

https://zhuanlan.zhihu.com/p/35725217

3.爬虫

https://china-testing.github.io/scrap_books.html

## Log:two:

1.cep圆概率误差

2.gscatter

3.struct array

4.dbscan

https://blog.csdn.net/huacha__/article/details/81094891

## Log:five:

1.table使用



## Log:two:

1.鼠标、键盘事件监控

https://docs.microsoft.com/en-us/windows/win32/winmsg/using-hooks#installing-and-releasing-hook-procedures

https://www.cnblogs.com/fanling999/p/4592740.html

## Log:three:

1.geopy

## Log:four:

1.find

2.table是否要求每列长度相同

3.bluetooth

https://stackoverflow.com/questions/1863092/bluetooth-discover-devices-type-question

https://blog.csdn.net/wangzhen209/article/details/50250321

api doc https://docs.microsoft.com/zh-cn/windows/win32/api/BluetoothAPIs/

https://blog.csdn.net/wangzhen209/article/details/49204771

https://blog.csdn.net/guotianqing/article/details/104224439

bluez http://www.bluez.org/

https://www.jb51.net/article/163875.htm

https://www.elinux.org/RPi_Bluetooth_LE



## Log:five:

1.linux 

查看进程 ps https://blog.csdn.net/yihanzhi/article/details/82351243

重启

http://c.biancheng.net/view/793.html

系统使用

https://blog.csdn.net/albenxie/article/details/72885951

## Log:one:

1.meal to eat

## Log:two:

1.获取键盘输入

https://blog.csdn.net/shuwenting/article/details/79711869

## Log:five:

1.groot

https://blogs.mathworks.com/steve/2019/02/22/making-your-plot-lines-thicker/?s_tid=mlc_recom_leaf

## Log:one:

1.matlab动图

https://blog.csdn.net/zengxiantao1994/article/details/77482852

2.share data among callbacks 

https://www.mathworks.com/help/matlab/creating_guis/share-data-among-callbacks.html

3.按键推出

https://blog.csdn.net/u010186001/article/details/73335385

## Log:two:

滤波器|经典高低通滤波器推导

https://blog.csdn.net/piaoxuezhong/article/details/78619150

## Log:three:

1.bp神经网络

https://zhuanlan.zhihu.com/p/45190898

2.matlab图像操作

https://blog.csdn.net/xsz591541060/article/details/107782376

## Log:four:

1.kalman

https://blog.csdn.net/qq_43499622/article/details/103055593

## Log:five:

1.fitfist algorithm

[对数据进行概率分布对象拟合 - MATLAB fitdist - MathWorks 中国](https://ww2.mathworks.cn/help/stats/fitdist.html)



## log:seven:

1.[卡尔曼滤波：从入门到精通 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/36745755)

2.[室内定位系列（五）——目标跟踪（卡尔曼滤波） - rubbninja - 博客园 (cnblogs.com)](https://www.cnblogs.com/rubbninja/p/6220284.html)

## Log:one:

方差&协方差https://zhuanlan.zhihu.com/p/37609917

## Log:five:

1.加权非线性最小二乘

https://ww2.mathworks.cn/help/stats/weighted-nonlinear-regression.html

## Log:four:

[类构造函数方法 - MATLAB & Simulink - MathWorks 中国](https://ww2.mathworks.cn/help/matlab/matlab_oop/class-constructor-methods.html)

[matlab 转义字符_#+!-CSDN博客_matlab转义字符](https://blog.csdn.net/colddie/article/details/7248651)

```

Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 8 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (12/12), 104.95 MiB | 1.11 MiB/s, done.
Total 12 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 1 local object.
remote: warning: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: warning: See http://git.io/iEPt8g for more information.
remote: warning: File Doc/MATLAB面向对象编程 13662949.pdf is 64.40 MB; this is larger than GitHub's recommended maximum file size of 50.00 MB
To github.com:Joiner12/ArchivedNote.git
   09eff24..5a8a30d  master -> master

```

## Log:five:

1.矩阵逆和矩阵除法

2.nlfit-matlab

## Log:six:

[优秀的开源GIS软件 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/265023839)

## Log:two:

1.matlab数据结构探讨

[MATLAB 高级数据结构连载 1：金融时间序列Financial Time Series (Part A) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/21409091)

[MATLAB映射表数据结构-技术专栏-MATLAB中文论坛 (ilovematlab.cn)](https://www.ilovematlab.cn/article-56-1.html)

## Log:three:

[C 和 C++ 的矩阵库评估和比较 Meschach、Cooperware 矩阵和 Blitz_Steven_Sunny的专栏-CSDN博客](https://blog.csdn.net/sunnyxidian/article/details/8916861)

[矩阵的逆 C 语言 算法一 - 忽而今夏 - 博客园 (cnblogs.com)](https://www.cnblogs.com/tianzhenyun/p/4527742.html)

## Log:four:

[（数学概念）矩阵的逆、伪逆、左右逆，最小二乘，投影矩阵 - AndyJee - 博客园 (cnblogs.com)](https://www.cnblogs.com/AndyJee/p/5082508.html#:~:text=一、矩阵的逆、伪逆、左右逆 1 矩阵A可逆的充要条件是A的行列式不等于0。 2 可逆矩阵一定是方阵。 3 如果矩阵A是可逆的，A的逆矩阵是唯一的。,4 可逆矩阵也被称为非奇异矩阵、满秩矩阵。 5 两个可逆矩阵的乘积依然可逆。 6 可逆矩阵的转置矩阵也可逆。 7 矩阵可逆当且仅当它是满秩矩阵。)

[extern "C"：实现C++和C的混合编程 (biancheng.net)](http://c.biancheng.net/view/8064.html)

## Log:one:

[[总结\]C语言二维数组作为函数的参数 - Rabbit_Dale - 博客园 (cnblogs.com)](https://www.cnblogs.com/Anker/archive/2013/03/09/2951878.html)