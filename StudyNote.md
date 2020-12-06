# C专家编程

## 第一章 C:穿越时空的迷雾

#### 1.早期C、Unix和相关的硬件系统

<img src="figure/c、unix和相关的硬件系统.png">



## 第二章 这不是Bug，而是语言特性

///

## 第三章 分析C语言的声明

### 1.用优先级解决声明问题

#### 1.1 优先级规则

```c
A	从名字开始读取，按照优先级顺序读取
B	优先级从高到低：
	B.1	声明中被括号括起来的部分
	B.2 后缀操作符：
		() → 函数
		[] → 数组
    B.3 前缀操作符：
    	* → 指向...的指针
C	const和（或）volatile关键字后紧跟类型说明符（int 、long），那么它作用于
	类型说明符。其他情况，const和（或）volatile作用于它左边紧邻的指针*。
```



### 2.typedef

**typedef**：为一种类型引入新的名字，而不是为变量分配空间，类似于宏文本替换。

##### 2.2 typedef .vs. #define

- 宏类型名扩展；
- 连续变量声明中，typedef定义类型可以保证变量均为同一类型，#define定义类型不能；

```c
#define peach int
#define mapv 1000	//classical usage
typedef int banana;

unsigned peach b = 7; 	// √
unsigned banana c = 3;	// error!
    
```

### 3.术语

类型模型（type model）

typedef (存储类型说明符)

### 4.声明（declarator）

##### 4.1 结构（Struct）

结构就是一种把一些数据组合在一起的数据结构。

结构通常形式：

```c
struct 结构标签(可选)
{
    类型1 标识符1;
    类型2 标识符2;
    ...
}变量定义(可选);
```



##### 4.2 联合(Union)

外表和结构相似，但是在内存布局上存在关键性的区别。

Union

```c
union 标签(可选)
{
    类型1 标识符1;
    类型2 标识符2;
    ...
}变量定义(可选);
```

联合中，所有成员都从偏移地址零开始存储。联合一般被用来节省空间，有些数据项不可能同时存在。

##### 4.3 枚举（Enum）

枚举通过一种简单的途径把一串名字于一串整型值联系在一起；

emum

```c
enum 标签（可选）
{
    内容
}定义变量（可选）;
```





## 第四章 令人震惊的事实：数组和指针并不相同

### 1.声明和定义

C语言中有且仅有一个定义，但可以有多个`extern`声明。

|  1   |             2              |                              3                               |
| :--: | :------------------------: | :----------------------------------------------------------: |
| 定义 | 只能出现在一个地方（一次） |  确定对象的类型并分配内存，用于创建新的对象：int value=10;   |
| 声明 |     可以出现在多个地方     | 描述对象的类型，用于指代其他地方定义的对象：extern int value |

### 2.指针和数组的差异

```c
char * p; // p是一个指针，指针指向的内存存储的是指针的内容
char tp[];// tp自身就是地址
```

相比较于数组，指针的操作需要多一个取地址的过程。



## 第五章 对链接的思考

### 1.动态链接& 静态链接

### 1.1 定义

函数库的拷贝，是可执行文件的物理组成部分，则称为静态链接。

可执行文件只包含文件名，载入器在运行是寻找可执行文件，则称为动态链接。

```c
*.a //a = archive，静态链接库
*.so // shared object 动态链接库
```

​	收集模块准备执行三阶段：链接-编辑（link-editing）、载入（loading）、运行时链接（runtime linking）。静态链接的模块被链接-编辑并载入以便运行。动态链接的模块被链接编辑后载入，并在运行时进行链接以便运行。

### 1.2 ABI

​	动态链接的目的是将程序与其所用的特定函数库版本分离。介于应用程序和函数库二进制可执行文件所提供的服务之间的接口，称之为应用二进制接口（Application Binary Interface,ABI）。

### 1.3 链接器（Linker）

​	编译器创建一个输出文件，这个文件包含可以重定向的对象。这些对象就是与源程序对应的数据和机器指令。

### 1.4 编译器（Compiler)

​	编译器包括（Compiler）：预处理器（Preprocessor）、语法和语义检查器（syntactic and semantic checker）、代码生成器（code generator）、汇编程序（assembler）、优化器（optimizer）、链接器（linker）。

```CQL
-# // 查看编译过程的各个独立阶段
-V // 查看版本信息

```



​	目标文件不能直接执行，需要载入到链接器中。链接器确认main函数为初始进入点，把符号引用（Symbolic Reference）绑定到内存地址，再把所有的目标文件集中在一起，加上库文件，从何产生可执行文件。



## 第六章 运动的诗章：运行时数据结构

### 6.1.a.out

a.out（Assembler Output）汇编输出，实际是连接器输出；

### 2.IntelX86和 Unix段（Segment）的区别

Intelx86中，内存模型设计为64kb大小的模块，一个模块就是一个段。

Unix表示一个二进制文件相关的块；

### 3.Unix 段内容

 Unix段：数据段、bbs段、文本段；

### 6.5 当函数被调用时发生了什么：过程活动记录

1.C语言自动提供的服务—跟踪调用链（哪些函数调用了哪些函数），当下一个return语句执行之后，控制将返回何处。

## 第九章 再论数组

### 9.1 什么时候数组与指针相同

​	实际应用中，数组和指针可以互换的场景比不能互换的场景多。

数组三种声明情况：

- 外部数组（external array）声明；
- 数组的定义（定义是声明的一种特殊情景，分配内存提供初始值）；
- 函数参数的声明；

`所有作为函数参数的数组名总是可以通过编译器转换为指针。`对编译器而言，一个数组就是地址，一个指针是地址的地址。



```c
int narrays[]  = {0,1,2,3};
int arraySize =sizeof(narrays)/sizeof(narrays[0]); // arraySize = 4;

```

**2.数组和指针（不）相同**

```c
/*
不同
*/
// 外部声明
extern char a[10];
// 定义
char a[10];

/*
相同
*/
// 函数形参
void function(char a_[]);
void function_1(char* a_);

// 表达式中使用
char b = a[0];
char b = *(a + index);
```

**3.数组引用**

**规则1：** 表达式中的数组名就是指针

```c
// 对数组的引用a[i]被编译器翻译成*(p+i)
int na[10]={0};
int *pna = na;
int nvalue = na[i];
nvalue == *(pna+i);

```

取下标操作符`[]` 自动将步长调整到数组元素的大小，这就是为什么不使用**sizeof**的原因。

取下标操作符`a[10]` 表示结果和 `10[a]` 相同。



**规则2：** C语言把数组下标作为指针的偏移量

不同方式访问速度问题；

**规则3：** 作为函数参数的数组名等同于指针

| 术语              | 定义                                                         |
| ----------------- | ------------------------------------------------------------ |
| 形参（parameter） | 它是一个变量，在函数定义或函数声明原型中定义，又称为形式参数（formal parameter） |
| 实参（argument）  | 它是一个值，在函数调用时传递给函数的值，又称实际参数（actual parameter） |

编译器只能向函数传递数组的指针而不是整个数组的拷贝。

### 9.6 C语言的多维数组

定义和引用多维数组的唯一方式就是使用多维数组。

```c
// 定义 → 访问 
typedef char Vegetable[20];
Vegetable bo[10];
b0[i][j]= *(*(bo+i)  + j )
```

**数组的数组。**



## 第十章 再论指针

#### 1.多维数组内存分配

内存是线性排列方式，不是表分配方式。

#### 2.指针数组就是Iliffe向量

通过声明一个一维指针数组，每个指针指向一个字符串来获取二维数组的效果。

```c
//sqush[i][j] 可能声明形式
int sqush[4][5]; // int型 二维数组
int *sqush[4]; // int 类型指针的数组Iliffe向量
int **sqush;	// int 类型执行指针的指针
int (*sqush)[5];// 类型为int数组（长度为5）的指针
```

#### 3.锯齿状数组上使用指针



#### 4.向函数传递一个一维数组



#### 5.使用指针向函数传递一个参数



#### 6.使用指针从函数返回一个数组



#### 7.使用指针创建和使用动态数组



## 第十一章 你懂得C，所以C++不在话下

### 11.1 OOP(object-oriented paradigm)概念

| 术语                  | 定义 |      |
| --------------------- | ---- | ---- |
| 抽象(abstraction)     |      |      |
| 类（class)            |      |      |
| 对象（object）        |      |      |
| 封装（encapsulation） |      |      |
| 继承(inheritance)     |      |      |

### 11.2 访问控制

| 控制字    | 描述 |      |
| --------- | ---- | ---- |
| public    |      |      |
| protected |      |      |
| private   |      |      |
| friend    |      |      |
| virtual   |      |      |



# 利用Python进行数据分析

## 第一章 准备工作

### 1.重要Python库

|    Lib     | Discription                                  |
| :--------: | -------------------------------------------- |
|   Numpy    | 科学计算基础包                               |
|   pandas   | 快速便捷地处理结构化数据的大量数据结构和函数 |
| matplotlib | 用于绘制数据图表的Python库                   |
|   SciPy    | 专门解决科学计算中各种标准问题域的包的集合   |
|    ...     | ...                                          |



## 第二章 ipython

```python
"""
	开发环境：python3.7 + anaconda + vs Code + spyder
"""
```

加强版ipython 不是最好的解决方案。



## 第三章 Numpy基础：数组和矢量计算

### 1.Numpy模块功能

- ndarray， 一个具有矢量算术运算和复杂广播能力的快速且节省空间的多维数
  组。
- 用于对整组数据进行快速运算的标准数学函数（ 无需编写循环） 。
- 用于读写磁盘数据的工具以及用于操作内存映射文件的工具。
- 线性代数、 随机数生成以及傅里叶变换功能。
- 用于集成由C、 C++、 Fortran等语言编写的代码的A C API。  

### 2.算法耗时分析

https://selfboot.cn/2016/06/13/python_performance_analysis/

### 3.Numpy的ndarray

#### 定义

ndarray：N维数组对象，快速而灵活的大数据集容器。

面向数组的编程和思维方式。

#### 创建ndarray

1.array—函数

array接受一切序列型数据对象，并将其转换为数组。



#### ndarray属性

| Property | Discription  | Other |
| -------- | ------------ | ----- |
| ndim     | 数组维度     |       |
| shape    | 数组形状     |       |
| dtype    | 数组数据类型 |       |



#### 2.其他

`zeros` 、`ones` 、`empty`创建。`empty`创建没有任何具体值的数组。要使用上述函数进行数组创建，只需要传入表示形状的元组。

| 函数              | 描述                                             | 其他           |
| ----------------- | ------------------------------------------------ | -------------- |
| zeros，zeros_like | 创建全零数组                                     |                |
| ones，ones_like   | 创建全1数组                                      |                |
| empty，empty_like | 分配内存，不填充数值                             | like：数组形状 |
| array             | 输入数据转换为数组                               |                |
| asarray           |                                                  |                |
| arange            | 类似于range函数                                  |                |
| full，full_like   | 用fill value中的所有值，根据shape和dtype创建数组 |                |
| eye，identity     | N*N单位对角矩阵                                  |                |
| ...               | ...                                              | ...            |



### 3.ndarray数据类型

dtype（ 数据类型） 是一个特殊的对象  。

- 数据类型
- 数据类型转换astype



### 4.Numpy数组的运算

#### 4.1 矢量化

矢量化（Vectorization）:大小相等数组之间的任何算数运算都会被应用到元素级。

**数组乘法**

```python
# python 
>>> a = np.array([1,2,3],[4,5,6])
>>> a*a
```



```matlab
% matlab
a = [[1,2,3];[4,5,6]]
a.*a 
```

**数组与标量运算**

**数组比较**

```python
>>> a = np.array([1,2,3])
>>> b = np.array([4,2,2])
>>> c = a>b

```



**广播(Broadcasting) **

大小不同数组之间的运算。

#### 4.2 切片与索引

切片方法`:` 。

```python
array[startIndex:endIndex]

```

切片使用标量赋值会自动广播到整个选区。

```python
arr_a = np.arange(10)
arr_aslice = arr_a[3:5]
arr_aslice = 1
```

对切片进行单值修改会体现在原始数组中。

数组显示复制而非切片视图。

切片复制：

```python
# 切片复制
arr_ascopy = arr_aslice.copy()
```



二维数组索引方式

```python
arr_tw = np.array([[1,2],[3,4]])

```

#### 4.3布尔型索引

通过bool数组进行索引；布尔型数组的长度必须跟被索引的轴长度一致。此外， 还可以将布尔型数组跟切片、 整数（ 或整数序列） 混合使用 。

```python
def boolIndex():
    print('bool index explore')
    arr_str = np.array(["bob","jack","nei","ham"])
    arr_randn = np.random.randn(4,7)
    name_bool = arr_str == 'bob'
    ah = arr_randn[name_bool]
    print(ah)
```

通过布尔型索引选取数组中的数据， 将总是创建数据的副本， 即使返回一模一样的
数组也是如此。
`注意` Python关键字and和or在布尔型数组中无效。 要使用&与|  。

#### 4.4 花式索引（Fancy indexing）

指利用整个数组进行索引。花式索引跟切片不一样， 它总是将数据复制到新数组中 。



#### 4.5 数组转置与轴对换

转置是重塑的一种特殊形式， 它返回的是源数据的视图（ 不会进行任何复制操作） 。对于高维数组，`transpose`需要得到一个由轴编号组成的元组才能对这些轴进行转置。简单的转置可以使用`.T`。

| 转置      |                          |      |
| --------- | ------------------------ | ---- |
| transpose | 转置是重塑的一种特殊形式 |      |
| T         | 轴对称变换               |      |
| swapaxes  |                          |      |

#### 4.6 通用函数：快速的元素级数组函数

通用函数（即ufunc）是一种对ndarray中的数据执行元素级运算的函数。



#### 4.7 利用数组进行数据处理

`矢量化`：用数组表达式代替循环的做法，通常被称为矢量化。

三元表达式：

```python
# python 实现方式
x if condition else y

#where 函数
np.where(cond,x,y)

```

#### 4.8 数学和统计方法

可以通过数组上的一组数学函数对整个数组或某个轴向的数据进行统计计算。sum、mean以及标准差std等聚合计算 （aggregation，通常叫做约简（reduction））既可以当做数组的`实例方法调用`，也可以当做`顶级NumPy函数使用`。

**基本数组统计方法**

| 方法           | 说明                                       |
| -------------- | ------------------------------------------ |
| sum            | 数组全部或者某轴向求和，零长度数组sum为0； |
| mean           | 算术平均数；零长度为NaN                    |
| std、var       | 标准差和方差，自由度可调整；               |
| min、max       | 最大值和最小值；                           |
| argmin、argmax | 最大值、最小值索引；                       |
| cumsum         | 所有元素累计和                             |
| cumprod        | 所有元素的累计积                           |
| ...            | ...                                        |

#### 4.9 用于bool型数组的方法

通用方法中，`True` 转换为`1`，`False `转换为`0`；

| 方法 | 说明             |
| ---- | ---------------- |
| sum  | 求所有True的个数 |
| any  | 至少存在一个True |
| all  | 是否所有都为True |

用于`非布尔型`数据，非0元素转换为1；



#### 4.10 排序

`sort()`

#### 4.11 唯一化以及其他的集合逻辑

| 方法             | 说明                              |
| ---------------- | --------------------------------- |
| unique(x)        | 计算x中的唯一元素，并返回有序结果 |
| intersect1d(x,y) | 计算x和y中公共元素，返回有序结果  |
| union1s(x,y)     | 计算x和y中的并集，并返回有序结果  |
| in1d(x,y)        | x的元素是否包含于y的布尔型数组    |
| setdiff1d(x,y)   | 集合的差，元素x不在y中            |
| setxor1d(x,y)    | 集合的对称性，xor函数             |
| ...              | ...                               |

#### 4.12 用于数组的文件输入输出

load()

save()

#### 4.13 线性代数

`nunpy.linalg`中有一组标准的矩阵分解运算以及诸如求逆和行列式之类的东西。它们跟MATLAB和R等语言所使用的是相同的行业标准级Fortran库，如BLAS、LAPACK、Intel MKL（可能有，取决于你的NumPy版本）等。



#### 4.14 随机数

`umpy.random`模块对Python内置的random进行了补充，增加了一些用于高效生成多种概率分布的样本值的函数。



## 第四章 pandas入门

### 1.数据结构介绍

两个主要数据结构：`Series`和`DataFrame`。

Series是一种类似于一维数组的对象，它由一组数据（各种NumPy数据类型）以及一组与之相关的数据标签（即索引）组成。

#### 1.1 Series

- 数据结构定义
- 数据索引
- numpy 对比
- 字典
- 数据缺失（检查`isnull` & `notnull` ）
- 根据索引对齐数据
- 索引修改

#### 1.2 DataFrame

DataFrame是一个表格型的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值、字符串、布尔值等）。 DataFrame既有行索引也有列索引，它可以被看做由Series组 成的字典（共用同一个索引）。



# sword means offer

## 1.Rope



动态规划&贪心算法

<https://github.com/Checkson/blog/issues/34>

<https://liweiwei1419.github.io/sword-for-offer/14-%E5%89%AA%E7%BB%B3%E5%AD%90/>

https://blog.csdn.net/qq_16234613/article/details/52235082



**https://web.stanford.edu/class/cs97si/**

## 2.非符号运算加

1.异或&同或

${a⊙b = ab + a'b'}$

$a $^$ b = a'b + b'a$

2.位运算

https://blog.nowcoder.net/n/dcbca76d214744a9a1644ae54a183549

https://segmentfault.com/a/1190000015796106



## 3.NoteDepth

1.https://www.cnblogs.com/aademeng/articles/11309253.html

2.https://www.cnblogs.com/edisonchou/p/4823213.html





# Kalman Filter

## 1.Reference

[1]《Math\]理解卡尔曼滤波器 (Understanding Kalman Filter)》

<https://segmentfault.com/a/1190000000514987>

[2]《细说Kalman滤波：The Kalman Filter》★★★

<https://www.cnblogs.com/ycwang16/p/5999034.html>

[3]《H无穷滤波器和Kalman滤波器比较》

<https://wenku.baidu.com/view/6e7035323968011ca3009147.html>

[4]《MATLAB VAR函数》

<https://blog.csdn.net/ouening/article/details/51281242>

[5] 《EKF》★★★

<https://blog.csdn.net/Q_18163961/article/details/52505591>

[6]《KF、EKF、UKF、PF》

<https://blog.csdn.net/drilistbox/article/details/80506249>

[7] 《贝叶斯滤波器》

<https://www.cnblogs.com/aipiano/p/9060054.html>

[8] <>

<http://www.tina-vision.net/docs/memos/2003-003.pdf>

[9] 《KALMAN滤波的假设》

<https://www.cnblogs.com/HaoQChen/p/11048610.html>

[10]  Kalman Filter Method

<http://www.sherrytowers.com/kalman_filter_method.pdf>

[13]kalman tutorial

https://www.kalmanfilter.net/default.aspx

[14]

https://zhuanlan.zhihu.com/p/151818920

[16]

https://zhuanlan.zhihu.com/p/36374943

Fundamentals of Kalman Filtering A Practical Approach.pdf

https://zhuanlan.zhihu.com/p/125554723



https://blog.csdn.net/qq_33835307/article/details/82935682

https://blog.csdn.net/u010703122/article/details/49074297

https://zhuanlan.zhihu.com/p/59681380

## 2.CODE

**MATLAB**

```matlab
clear
N=200;%取200个数
%% 生成噪声数据 计算噪声方差
% 产生一个1×N的行向量，第一个数为0
% w为过程噪声（其和后边的v在卡尔曼理论里均为高斯白噪声）
w=randn(1,N); 
w(1)=0;
 % R、Q分别为过程噪声和测量噪声的协方差
 % (此方程的状态只有一维，方差与协方差相同) 
Q=var(w);

v=randn(1,N);%测量噪声
R=var(v);

%% 计算真实状态
x_true(1)=0;%状态x_true初始值
A=1;% a为状态转移阵，此程序简单起见取1
for k=2:N
 	% 系统状态方程，k时刻的状态等于k-1时刻状态乘以状态转移阵加噪声
 	% 控制输入量位0，
    x_true(k)=A*x_true(k-1)+w(k-1); 
end

%% 由真实状态得到测量数据， 测量数据才是能被用来计算的数据， 其他都是不可见的
H=0.2;
z=H*x_true+v;%量测方差，c为量测矩阵，同a简化取为一个数


%% 预测-更新过程

% x_predict: 预测过程得到的x
% x_update:更新过程得到的x
% P_predict:预测过程得到的P
% P_update:更新过程得到的P

%初始化误差 和 初始位置
x_update(1)=x_true(1);%s(1)表示为初始最优化估计
P_update(1)=0;%初始最优化估计协方差

for t=2:N
    %{
    -------------------1. 预测-------------------
    %}
    %-----1.1 预测状态-----
    x_predict(t) = A*x_update(t-1); %没有控制变量
    %-----1.2 预测误差协方差-----
    %{
    	p1为一步估计的协方差，
    	此式从t-1时刻最优化估计s的协方差得到t-1时刻到t时刻一步估计的协方差
    %}
    P_predict(t)=A*P_update(t-1)*A'+ Q;
    %{
    -------------------2. 更新-------------------
    %}
    %-----2.1 计算卡尔曼增益-----
    %{
   		仿真程序需要使用R，实际过程中，R存在于观测值中，是客观到物理量
    %}
    k(t)=H*P_predict(t) / (H*P_predict(t)*H'+R);
    % b为卡尔曼增益，其意义表示为状态误差的协方差与量测误差的协方差之比(个人见解)
   
   	%-----2.2 更新状态-----
   	% Y(t)-a*c*s(t-1)称之为新息，是观测值与一步估计得到的观测值之差，
    % 此式由上一时刻状态的最优化估计s(t-1)得到当前时刻的最优化估计s(t)
    x_update(t)=x_predict(t)  +  K(t) * (z(t)-H*x_predict(t));
    
    %-----2.3 更新误差协方差-----
    %此式由一步估计的协方差得到此时刻最优化估计的协方差
    P_update(t)=P_predict(t) - H*K(t)*P_predict(t);
end

%% plot
%作图，红色为卡尔曼滤波，绿色为量测，蓝色为状态
%kalman滤波的作用就是 由绿色的波形得到红色的波形， 使之尽量接近蓝色的真实状态。
t=1:N;
plot(t,x_update,'r',t,z,'g',t,x_true,'b');
legend('kalman','obser','true')

```

C Code Ver.1.0

```c
/*********************kalman.h**********************/
#pragma once
/*
	Created date:2019-7-8
	Kalman Filter
*/ 
typedef struct
{
	double nVarQ;			// 过程噪声方差
	double nVarR;			// 观测噪声方差
	double nPreX;			// X(k-1|k-1)
	double nKg;				// kalman增益
	double nPreZ;			// Z(k-1|k-1)
	double nP;				// 协方差
	double nU;				// 控制量
	double nXreal;			// 真实状态量
}tKalman;

tKalman* KalmanGet();

void KalmanInit(tKalman* pSelf_, double nVarQ_, double nVarR_);

void KalmanProcess(tKalman* pSelf_, double nZk_,double nUk_);

void Kalman_Test();


/*********************kalman.c**********************/
#include "stdafx.h"
#include "kalman.h"

tKalman g_tKalman;

/*
Kalman Filter
Q:过程噪声，Q增大，动态响应变快，收敛稳定性变坏
R:测量噪声，R增大，动态响应变慢，收敛稳定性变好
/------------预测-----------/
X(k | k - 1) = X(k - 1 | k - 1)	+ u(k)		(1)	状态预测
P(k | k - 1) = P(k - 1 | k - 1) + Q			(2)	预测方差
/-----------更新------------/
K(k)=P(k|k-1)/（P(k|k-1)+R）					(3)	更新kalman增益
X(k|k)=X(k|k-1)+K(k)*（Z(k)-X(k|k-1)）		(4)	状态更新
P(k|k)=（1-K(k)）*P(k|k-1)					(5)	滤波方差更新
*/

// 获取全局变量
tKalman* KalmanGet()
{
	return 	&g_tKalman;
}

void KalmanInit(tKalman* pSelf_, double nVarQ_, double nVarR_)
{
	nVarQ_ > 0 ? pSelf_->nVarQ = nVarQ_ : pSelf_->nVarQ = 0.0;
	nVarR_ > 0 ? pSelf_->nVarR = nVarR_ : pSelf_->nVarR = 0.0;
	pSelf_->nKg = 0.0;
	pSelf_->nP = 10.0;			// 初始化不为零
	pSelf_->nPreX = 0.0;			// 初始状态x(k-1|k-1)
	pSelf_->nU = 0.0;
	pSelf_->nXreal = 0.0;
}

void KalmanProcess(tKalman* pSelf_, double nZk_, double nUk_)
{
	int _nAs = 1;//A状态矩阵
	/*
		X(k | k - 1) = X(k - 1 | k - 1) + u(k)		(1)	状态预测
	*/
	double _nXKK_1 = (pSelf_->nPreX)*_nAs + nUk_;
    /*
	P(k | k - 1) = P(k - 1 | k - 1) + Q			(2)	预测方差
    */
    double _nPkk_1 = pSelf_->nP + pSelf_->nVarQ;

    /*
        K(k)=P(k|k-1)/（P(k|k-1)+R）					(3)	更新kalman增益
    */
    double _nKg = _nPkk_1 / (_nPkk_1 + pSelf_->nVarR);
    pSelf_->nKg = _nKg;

    /*
        X(k|k)=X(k|k-1)+K(k)*（Z(k)-X(k|k-1)）		(4)	状态更新
    */
    double _nXkk = _nXKK_1 + _nKg * (nZk_ - _nXKK_1);
    pSelf_->nPreX = _nXkk;
    pSelf_->nPreZ = nZk_;

    /*
        P(k|k)=（1-K(k)）*P(k|k-1)					(5)	滤波方差更新
    */
    double _nPkk = (1 - _nKg)*_nPkk_1;
    pSelf_->nP = _nPkk;
}
void Kalman_Test()
{
	cout << "Simulator for kalman filter" << endl;
	int _nLoopCnt = 0;
	ofstream kalman("kalman.txt");
	clock_t tStart, tEnd;
	tStart = clock();
	while (++_nLoopCnt <= 1000)
	{
		if (_nLoopCnt == 1)
		{
			double _nVarQ = 10;
			double _nVarR = 10;
			KalmanInit(KalmanGet(), _nVarQ, _nVarR);
			srand((unsigned)time(NULL));
		}
		else
		{
			// x(k) = a*x(k-1) + w1(k) + u(k)
			// sin(2*pi*f*t)
			static double _nFre = 2 * 3.1415 * 0.1 * 0.1;
			double _nUk = 10 * sin(_nFre*_nLoopCnt);
			// 真实状态
			double _nXreal = _nUk + KalmanGet()->nXreal;// +(rand() % 10 - 5.0);
			// z(k) = h*x(k)+w(k); 带观测噪声观测值
			double _nZk = _nXreal + (rand() % 10 - 1.0);


		KalmanProcess(KalmanGet(), _nZk, _nUk);
		KalmanGet()->nXreal = _nXreal;
		double _nXkk = KalmanGet()->nPreX;
		kalman << _nLoopCnt * 0.1 << "," << _nXreal << "," << _nZk << "," 			<< _nXkk << endl;
		}
    }
    kalman.close();
    tEnd = clock();
    cout << "Operation duration:" << (tEnd - tStart) << endl;
}
```

%% 数据处理

```matlab
%% 测试kalman.h .c
%{
    获取处理数据
%}
clc;
datapath = 'D:\Codes\VsProjects\LeetCode\LeetCode';
filename = 'kalman.txt';
file = strcat(datapath,'\',filename);

origin = load(file);
if isequal(length(origin),0)
    warning('数据导入出错');
end
time_k = origin(:,1);
real_x = origin(:,2);
obser_x = origin(:,3);
kalman_x = origin(:,4);

figure(1)
p = plot(time_k,real_x,time_k,obser_x,time_k,kalman_x);
p1.LineWidth = 2;
grid on 
legend('real','obser','kalman')
```



## 3.（协）方差 | 期望 | 标准差

#### 3.1《方差，协方差、标准差，与其意义》

<https://blog.csdn.net/yangdashi888/article/details/52397990>

均值：样本集合的中间点；

方差：样本点到样本中间点距离的均值；

标准差：sqrt(方差)；

协方差：表示两组数据的相关度（正负相关）

#### 3.2 std、var函数

var计算矩阵（数组）的方差；

<https://ww2.mathworks.cn/help/matlab/ref/var.html>



## 4.Kalman滤波推导过程

$$
Reference:https://www.cnblogs.com/ycwang16/p/5999034.html
$$



#### 4.1 Extented Kalman

（1）扩张卡尔曼滤波是将非线性系统线性化，然后进行滤波，其本质是还是线性滤波器，且存在一定的局限性，强非线性违背局部线性假设，Taylor展开式中大偏差的高阶项被忽略，但可能会造成滤波发散；

（2）Jacobian matrix

#### 4.2 KF解决的问题

1. Kalman滤波所解决的问题，是对一个动态变化的系统的状态跟踪的问题，基本的模型假设包括：1）系统的状态方程是线性的；2）观测方程是线性的；3）过程噪声符合零均值高斯分布；4）观测噪声符合零均值高斯分布；从而，一直在线性变化的空间中操作高斯分布，状态的概率密度符合高斯分布。

2. 对于线性系统，零均值高斯噪声的系统，Kalman是理论上无偏的，最优滤波器；

3. Kalman滤波在实际使用中，要注意参数R和Q的调节，这两者实际上是相对的，表示更相信观测还是更相信预测。具体使用时，R可以根据过程噪声的幅度决定，然后Q可以相对R来给定。当更相信观测时，把Q调小，不相信观测时，把Q调大；

4. Q越大，表示越不相信观测，这是系统状态越容易收敛，对观测的变化响应越慢。Q越小，表示越相信观测，这时对观测的变化响应快，但是越不容易收敛。Q、R值的大小表示置信度大小；

5. 贝叶斯的马尔卡夫假设

   假设当前状态S（k）只与S(k-1)相关，与之前（0，k-2）状态无关；

#### 4.3 KF

$$
\begin{align}
&X(k) = A*X(K-1) + B*U(K-1) + \delta (k) \\
&Z(k) = H*X(k) + \epsilon (k)\\

&**Predication**\\
&1.状态预测\\
&X(k|k-1) = A*X(k|k) + B*u(k|k)\\
&2.预测协方差矩阵\\
&P(k|k-1) = A*P(k|k)*A' + R(k)...R(k)：过程噪声方差\\
&**Corection**\\
&3.Kalman增益\\
&K(k|k) = P(k|k-1)*H(k)'*(H(k)*P(k|k-1) + Q(K))^{-1}\\
&4.基于观测值的状态更新\\
&X(k|k) = X(k|k-1) + k(k|k)*(Z(k) - H(k)*X(k|k-1))\\
&5.更新状态的方差矩阵\\
&P(k|k) = (I - k(k|k)*H(k))*P(k|k)\\
\end{align}
$$



​	

