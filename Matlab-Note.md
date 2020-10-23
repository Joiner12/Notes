# Matlab Note

——记录Matlab相关；

### 1.自然对数e

<https://blog.csdn.net/Katherine_S/article/details/53677608>

符号变量

syms sys

### 2.S函数

《S函数介绍》

<https://blog.csdn.net/acelit/article/details/59082349>

### 3.MATLAB批量修改名字

《利用MATLAB批量修改文件名》

包括对eval函数的解释

<https://blog.csdn.net/rs_huangzs/article/details/56674181>

https://blog.csdn.net/u010099080/article/details/49915743

### 4.MATLAB 静态变量和全局变量

persistent  & global

<https://blog.csdn.net/u010177286/article/details/45674887>

--winopen()

### 5.Matlab字符串做变量名

《字符串处理函数》

<http://www.cnblogs.com/emanlee/archive/2012/09/13/2683912.html>

《字符串|变量名》

<https://blog.csdn.net/humanking7/article/details/80628757>

```matlab
str_var = 'varNumber';
eval( [str_var, '= 10']);
```

《字符串变量名》

<https://blog.csdn.net/qq_21090131/article/details/82953326>

### 6 Matlab*.fig中提取Origin Data

《*.fig提取数据》

<https://blog.csdn.net/shineprince/article/details/79688351#>

### 7 MATLAB 多点运动图

<https://www.zhihu.com/question/30908838>

[matlab绘图的坐标轴数字、范围、间隔控制 .](https://www.cnblogs.com/xbinworld/archive/2011/11/24/matlab1.html)

《Color》

<https://blog.csdn.net/wh1312142954/article/details/80796764>

### 8 Matlab解决调用其他文件夹函数的问题

<https://blog.csdn.net/cfyzcc/article/details/50535632> Matlab中用文件夹中子文件夹内.m文件的方法

<https://blog.csdn.net/qq_31811537/article/details/79036152> matlab主程序和子函数不在一个文件夹下，怎么调用

-.1*.asv

```
有时在存放m文件的文件夹中会出现*.asv,asv 就是auto save的意思，*.asv文件的内容和相应的*.m文件内容一样，用记事本和matlab都能打开它。它可以作为*.m文件的“备份”。
　　可以在preference中通过设置取消自动备份功能：file-&gt;preferences-&gt;editor/debugger--&gt;auto save,uncheck "autosave on" checkbox ，把勾选去掉就行了。

```

-.2sign函数

### 9 Matlab脚本 ->exe

<https://blog.csdn.net/proton_boke/article/details/72865498>

### 10 GUI获取数据

《Matlab GUI设计——文件读取和保存uigetfile,uiputfile》

<https://blog.csdn.net/hit1524468/article/details/48935511>

《Matlab读取txt文件中的数据（使用textread函数）》

<https://blog.csdn.net/jisuanjiguoba/article/details/79997805>

《Matlab中读取txt文件的几种方法》

<https://blog.csdn.net/zhuxiaoyang2000/article/details/7330783>

《Matlab GUI界面设计》

<https://blog.csdn.net/u011939755/article/details/54705664>

《判断文件夹、文件是否存在、创建文件 c++ matlab》

<https://blog.csdn.net/u012005313/article/details/50688257>

《Matlab GUI设计》

<https://www.cnblogs.com/ruo-li-suo-yi/category/1152708.html>

《Callback 和 CreatFcn的区别》

<https://blog.csdn.net/yundanfengqing_nuc/article/details/77160622>

《GUI修改背景图》

<https://blog.csdn.net/leo0308/article/details/82694995>

<https://blog.csdn.net/qq_20823641/article/details/51910690>

《数据传递》

<https://blog.csdn.net/xgf415/article/details/50742740>

<https://blog.csdn.net/eric_e/article/details/86708307>

《异常捕获》

<https://blog.csdn.net/bible_reader/article/details/72960200>

《Matlab中函数句柄@的作用及介绍》

<https://blog.csdn.net/kevinhg/article/details/8861774>

《MATLAB读取表中数据》

<https://ww2.mathworks.cn/help/matlab/import_export/read-spreadsheet-data-into-table.html>

### 11 Table数据类型

<https://www.ilovematlab.cn/article-52-1.html>

```matlab
% 函数
importdata('file')
readdata('file')

%访问数据
'.' , '{}','()'
```

### 12 正态分布常用函数

《normpdf_normcdf_norminv_normrnd_normfit》

<https://blog.csdn.net/shanchuan2012/article/details/52901758>

### 13.矩形波

《matlab产生方波脉冲和周期性方波信号》

<https://blog.csdn.net/wordwarwordwar/article/details/56676130>

### 14 Persistent Global

《Persistent》

<https://ww2.mathworks.cn/help/matlab/ref/persistent.html?s_tid=doc_ta>

《动画实现》

<http://www.matlabsky.com/thread-570-1-1.html>

<http://www.matlabsky.com/thread-240-1-1.html>

### 15 CMD指令运行MATLAB

1.《cmd 命令行方式执行 matlab 脚本》

<https://blog.csdn.net/lanchunhui/article/details/51273109>

2.《远程运行MATLAB》

<https://ww2.mathworks.cn/matlabcentral/answers/84619-close-the-terminal-but-keep-matlab-running-remotely>

3.《VS coder 配置MATLAB》

<https://www.waitig.com/vs-code%E9%85%8D%E7%BD%AEmatlab%E7%8E%AF%E5%A2%83.html>

4.《C语言调用MATLAB程序之简单样例》

<https://blog.csdn.net/u011008379/article/details/52770863>

5.《C++调用Matlab生成的DLL动态链接库进行混合编程》

<https://blog.csdn.net/qq_36165459/article/details/81283932>

6.《C语言环境中调用Matlab程序指南》

<https://wenku.baidu.com/view/2aa0632a0066f5335a812178.html?re=view>

### 16.写Txt

<https://blog.csdn.net/kunyxu/article/details/53563154>

```m
fopen方式
save方式
```

### 17.中文乱码

1.《解决Matlab script脚本文件显示中文乱码的问题》

<https://blog.csdn.net/He_MM/article/details/51943526>

2.《解决matlab中文乱码》

<https://blog.csdn.net/soliddream66/article/details/61414565>

3.《MATLAB将默认编码方式由GBK转为UTF-8》

<https://blog.csdn.net/qq_36829091/article/details/80098828>

4.《GBK | UTF-8 | GB2312区别》

<https://blog.csdn.net/ZYY88886666/article/details/75285780>

### 18 .Simulink外部数据，信号源

1.<https://www.ilovematlab.cn/thread-506910-1-1.html>

---

### 19. figure属性操作|Print保存图片

1.《figure属性操作》

<https://blog.csdn.net/kevinxdg/article/details/81106750>

2.《print保存图片》

<https://www.cnblogs.com/stxs/p/8808971.html>

---

### 20. matlab书籍资源

<https://blog.csdn.net/myvanguard/article/details/84061563>

### 21 修改启动默认位置

https://blog.csdn.net/u012210613/article/details/52346842

```

```

---

### 22 高级绘图

1.<https://www.cnblogs.com/jeromeblog/p/3396494.html>

2.MATLAB的Gui对象关系

https://blog.csdn.net/yangguangqizhi/article/details/53815382

3.set函数用法

https://blog.csdn.net/weixin_41554884/article/details/79913272

---

### 23 打包exe文件

1.matlab将M文件直接编译为可独立使用的EXE可执行文件

https://blog.csdn.net/jkhere/article/details/8906124

### 24 差分

```
diff(x)
```

<https://ww2.mathworks.cn/help/matlab/ref/diff.html?s_tid=srchtitle>

### 25 WordsCloud

<https://ww2.mathworks.cn/help/matlab/ref/wordcloud.html?s_tid=srchtitle>

### 26 Try catch

https://ww2.mathworks.cn/help/matlab/ref/try.html?searchHighlight=try&s_tid=doc_srchtitle

### 27 Java.Robot 实现键鼠控制

1.JVM(Java Virtural Machine)

```matlab
version -java
```

2.Java 控制键鼠

<https://blog.csdn.net/u011389706/article/details/57399942>

### 28 Retangle|Viscircles画圆

<https://blog.csdn.net/ZLK961543260/article/details/70216089>

2.属性

<https://ww2.mathworks.cn/help/matlab/creating_plots/access-and-modify-property-values.html>

3.动态绘图

<https://blog.csdn.net/u010480899/article/details/78234884>

<https://blog.csdn.net/nbu2004/article/details/50993093>

### 29 Cell数据操作

<https://blog.csdn.net/yam_killer/article/details/7964872>

2.Cell全部函数

<https://blog.csdn.net/u010999396/article/details/54386465>

### 30 datenum函数

<https://blog.csdn.net/without_scruple/article/details/77352641>

**etime()**

### 31 字符串拆分

<https://blog.csdn.net/gotomic/article/details/7898307>

### 32 文件夹内容

```matlab
% 两种方式均能使用reg
what
ls 
% 搜索doc
docsearch <string>

```

---

### 33 积分

《int》

<https://blog.csdn.net/qq_34374664/article/details/79186465>

《trapz》

<https://ww2.mathworks.cn/help/matlab/ref/trapz.html?requestedDomain=cn

《b数值积分方法》

<https://zhuanlan.zhihu.com/p/82459587>

### 34 APP

1.《2018Rb》

<https://ww2.mathworks.cn/help/matlab/code-app-behavior-in-app-designer.html>

2.《2019》

https://ww2.mathworks.cn/help/matlab/components-in-app-designer.html?searchHighlight=app&s_tid=doc_srchtitle

3.timer

https://ww2.mathworks.cn/help/matlab/ref/timer-class.html?searchHighlight=timer&s_tid=doc_srchtitle

4.对话框处理

《GUI之常用对话框（三）--- dialog \ errordlg \ warndlg \ helpdlg \ msgbox \questdlg》

https://blog.csdn.net/zjq2010014137/article/details/8535431

《matlab GUI之常用对话框（四）---输入对话框 inputdlg、目录对话框 uigetdir、列表对话框 listdlg》

**https://blog.csdn.net/zjq2010014137/article/details/8535913**

《matlab inputdlg》

https://ww2.mathworks.cn/help/matlab/ref/inputdlg.html?searchHighlight=inputdlg&s_tid=doc_srchtitle

《matlab questdlg》

https://ww2.mathworks.cn/help/matlab/ref/questdlg.html

### 35 SerialPort

《自动识别串口设备并获取其串口号（serial && friendly name）》

<https://blog.csdn.net/u011389706/article/details/78929480>

### 36 RunTime

《RunTime 文档》

<https://ww2.mathworks.cn/help/compiler/deployment-process.html>

### 37 全屏figure

<https://blog.csdn.net/am290333566/article/details/84581313>

### 38 匿名函数

https://blog.csdn.net/lqhbupt/article/details/18951311



### 39 回调函数编写

https://blog.csdn.net/whu_shao/article/details/53868956

### 40 Simulink 代数环

```
一、代数环的问题
在数字计算中，输入信号决定输出信号，同时输出信号也决定输入信号，由于数字计算的时序性，导致没有输出信号无法计算输入信号，没有输入信号又反过来无法计算输出信号，形成一个死锁（deadlock）或死循环，这就是代数环。如下图1所示，就是一个简单的代数环的例子。
二、代数环产生的条件
简单地说，代数环其实就是一个输入信号包含输出信号，同时输出信号也包含输入信号的特殊反馈回路。在simulink中，这是由于直通模块（无延时的模块）的原因造成的，simulink中大部分的模块都是直通模块，因此很容易形成代数环。在整个回路中，只包含直通模块就会形成代数环，反馈回路有延时模块就会消除代数环。
三、代数环的解决措施
1、用工具栏中的“simulink”中的“diagnostics”对代数环进行消除
将simulink中diagnostics的对代数环的处理信息进行选择，将对代数环的处理信息选择为“none”，即忽略代数环的信息。
2、在反馈回路中添加延时模块进行消除
由于代数环的产生是由于整个模型中所有模块均为直通模块，因此只需在反馈回路中添加延时模块即可消除代数环。延时模块有delay模块、memory模块，如图2所示，用memory来消除代数环。
3、用变换法消除代数环
对于简单的代数环问题，可以通过人为地采用数字变换法来求解消除代数环，但这只针对简单的代数环有限，对于复杂的代数环基本不可能实现。
4、在反馈回路中添加入高频传递环节
在反馈回路中添加入高频传递函数，打断反馈回路中的直通模块，消除输入信号与输出信号的关联关系。如图3所示。

reference:
https://www.ilovematlab.cn/thread-260304-1-1.html
```

### 41 绘图

<https://zhuanlan.zhihu.com/p/23598477>

### 42 Cody

https://www.mathworks.com/matlabcentral/cody/

### 43.Matlab Command Color

<http://undocumentedmatlab.com/blog/changing-matlab-command-window-colors/>

### 44.iddata

数据保存类型，相比较于mat文件，可以存储数据的类型，以及相关属性；

https://ww2.mathworks.cn/help/ident/gs/identify-nonlinear-black-box-models-using-the-gui.html

### 45.蕨形树叶

《蕨形树叶》<https://zhuanlan.zhihu.com/p/24649825>

---

### 46.地图

#### 45.1 地图绘图

1.

<https://ww2.mathworks.cn/help/matlab/ref/geoscatter.html?s_tid=doc_ta>

2.《Geobasemap》

<https://ww2.mathworks.cn/help/matlab/ref/geobasemap.html?requestedDomain=cn>

3.《worldmap》

<https://www.cnblogs.com/stxs/p/8666372.html>



---

#### 45.2 gca | gcf | shg | clf

**gca：**坐标轴区域图；

**gcf：**当前图句柄；

**shg：** 显示最新图窗；

**clf：**清除当前图窗；

---

### 47.Simulink 仿真

1.<https://blog.csdn.net/zkzfengyi/article/details/80473110>

2.[基于S函数的RBF神经网络PID控制器Simulink仿真](http://d.wanfangdata.com.cn/Periodical/ahyjkjzyxyxb200801007)

3.[基于S函数在自抗扰控制器Simulink仿真中的应用](http://d.wanfangdata.com.cn/Periodical/yqybyh201204027)

4.《matlab(Simulink)中S-function函数编写规则》

<https://blog.csdn.net/mengxiangjia_linxi/article/details/75516142>

5.《SIMULINK6 S-Function 编程（M，C/C++语言）与模块封装技术(1)Simulink S函数概观》

<https://blog.csdn.net/ComplexAdaptiveSys/article/details/919938#commentBox>

6.《MATLAB2015a中Simulink使用S函数的方法全过程》

<https://blog.csdn.net/peixianlyc/article/details/84034583>

7.《离散系统-simulink》

https://blog.csdn.net/weixin_43159148/article/details/88574201

http://bbs.elecfans.com/jishu_369721_1_1.html

8.《S函数指南》

<https://blog.csdn.net/acelit/article/details/59082349>

基于MATLAB/Simulink系统仿真权威指南   pdf'

9.《S funtion基础》

<https://ww2.mathworks.cn/help/simulink/s-function-basics-matlab.html>

---

### 48.Histogram 

1.《Doc-Histogram》

<https://ww2.mathworks.cn/help/matlab/ref/matlab.graphics.chart.primitive.histogram.html>

### 49.Table补全

```matlab
file = 'C:\\User\\Desktop\\file.txt';
opts = detectImportOptions;
opts.VariableNames = {'what','the','fun'};
origin_table = readtable(file,opts);
% 局部使用struct2table table2struct
full_struct = table2struct(origin_table);
% 使用截断方法
table_size = size(origin_table);
cut_index = 1;
for i = 2:1:table_size(1)
	% table以列为导向(column oriented)，strut 以行为导向(row oriented)
	if isempty(origin_table.what(i)) || imempty(origin_table.fun(i))
		full_struct(i).what = origin_table.what(cut_index);
	else
		cut_index = i;
	end
end
```

---

### 50.信号频谱

1.《使用MATLAB—SIMULINK分析典型信号频谱特性》

https://www.cnblogs.com/cql/archive/2012/12/01/2797821.html

2.《三角波》

<https://www.jianshu.com/p/ea3f9a325801>

《TD》

<https://zhuanlan.zhihu.com/p/76326861>

---

### 51.Reg

1.《Official Doc》

<https://ww2.mathworks.cn/help/matlab/matlab_prog/regular-expressions.html>

---

### 52.《matlab dos执行》

1.<https://blog.csdn.net/nupt123456789/article/details/7943910>

2.<https://stackoverflow.com/questions/7614292/run-a-matlab-script-from-windows-dos-prompt>

3.<https://ww2.mathworks.cn/matlabcentral/answers/238069-how-to-run-a-m-file-without-showing-command-window>

---

### 53.Copy File

1.《Official Doc》

<https://ww2.mathworks.cn/help/matlab/ref/copyfile.html>

---

### 54. classdef

1.《Official Doc》

<https://ww2.mathworks.cn/help/matlab/sample-classes.html>

2.《matlab——之class类（详细总结）》

<https://blog.csdn.net/qinze5857/article/details/80545885>

3.《matlab-如何定义类》

<https://www.cnblogs.com/wangduo/p/5908311.html>

4.《Tutorial: Using Matlab compiled classes from within Python》

<http://www.cloud-rocket.com/2016/08/using-matlab-compiled-class-from-python/>

---

### 55.《MATLAB versus Python》

1.《Offical Doc》

<https://ww2.mathworks.cn/products/matlab/matlab-and-python.html>

<https://ww2.mathworks.cn/help/matlab/matlab-engine-for-python.html>

2.《开发类 - 典型工作流 - MATLAB & Simulink - MathWorks 中国.html》

<https://ww2.mathworks.cn/help/matlab/matlab_oop/developing-classes-typical-workflow.html>

---

### 56.《C调用matlab engine》

1.<https://ww2.mathworks.cn/help/matlab/apiref/engopen.html>

2.《demo - matlab》

```
//MATLAB//R2018b//extern//examples//eng_mat//engdemo.c
//MATLAB//R2018b//extern//examples//eng_mat//engdemo.cpp
```

3.《visual 调用MATLAB静态库》

<https://ww2.mathworks.cn/matlabcentral/answers/467518-how-can-i-build-a-c-program-using-matlab-engine-in-visual-studio>

4.《official doc》

<https://ww2.mathworks.cn/help/matlab/matlab_external/compiling-engine-applications-in-an-ide.html>

---

### 57.《Path操作》

1.《指令操作路径》

<https://blog.csdn.net/chaolei3/article/details/83003426>

```matlab
addpath([path|genpath(path)]);% 添加文件夹|及其子路径
rmpath([path|genpath(path)]);% 删除文件夹|及其子路径

```



---

### 58.《范数计算》

<https://blog.csdn.net/wywywy01/article/details/77823003>

```matlab
norm(a,size1,...sizen,'classdef')
```



---

### 59.《Simulink \To WorkSpace模块》

```matlab
%{
	To WorkSpace模块输入数据类型：timeseries;
	e.g:yout
	>> yout
	timeseries常见属性：
		Name:''
		Time:[]
		TimeInfo:
		Data:[]
		DataInfo:
	使用方式类似于struct和table
%}
yout;% timeseries
time = yout.time;
data = yout.data;
```

---

### 60.fimplicit 隐函数绘图

1.《Official Doc》

 <https://ww2.mathworks.cn/help/matlab/ref/fimplicit.html>

---

### 61.色块图

<https://blog.csdn.net/zzx2016zzx/article/details/80635840>

---

### 62.局部放大

<https://blog.csdn.net/schwein_van/article/details/78513908>

<https://ww2.mathworks.cn/matlabcentral/fileexchange/5961-magnify>

---

### 63.Levenshtein Distance 

<https://blogs.mathworks.com/cleve/2017/08/14/levenshtein-edit-distance-between-strings/>

---

### 64.figure handle

<https://www.cnblogs.com/BlueMountain-HaggenDazs/p/4306865.html>

---

### 65.Inverted Pendulum Simulator

  Simulink 实现倒立摆可视化；

1.倒立摆数学模型

<https://blog.csdn.net/yin_bu_feng/article/details/89100188>

2.Roy Featherstone's Website

<http://royfeatherstone.org/>



### 66.数组操作

#### (1)找出复合条件的数

```matlab
a = 100*rand(1,100);
b = a;
b(a>50)=0;
```

[1] https://blog.csdn.net/u014636245/article/details/102575785



### 67.微分处理

```matlab
% 符号函数实用
t = sym('t'); % syms t;
y = t^2 + sqrt(t);
diff_y = diff(y);

```

<https://www.yiibai.com/matlab/matlab_differential.html>



### 68.Patch绘图|Patch Property

<https://ww2.mathworks.cn/help/matlab/ref/patch.html>

---

### 69.Matlab数字信号处理函数（波形）

1.Signal Generator https://ww2.mathworks.cn/help/signal/waveform-generation.html

2.tripuls

<https://blog.csdn.net/Nan_qi_de_ming_zi/article/details/88076592>

3.逻辑判断（矩阵）生成典型信号

<https://www.mathworks.com/help/signal/gs/impulse-step-and-ramp-functions.html>

---

### 70.进制转换

<https://ww2.mathworks.cn/help/matlab/ref/dec2hex.html>



### 72.SimMechanics

#### 1.模型搭建

实体（bodies）、铰（joints）、外力（forces）

Rigid Transform：定义相对位置

Revolute Joint：定义ZX平面运动

World Frame：绝对坐标系

使用SimMechanics Link 导入CAD模型和数据

```matlab
smimport %导入xml文件
```

content preview



### 73.Map 

1.m_map工具包—2020

<https://cloud.tencent.com/developer/article/1606160>

2.matlab Mobil

<https://zhuanlan.zhihu.com/p/27346710>



### 74.cellfun

1.cellfun

<https://ww2.mathworks.cn/help/matlab/ref/cellfun.html>

2.arrayfun & cellfun & bsxfun

<http://chuan92.com/2016/01/17/bsxfun-cellfun-and-arrayfun-in-matlab>

3.eval函数

<https://www.mathworks.com/help/matlab/ref/eval.html>



### 75.Map 

1.调用GoogleMAP API

<https://www.mathworks.com/matlabcentral/fileexchange/27627-zoharby-plot_google_map>

2.Matlab Mobile高逼格实时记录GPS运动轨迹（各项参数统计计算）

https://zhuanlan.zhihu.com/p/126242819

3.获取传感器数据

https://zhuanlan.zhihu.com/p/128968603

4.basemap

<https://www.mathworks.com/help/map/ref/addcustombasemap.html>

<https://www.mathworks.com/help/map/ref/addcustombasemap.html>



### 76.Search Method

1.BFS WFS https://www.thinbug.com/q/33047929

2.迷宫解决matlab中的广度优先搜索算法 https://www.thinbug.com/q/33047929

3.https://blog.csdn.net/qq_35644234/article/details/60870719