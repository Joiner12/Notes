# Processing

## 什么是Processing



## 为什么要学Processing





## 学习资料

[Processing 入门基础【秒懂小白篇】_升卿的博客-CSDN博客_processing](https://blog.csdn.net/hewes/article/details/76034154)

[一天一点Processing|12网易云音乐动效并不难2——迷幻水波 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/104271430)

经验之谈

[作为一名交互设计师应该如何学习 Processing？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/22017067)

[processing生成设计学习之路 - 知乎 (zhihu.com)](https://www.zhihu.com/column/c_1177899269960450048)

1. [Tutorials / Processing.org](https://processing.org/tutorials/)

2. [Processing编程学习指南（原书第2版） (豆瓣) (douban.com)](https://book.douban.com/subject/26992338/)
3. [The Nature of Code (豆瓣) (douban.com)](https://book.douban.com/subject/20452058/)

## 零碎想法

博客更新

学习节点 多久学习到什么程度

# Processing编程学习指南

## 像素:paintbrush:

**坐标系和像素:pick:**

概念：坐标纸和电脑窗口坐标系都是采用笛卡尔坐标系统(Cartesian coordinate system)，坐标纸和显示器的坐标系不同点：坐标纸，坐标值y轴正半轴朝上，x轴正半轴朝右，原点在中央；电脑窗口，原点在左上角，y轴正半轴朝下，x轴正半轴朝右。显示器显示的最小单位是像素，每个像素就是一个有效坐标点。

![image-20220407143045234](https://cdn.jsdelivr.net/gh/Joiner12/PicBed@main/image-20220407143045234.png)

**绘制基本图形:triangular_ruler:**

Processing基本图形包含：点(point)、线(line)、矩形(rect)、椭圆(ellinpse)、三角形(triangle)、弧线(arc)、正方形(quad)、曲线(curve)等。

**灰度模式:grey_exclamation:**

灰度(grayscale)是一种颜色表示的方法，用一个字节表示的数值表示颜色逐渐从黑色到白色的过渡色。0表示黑色，255表示白色。

![image-20220407144141362](https://cdn.jsdelivr.net/gh/Joiner12/PicBed@main/image-20220407144141362.png)

**RGB颜色模式:computer:**

RGB——数位色彩(digital color)是指混合红(R)蓝(G)绿(B)三种颜色来实现不同的颜色表示。三通道RGB中按照顺序通过颜色混合，表示为(R,G,B)，其中每个值的范围是0-255。除了红蓝绿之外，还有另外一种元素可选，那就是颜色的alpha值，alpha值的0-255。0：完全透明，255：完全不透明。

**HSB颜色模式:taco: **

颜色除了用RBG(alpha)表示外，还可以用HSB颜色模式来表示，H(hue,色调)，S(saturation，饱和度)，B(brightness，亮度)。

**自定义颜色取值范围:sagittarius:**

默认颜色取值范围是0-255，但是这不是processing中颜色的唯一处理方式。计算机内存中，该值有一个计算机存储方式，因此可以支持自定义修改取值范围。

```java
// processing中自定义颜色取值范围的函数
colorMode() 
```

## 交互:first_quarter_moon:

**setup和draw**

processing的代码结构很简单，其通常结构如下：

```java
// Explicitly import library functions
import lib1;
import lib2;

void setup()
{
    // a block of code
}
void draw()
{
    // a block of code
}
    
    
```

运行项目的时候，首先执行一次setup然后执行跳转到draw中，最后不停循环执行draw函数。

**鼠标&键盘 :mouse:**

获取鼠标x坐标：`mouseX`，获取鼠标y坐标：`mouseY`。

获取鼠标上一个x坐标：`pmouseX`，获取鼠标上一个y坐标：`pmouseY`。

响应事件：鼠标（或键盘）所触发的事件。

函数mousePressed()处理鼠标操作，函数keyPressed()处理键盘操作。

## 变量:v:

坐标平移函数translate()，使用translate函数可以理解为将坐标参考原点进行平移。

## 数组:arrow_backward:

数组的创建和申明：

```java
//-------------------------------------------
// 数据类型 数组申明  数组名字           数组长度
//    |      |          |                |
    int      []     arrayName = new int[42];

    
```

## 条件语句 :ice_cream:

布尔表达式(Boolean expression)：用来衡量真或假的表达式。

**关系运算符号**

```java
// 常用的关系表达式
> 
<
>=
<=
!=
==
```

**if 、else、 else if**

```java
if (条件表达式1)
{
    // 条件表达式1为真，执行代码块
}
else if (条件表达式2)
{
    // 条件表达式2为真，执行代码块
}else
{
	// 上述条件都不满足，执行代码快    
};
```

**逻辑运算符:baby_chick:**

逻辑运算符包括：and—与：&& 、or或：|| 、not非：!

&，| 分别表示位运算符。

## 循环:white_circle:

迭代（iteration）：将一系列规则或者步骤不断重复产生的过程。

**while循环——你唯一真正需要的循环**

processing中有三个循环：while循环，do-while循环和for循环。

**for循环**

for循环由三部分组成：

- 初始值：变量在循环体重新被声明和初始化；
- 布尔测试：测试值为真和假的表达是，作为退出for迭代的条件；
- 迭代表达式：没个循环周期所要执行的指令。

**增（减）量运算符**

自增：++

自减：--

加等：+=

减等：-=

乘等：*=

除等：/=

**局部变量和全局变量**

作用域：变量有效的范围。存在于程序声明的整个周期的变量是全局变量。Processing中，有些变量是在setup()和draw()之外进行声明的，这些变量就是全局变量。存在于代码块内部的变量是局部变量。如函数中声明的变量。

**draw()循环的内部循环**

只有到了draw()循环的末尾，processing才会更新窗口的现实内容；

## PShape类:sailboat:

PShape可以存储通过一种算法构建的自定义的几何图形，以及一个外部文件载入的图形，比如可缩放的矢量图形（scalable vector graphics,SVG）,他是一种用于存储图形数据的标准格式。PShape对象可以通过createShape函数或者loadShape()进行创建。

## 图像:framed_picture:

