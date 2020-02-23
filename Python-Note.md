# Python Note

### 1.Lib-datetime

1.python 时间库

<https://www.cnblogs.com/vamei/archive/2012/09/03/2669426.html>

---

### 2.文件操作

1.检查路径是否存在

<https://www.cnblogs.com/jhao/p/7243043.html>

---

### 3.Anaconda

1.《anaconda离线安装第三方包》

<https://blog.csdn.net/qq_39657585/article/details/82667450>

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