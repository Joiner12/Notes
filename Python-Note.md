# Python Note

### 1.Lib-datetime

1.python 时间库

<https://www.cnblogs.com/vamei/archive/2012/09/03/2669426.html>

---

### 2.文件操作

1.检查路径是否存在

<https://www.cnblogs.com/jhao/p/7243043.html>

2.Python读写文本三种方式 https://zhuanlan.zhihu.com/p/21347291

3.Python读写txt文本文件 https://www.cnblogs.com/hackpig/p/8215786.html

4.打开文件https://blog.csdn.net/humanking7/article/details/80546728

5.python运行其他程序方式https://blog.csdn.net/Jerry_1126/article/details/46584179

---

### 3.Anaconda

1.《anaconda离线安装第三方包》

<https://blog.csdn.net/qq_39657585/article/details/82667450>

2.《本地安装》

<https://blog.csdn.net/weixin_41782111/article/details/82818319?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task>

---

### 4.串口-Python

1.串口操作

<https://blog.csdn.net/xhao014/article/details/7640568>

<https://blog.csdn.net/happyliuliming/article/details/84845560>

2.《pyserial串口操作》

<https://www.cnblogs.com/dongxiaodong/p/9992083.html>

3.《Official Doc》

<https://pythonhosted.org/pyserial/index.html>

---

### 5.GUI-PY

1.pycharm + pyqt Gui

 https://blog.csdn.net/bailang_zhizun/article/details/79310419 

 https://blog.csdn.net/m0_37606112/article/details/78556683 

2.《pyqt中文教程》

 https://maicss.gitbooks.io/pyqt5/content/hello_world.html 

3.《PyQt5 reference》

<https://www.riverbankcomputing.com/static/Docs/PyQt5/>

---

### 6.#UTF-8

https://legacy.python.org/dev/peps/pep-0263/

---

### 7.OS库

1.《调用*.sh》

https://www.cnblogs.com/daduryi/p/6856249.html

《重命名os.rename》

https://blog.csdn.net/alicelmx/article/details/79092964

2.《python执行系统命令四种方法比较》

https://blog.csdn.net/luckytanggu/article/details/51793218

---

### 8.turtle库

1.<https://blog.csdn.net/xiamoyanyulrq/article/details/81842604>

2./cry

<https://blog.csdn.net/qq_36369267/article/details/82831767>

---

### 9. syntax 

##### 9.1 self

<https://www.cnblogs.com/jessonluo/p/4717140.html>

##### 9.2 Break & Return & Continue

1.对整个循环的控制作用；

2.对break、return、continue后面语句的影响；

[1] https://stackoverflow.com/questions/28854988/what-is-the-difference-between-return-and-break-in-python

[2] https://blog.csdn.net/Moniicoo/article/details/79990612



### 10.路径操作

1.Official Doc - Path

<https://docs.python.org/2/library/os.path.html#os.path.realpath>

2.《绝对路径|相对路径》

<https://www.cnblogs.com/wangyanyan/p/7440685.html>

3.文件路径操作

<https://www.cnblogs.com/yanglang/p/7610838.html>

4.获取上一级文件路径

<https://blog.csdn.net/leorx01/article/details/71141643>



### 12.ICON

<https://zhuanlan.zhihu.com/p/27493719>



### 13.设置窗口背景

1.PyQt5图形和特效之设置窗口背景（六）

<https://blog.csdn.net/jia666666/article/details/81874045>

2.禁止窗口大小调整

<https://blog.csdn.net/sollor525/article/details/39316065>

3.PyQt：无边框自定义标题栏及最大化最小化窗体大小调整

<https://www.cnblogs.com/jyroy/p/9461317.html>



### 14.PyQt时钟

1.基本时钟功能

<https://blog.csdn.net/Kprogram/article/details/83623079>

2.桌面时钟（透明）

<https://cloud.tencent.com/developer/article/1124715>

3.时钟带表盘

<https://blog.csdn.net/liang19890820/article/details/52064169>

4.获取系统时间

<https://blog.csdn.net/laozhuxinlu/article/details/70217090>

<https://blog.csdn.net/zong596568821xp/article/details/82996945>



---

### 15.无边框

1.PyQt实现无边框

<https://www.cnblogs.com/codeAB/p/5019439.html>

https://www.cnblogs.com/jyroy/p/9461317.html

---

### 16.进度条

1.嵌入状态栏进度条

<https://blog.csdn.net/higher80/article/details/82703532>

2.波浪形进度条

<https://blog.csdn.net/wang13342322203/article/details/82116286>

3.动态进度条

<https://blog.csdn.net/weixin_34378969/article/details/93306790>

4.loading界面

<https://blog.csdn.net/weixin_40273809/article/details/81514646>

---

### 17.PyQt类继承关系

<https://www.cnblogs.com/tongchengbin/p/pyqt5.html>

---

### 18.PyQt&Anaconda&Pycharm环境配置

```python
# designer.exe 配置
Program: D:\ProgramData\Anaconda3\Library\bin\designer.exe
Parameters: 
Working directionary:$FileDir$

#PyUIC配置(.ui -> .py)
# Program 中写入Python的地址
Program:python.path
Parameters:-m PyQt5.uic.pyuic $FileName$ -o $FileNameWithoutExtension$.py
Working directionary:$FileDir$

#pyrcc 配置

```

目的：类似MATLAB进行拖拽编程，加快进程。

1.搭建Python开发环境，用Anaconda + PyQt + Pycharm https://zhuanlan.zhihu.com/p/30261406

2.Python制作小软件——1. 安装并使用PyQt5进行界面设计 https://blog.csdn.net/weixin_41929524/article/details/81456308

3.python3+PyQt5+Qt designer+pycharm安装及配置+将ui文件转py文件https://www.cnblogs.com/JackyXu2018/p/8722703.html

4.搭建Anaconda+pyCharm环境（NumPy，SciPy ）https://www.jianshu.com/p/916362ca16a6

5.python界面编程：VScode+pyqt+pyqt integration配置备忘 https://zhuanlan.zhihu.com/p/66758263

---

### 19.基于QT编码

https://www.jianshu.com/p/962b572a216c

### 20.Random函数

```python
import random
import numpy as np
np.random.randi()
random.random()
```

[1]https://www.jianshu.com/p/36a4bbb5536e

[2]https://www.cnblogs.com/yd1227/archive/2011/03/18/1988015.html

---

### 21.QMainWindow和QWidget的区别

主要区别在于，QMainWindow创建的是一个复合窗口，包括状态栏、菜单栏等。QWidget创建的是单一的页面。

[1]<https://blog.csdn.net/superhcq/article/details/53509183>

---

### 22.布局管理

1.嵌套布局  <https://www.cnblogs.com/hhh5460/p/5173645.html>

2.PyQt5布局管理<https://blog.51cto.com/9291927/2423303>

3.堆叠布局  https://blog.csdn.net/jia666666/article/details/81669425

https://blog.csdn.net/gan19951101/article/details/79978033?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

4.QFrame控件 https://blog.csdn.net/fanyun_01/article/details/53282676?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

6.快速掌握PyQT5 https://blog.csdn.net/La_vie_est_belle/article/details/82316745

7.高级布局 https://muyuuuu.github.io/2019/10/19/pyqt-layout/

8.tutorialspoint <https://www.tutorialspoint.com/pyqt/index.htm>

9.设置QListWidget <https://blog.csdn.net/u011125673/article/details/51753997>

10.实战！在Python中制作精美的图形用户界面 https://zhuanlan.zhihu.com/p/44146707

11.Layout https://www.learnpyqt.com/courses/start/layouts/

12.PyQt的Layout的比例化分块 https://blog.csdn.net/weixin_33995481/article/details/86275539

---

### 23.打包EXE

1.<https://blog.csdn.net/zengxiantao1994/article/details/76578421>

2.` 'utf-8' codec` <https://www.cnblogs.com/q735613050/p/10017394.html>

3.打包文件过大<https://frostime.github.io/2019/05/24/%E7%94%A8-Pyinstaller-%E6%9D%A5%E6%89%93%E5%8C%85-%E8%A7%A3%E5%86%B3%E6%89%93%E5%8C%85%E7%BB%93%E6%9E%9C%E8%BF%87%E5%A4%A7%E9%97%AE%E9%A2%98/>

---

### 24.滚动显示

1.[PyQt] 在QLabel上用drawText实现文字滚动 https://blog.csdn.net/wn0112/article/details/47086597

2.Qt 实现上下滚动字幕 https://blog.csdn.net/douzhq/article/details/80891144?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

---

### 25.数据结构

1.<https://blog.csdn.net/haiyu94/article/details/79684792>

2.<https://blog.csdn.net/sbjqiaoqiao/article/details/80713029?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task>

3.多维数组创建&遍历

```python
# 创建二维数组
[[0 for i in range(cols )] for j in range(rows)]

# 利用句柄的方式遍历
for j in list_a:
    for k in j:
        pass
```



<https://blog.csdn.net/u012505432/article/details/52218392>

<https://zhuanlan.zhihu.com/p/88197389>

<https://blog.csdn.net/qq_27261889/article/details/80422528?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task>

---

### 26.python help 

<https://blog.csdn.net/u013810296/article/details/55509284>

---

### 27.Signal & Slot

1.【PyQt5-Qt Designer】pyqtSignal()-高级自定义信号与槽] https://www.cnblogs.com/XJT2018/p/10222981.html

2.《Office tutorial》https://www.riverbankcomputing.com/static/Docs/PyQt5/signals_slots.html#connecting-signals-using-keyword-arguments

3.《PyQt5 信号与槽高级用法》http://www.broadview.com.cn/article/824

4.PyQt信号与槽之多窗口数据传递（七）https://blog.csdn.net/jia666666/article/details/81781697

---

### 28.字符串操作

1.read|readline|readlines <https://www.cnblogs.com/xiugeng/p/8635862.html>

---

### 29.Try except

1.try expect else finally <https://www.cnblogs.com/Lival/p/6203111.html>

---



### 30.Date & Time

1.time datetime moudles  https://www.cnblogs.com/tkqasn/p/6001134.html

2.计算时间差 https://www.cnblogs.com/SophiaTang/archive/2012/03/25/2417031.html

3.python--利用datetime模块计算时间差https://blog.csdn.net/wo1182929447/article/details/77841529?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task

4.python datetime处理时间 https://www.cnblogs.com/lhj588/archive/2012/04/23/2466653.html

  

---

### 31.数据可视化

1.MoviePy  使用https://zhuanlan.zhihu.com/p/36727011

2.PyQtGraph参考http://www.pyqtgraph.org/documentation/index.html

---

### 32.QCombobox

<https://doc.qt.io/qtforpython/PySide2/QtWidgets/QComboBox.html>

<https://zhuanlan.zhihu.com/p/36691866>

---

### 33.修改样式

1.setstylesheet <https://www.cnblogs.com/aheng123/p/5630761.html>

2.设置QListWidget透明背景—stylesheet  https://blog.csdn.net/liyan728/article/details/8955634

3.QListWidget 设置样式 https://www.bbsmax.com/A/KE5QOlL0zL/



---

### 34.QLabel Widget

1.PyQt - QLabel Widget https://www.tutorialspoint.com/pyqt/pyqt_qlabel_widget.htm

2.PyQt中QLabel背景与字体的一些设置 https://blog.csdn.net/jiuzuidongpo/article/details/45485127

3.QPalette https://doc.qt.io/qtforpython/PySide2/QtGui/QPalette.html

4.qss样式表之QPushButton https://blog.csdn.net/aiwangtingyun/article/details/94462976

5.setStyleSheet 一些QSS设置的集合https://www.cnblogs.com/xj626852095/p/3648112.html

---

### 35.PyQt & Matplotlib

1.nested pie chartshttps://matplotlib.org/3.2.0/gallery/pie_and_polar_charts/nested_pie.html#sphx-glr-gallery-pie-and-polar-charts-nested-pie-py

2.pie https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.pie.html

3.中文显示乱码https://www.jianshu.com/p/b5138e48fefa

4.embedin pyqt https://matplotlib.org/gallery/user_interfaces/embedding_in_qt_sgskip.html?highlight=pyqt

5.Matplotlib可视化50个图表https://www.jiqizhixin.com/articles/2019-01-15-11

6.https://matplotlib.org/3.2.1/api/_as_gen/matplotlib.figure.Figure.html

---

### 36.QLCDNumber

1.Qt 之 QLCDNumber https://blog.csdn.net/liang19890820/article/details/50917205

2.qLCDnumber https://www.riverbankcomputing.com/static/Docs/PyQt4/qLCDnumber.html

3.pyqt实现时钟效果 https://www.pythontab.com/html/2013/pythongui_0703/474.html

4.pyqt实现简易时钟 https://blog.csdn.net/Kprogram/article/details/83623079

5.QLCDNumber使用https://blog.csdn.net/xuancailinggan/article/details/77487705

---

### 37.QSpliter 

1.PyQt5布局管理之QSplitter（六）https://blog.csdn.net/jia666666/article/details/81705675

2.QSplitter 分割线 https://blog.csdn.net/skykingf/article/details/8247593

---

### 38.QDialog

1.PyQt5系列教程（8）：标准输入对话框https://zhuanlan.zhihu.com/p/29101077

---

### 39.conda创建单独环境

